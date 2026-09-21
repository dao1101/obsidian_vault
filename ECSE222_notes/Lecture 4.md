```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity mux21 is
    Port (
        s, x1, x2: in std_logic;
        f: out std_logic;
    );
end mux21;

--Structural
architecture logicfunc of mux21 is
begin
    f <= (x2 AND s) OR ((NOT s) AND x1);
end logicfunc;


--Behavioural
architecture Behavioral of mux21 is
begin
    with s select
	    f <= x1 when '0',
		     x2 when '1',
		     'X' when others;
end Behavioral;

--Signals
--The order does not matter since this is not programming.
architecure logicfunc of mux21 is
	signal sig1, sig2 : std_logic;
begin
	sig1 <= x1 and (not s); --transferring value into the signal
	sig2 <= s and x2;
	f <= sig1 or sig2;
end logicfunc
```
==Note: VHDL does not assume precedence, need to use parenthesis==

### Data type
- type must be fixed at signal declaration
	- in entity: port declaration
	- in architecture: signal declaration
- two main data types
	- scalar types - integer real, enumerated
	- composite types - arrays and records
		- arrays: collection of signals of the same type
			- `string(array of character)`
			- `std_logic_vector(array of std_logic)`

#### Concatenation operator `&` (RHS of <=)
```vhdl
architecture class1 of canct is
	signal byte: bit_vector (7 downto 0);
	signal A_bus, B_bus: bit_vector (3 downto 0);
	
begin
byte <= A_bus & B_bus;
end class1;
```

Cross switch example

![[Screenshot 2026-09-14 at 12.35.20.png|246]]![[Screenshot 2026-09-14 at 12.35.40.png|301]]
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Xbar is
port(x: in std_logic_vecotr(1 downto 0); --2 bits
	 s: in std_logic;
	 y: out std_logic_vector(1 downto 0); --2 bits
);
end Xbar;

--Structural
architecture Structure of Xbar is
	component mux21 --calling the component made before
	port (s, x1, x2: in std_logic;
		  f: out std_logic);
	end component;
begin
	--M1 and M2 are instances of mux21
	M1: mux21 port map (s, x(0), x(1), y(0)); --the order must match the  components ports order.
	M2: mux21 port map (x1 =>x(1), x2 => x(0), f => y(1), s => s);
	--`=>` mapper symbol, order deos not matter here
end structure;

--Beharvioural
architecture Behaviour of Xbar is 
begin
	with s select
		y <= x(1) & x(0) when 0, --concatenation used to put 2 bits together, corresponding y(1) and y(0)
	         x(0) & x(1) when 1;
end Behaviour;
```