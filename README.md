LIBRARY IEEE;
USE ieee.std_logic_1164.all;
---------------------------------------------------------
ENTITY selector IS
  PORT (     sws    : IN  STD_LOGIC_VECTOR(1 DOWNTO 0);--Switchs para definirla operacion a realizar
             auxi   : OUT STD_LOGIC;--Segundo auxiliar de 1 bit
             resret : IN  STD_LOGIC_VECTOR(7 DOWNTO 0);--Resultado de la resta codificada de 4 a 8 bits
				 resm   : IN  STD_LOGIC_VECTOR(7 DOWNTO 0);--Resultado de la multiplicacion de 8 bits
				 resat  : IN  STD_LOGIC_VECTOR(7 DOWNTO 0);--Resultado de la suma codificada de 4 a 8 bits
				 todis  : OUT STD_LOGIC_VECTOR(7 DOWNTO 0));--Resultado de la operacion seleccionada en el selector
END ENTITY selector;
----------------------------------------------------------
ARCHITECTURE mux OF selector IS
BEGIN
   WITH sws SELECT--Se tiene en cuenta los sws para definir la operacion y valor de todis dependiendo del caso
	
  todis <= 
   resret WHEN "01",--Se utiliza el resultado codificado de la resta cuando es "01"
	resat  WHEN "11",--Se utiliza el resultado codificado de la suma cuando es "11"
	resm   WHEN OTHERS;--En otros casos se asume el resultado de la multiplicacion
	
  with sws select--Se tiene de nuevo en cuenta los sws para definir el valor del segundo auxiliar auxi
  auxi <= 
    '1' WHEN "01",--
	 '0' WHEN OTHERS;
	
END mux;
