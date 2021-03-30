# 07-ffs
## Preparation:

![qD](Images/eqnD.png)

![qJK](Images/eqnJK.png)

![qT](Images/eqnT.png)


| **clk** | **d** | **q(n)** | **q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-- |
   | ![rising](Images/eq_uparrow.png) | 0 | 0 | 0 | No change |
   | ![rising](Images/eq_uparrow.png) | 0 | 1 | 0 | Store |
   | ![rising](Images/eq_uparrow.png) | 1 | 0 | 1 | Store |
   | ![rising](Images/eq_uparrow.png) | 1 | 1 | 1 | No change |

   | **clk** | **j** | **k** | **q(n)** | **q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-: | :-- |
   | ![rising](Images/eq_uparrow.png) | 0 | 0 | 0 | 0 | No change |
   | ![rising](Images/eq_uparrow.png) | 0 | 0 | 1 | 1 | No change |
   | ![rising](Images/eq_uparrow.png) | 0 | 1 | 0 | 0 | Reset |
   | ![rising](Images/eq_uparrow.png) | 0 | 1 | 1 | 0 | Reset |
   | ![rising](Images/eq_uparrow.png) | 1 | 0 | 0 | 1 | Set |
   | ![rising](Images/eq_uparrow.png) | 1 | 0 | 1 | 1 | Set |
   | ![rising](Images/eq_uparrow.png) | 1 | 1 | 0 | 1 | Toggle |
   | ![rising](Images/eq_uparrow.png) | 1 | 1 | 1 | 0 | Toggle |

   | **clk** | **t** | **q(n)** | **q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-- |
   | ![rising](Images/eq_uparrow.png) | 0 | 0 | 0 | No change |
   | ![rising](Images/eq_uparrow.png) | 0 | 1 | 1 | No change |
   | ![rising](Images/eq_uparrow.png) | 1 | 0 | 1 | Invert(Toggle) |
   | ![rising](Images/eq_uparrow.png) | 1 | 1 | 0 | Invert(Toggle) |
   
   ## D-latch:
   ### p_d_latch:
      ```vhdl
      p_d_latch : process (d, arst, en)
    begin
        if (arst = '1') then
            q     <= '0';
            q_bar <= '1';
        elsif (en = '1')then
            q <= d;
            q_bar <= not d;
        end if;
    end process p_d_latch;
      ```
   ### tb_d_latch:
     ```vhdl
     p_reset_gen : process
    begin
        s_arst <= '0';
        wait for 15 ns;
        -- Reset activated
        s_arst <= '1';
        wait for 27 ns;
        s_arst <= '0';
        wait for 58 ns;
        -- Reset activated
        s_arst <= '1';
        wait for 12 ns;
        s_arst <= '0';
        wait;
    end process p_reset_gen;

    --------------------------------------------------------------------
    -- Data generation process
    --------------------------------------------------------------------
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        
        s_en <= '0';
        s_d <= '0';
        
        --sequence
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        --end sequence
        
        s_en <= '1';
        
        --sequence
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        --end sequence
        
        s_en <= '0';
        
        --sequence
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        --end sequence
        
        s_en <= '1';
        
        --sequence
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_en <= '1';
        wait for 10 ns;
        s_d <= '0';
        --end sequence
        
        --sequence
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        --end sequence
        
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;     
     ```
### Waveforms:
![Waves](Images/Wavu1.png)

## Flip flops:
### processes:
#### p_d_ff_arst
   ```vhdl
       p_d_ff_arst : process (clk, arst)             
    begin                                         
        if (arst = '1') then                      
            q  <=   '0';                         
            q_bar <=   '1';
                                    
        elsif  rising_edge(clk) then                    
            q  <=   d;                               
            q_bar <=   not d;                       
        end if;                                   
    end process p_d_ff_arst; 
   ```
#### p_d_ff_rst
   ```vhdl
   p_d_ff_rst : process (clk)             
    begin
        if rising_edge(clk) then
            if (rst = '1') then
                q  <=   '0';
                q_bar <=   '1';
            else
                q   <=   d;
                q_bar <=   not d;
            end if; 
        end if;
    end process p_d_ff_rst;
   ```
#### p_jk_ff_rst
   ```vhdl
   p_jk_ff_rst : process (clk)             
    begin                                         
      if rising_edge(clk) then 
          if (rst = '1') then
              s_q <= '0';
          else
                 if (j = '0' and k = '0') then
                  s_q  <=  s_q;
                  
              elsif (j = '0' and k = '1') then
                  s_q  <=  '0';
                  
              elsif (j = '1' and k = '0') then
                  s_q  <=  '1';
                  
              elsif (j = '1' and k = '1') then                   
                  s_q  <=  not s_q; 
                   
              end if; 
            end if;                   
        end if;                                   
    end process p_jk_ff_rst;
   ```
#### p_t_ff_rst
   ```vhdl
   p_t_ff_rst : process (clk)
    begin
        if rising_edge(clk) then
            if (rst = '1') then
                s_q <=  '0';
                s_q_bar <=  '1';
            else
                if (t = '0') then
                    s_q <=   s_q;
                    s_q_bar <=   s_q_bar;
                else
                    s_q  <=  not s_q;
                    s_q_bar <=  not s_q_bar;
                end if;    
            end if;
        end if;
    end process p_t_ff_rst;
   ```   
## Shift register:
![block](Images/DE1PC7.png)
