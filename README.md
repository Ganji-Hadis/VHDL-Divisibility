# VHDL-Divisibility
Divisibility to 3 & 11


    library IEEE;
    use IEEE.STD_LOGIC_1164.ALL;
    use IEEE.std_logic_arith.all;

    -------------------------------------------------------------------------------
    entity Divisibility is
    	port( A, B, C, D ,E ,F ,G ,H : IN STD_LOGIC_VECTOR(3 DOWNTO 0);
		      	output_1 , output_2 : out bit);
    end Divisibility;

    -------------------------------------------------------------------------------
    architecture Behavioral of Divisibility is
  	signal sum_1 , sum_2 : INTEGER;                     --result of the sumation of inputs
	  signal div_1 , div_2 : INTEGER;                     --result of division to 3 & 11
    begin

    ----------------- check Divisibility to 3
	sum_1 <= (8*CONV_INTEGER(A(3))+ 4*CONV_INTEGER(A(2))+ 2*CONV_INTEGER(A(1))+ CONV_INTEGER(A(0))) + (8*CONV_INTEGER(B(3))+ 4*CONV_INTEGER(B(2))+ 2*CONV_INTEGER(B(1))+ CONV_INTEGER(B(0))) + (8*CONV_INTEGER(C(3))+ 4*CONV_INTEGER(C(2))+ 2*CONV_INTEGER(C(1))+ CONV_INTEGER(C(0))) + (8*CONV_INTEGER(D(3))+ 4*CONV_INTEGER(D(2))+ 2*CONV_INTEGER(D(1))+ CONV_INTEGER(D(0)));
	div_1 <= sum_1 mod 3 ;
	
	output_1 <= '1' when div_1 = 0 else
					'0' ;
					
					
    ----------------- check Divisibility to 11
	sum_2 <= (8*CONV_INTEGER(E(3))+ 4*CONV_INTEGER(E(2))+ 2*CONV_INTEGER(E(1))+ CONV_INTEGER(E(0))) - (8*CONV_INTEGER(F(3))+ 4*CONV_INTEGER(F(2))+ 2*CONV_INTEGER(F(1))+ CONV_INTEGER(F(0))) + (8*CONV_INTEGER(G(3))+ 4*CONV_INTEGER(G(2))+ 2*CONV_INTEGER(G(1))+ CONV_INTEGER(G(0))) - (8*CONV_INTEGER(H(3))+ 4*CONV_INTEGER(H(2))+ 2*CONV_INTEGER(H(1))+ CONV_INTEGER(H(0)));
	div_2 <= sum_2 mod 11 ;
	
	output_2 <= '1' when div_2 = 0 else
				   '0' ;
    end Behavioral;


#TestBench

    LIBRARY ieee;
    USE ieee.std_logic_1164.ALL;
    use IEEE.std_logic_arith.all;

    --------------------------------------------------------------------------
    ENTITY az2test IS
    END az2test;

    --------------------------------------------------------
    ARCHITECTURE behavior OF az2test IS 
 
    -- Component Declaration for the Unit Under Test (UUT)
 
    COMPONENT Divisibility
    PORT(
         A : IN STD_LOGIC_VECTOR(3 DOWNTO 0);
			B : IN STD_LOGIC_VECTOR(3 DOWNTO 0);
         C : IN STD_LOGIC_VECTOR(3 DOWNTO 0);
         D : IN STD_LOGIC_VECTOR(3 DOWNTO 0);
         E : IN STD_LOGIC_VECTOR(3 DOWNTO 0);
         F : IN STD_LOGIC_VECTOR(3 DOWNTO 0);
         G : IN STD_LOGIC_VECTOR(3 DOWNTO 0);
         H : IN STD_LOGIC_VECTOR(3 DOWNTO 0);
         output_1 : out bit;
         output_2 : out bit
        );
    END COMPONENT;
    

     --Inputs
     signal A : STD_LOGIC_VECTOR(3 DOWNTO 0);
     signal B : STD_LOGIC_VECTOR(3 DOWNTO 0);
     signal C : STD_LOGIC_VECTOR(3 DOWNTO 0);
     signal D : STD_LOGIC_VECTOR(3 DOWNTO 0);
     signal E : STD_LOGIC_VECTOR(3 DOWNTO 0);
     signal F : STD_LOGIC_VECTOR(3 DOWNTO 0);
     signal G : STD_LOGIC_VECTOR(3 DOWNTO 0);
     signal H : STD_LOGIC_VECTOR(3 DOWNTO 0);

 	--Outputs
     signal output_1 : bit;
      signal output_2 : bit;
     -- No clocks detected in port list. Replace <clock> below with 
    -- appropriate port name 
 

 
    BEGIN
 
	-- Instantiate the Unit Under Test (UUT)
     uut: Divisibility PORT MAP (
          A => A,
          B => B,
          C => C,
          D => D,
          E => E,
          F => F,
          G => G,
          H => H,
          output_1 => output_1,
          output_2 => output_2
        );


     -- Stimulus process
     stim_proc: process
       begin		

		wait for 100 ns;	
      A <= "0010" ;
		B <= "0011" ;
		C <= "0101" ;
		D <= "0001" ;
		wait for 100 ns;
		
      A <= "0010" ;
		B <= "0001" ;
		C <= "0000" ;
		D <= "0000" ;
		wait for 100 ns;
		
		E <= "1001" ;
		F <= "0011" ;
		G <= "0111" ;
		H <= "0000" ;
		wait for 100 ns;
		
		E <= "1001" ;
		F <= "1001" ;
		G <= "0000" ;
		H <= "0000" ;
		wait;
		
    end process;

    END;
