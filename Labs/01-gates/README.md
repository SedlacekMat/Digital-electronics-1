# Lab assignment 01-gates

## 1. Repository link:

Link to Digital-electronics-1 repository: [SedlacekMat/Digital-electronics-1](https://github.com/SedlacekMat/Digital-electronics-1.git)

## 2. De Morgan's law:

Link to EDA playground: [EDA De Morgan's law](https://www.edaplayground.com/x/QQSh#)

```vhdl
library ieee;               -- Standard library
use ieee.std_logic_1164.all;-- Package for data types and logic operations

------------------------------------------------------------------------
-- Entity declaration for basic gates
------------------------------------------------------------------------
entity gates is
    port(
        a_i    : in  std_logic;         -- Data input
        b_i    : in  std_logic;         -- Data input
        c_i    : in  std_logic;         -- Data input
        f_o    : out std_logic;         -- OR output function
        fnand_o: out std_logic;         -- AND output function
        fnor_o : out std_logic          -- XOR output function
    );
end entity gates;

------------------------------------------------------------------------
-- Architecture body for basic gates
------------------------------------------------------------------------
architecture dataflow of gates is
begin
    f_o     <= ((not b_i) and a_i) or ((not c_i) and (not b_i));
    fnand_o <= ((b_i nand b_i) nand (a_i)) nand ((c_i nand c_i) nand (b_i nand b_i));
    fnor_o  <= (((b_i) nor (a_i nor a_i)) nor ((c_i) nor (b_i)))nor(((b_i) nor (a_i nor a_i)) nor ((c_i) nor (b_i)));

end architecture dataflow;
```

| **c** | **b** |**a** | **f(c,b,a)** |
| :-: | :-: | :-: | :-: |
| 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 |

![alt text](https://github.com/SedlacekMat/Digital-electronics-1/blob/main/Labs/01-gates/DeMorganScreen.png)


## 3. Distribution laws

Link to EDA playground: [EDA Distribution laws](https://www.edaplayground.com/x/Ld__)

```vhdl
library ieee;               -- Standard library
use ieee.std_logic_1164.all;-- Package for data types and logic operations

------------------------------------------------------------------------
-- Entity declaration for basic gates
------------------------------------------------------------------------
entity gates is
    port(
        x_i    : in  std_logic;         -- Data input
        y_i    : in  std_logic;         -- Data input
        z_i    : in  std_logic;         -- Data input
        d1l_o  : out std_logic;         -- Left side of first Distribution law output function
        d1r_o : out std_logic;          -- Right side of first Distribution law output function
        d2l_o : out std_logic;          -- Left side of second Distribution law output function
        d2r_o : out std_logic           -- Right side of second Distribution law output function
    );
end entity gates;

------------------------------------------------------------------------
-- Architecture body for basic gates
------------------------------------------------------------------------
architecture dataflow of gates is
begin
    d1l_o <= (x_i and y_i) or (x_i and z_i);
    d1r_o <= x_i and (y_i or z_i);
    d2l_o <= (x_i or y_i) and (x_i or z_i);
    d2r_o <= x_i or (y_i and z_i);

end architecture dataflow;
```
![alt text](https://github.com/SedlacekMat/Digital-electronics-1/blob/main/Labs/01-gates/DistributiveScreen.png)
