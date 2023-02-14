# CmdLM - a program for matching unit cells from different crystals #

## Author: Larry Andrews larry6640995@gmail.com
## and Herbert J. Bernstein

## Summary
CmdLM is a command-line program for matching unit cells   
from different crystals.  It is executed as a program call  
without arguments, followed by a list of unit cells.  The   
first input cell is treated as a reference to which the   
following cells will be  "matched".  The list is ended   
by a single line beginning with "end".  The program  
matches cells in terms of "similarity", measured as a  
scale-independent angle between G6 vectors.

## Motivation: 
CmdLM is a command line program to make  
available certain capabilities of the research  
code in LatticeRepLib (Lattice Represention Libarary),  
a package of many funtions for implementing computations  
about the properties of lattices. The package allows for  
descriptions in many different basic forms.
	
CmdLM is a single purpose program. Input consists  
of a series of single line inputs, one for each  
input unit cell. The first input cell is treated as 
a  
reference to which the following cells will be   
"matched". Here, "matched" means that the cells are  
similar; note that similar does not mean matching  
in scale. All face-centered cubic unit cells are  
similar; the size is ignored.
	
For a given lattice, there is an infinite number  
of unit cells that can be chosen. For each of the  
non-reference cells, a search is made among many  
representations to find one that matches closely  
to the reference cell.
	
## Input and output:  
Output consists of one line for each input cell.  
The cells are output in the space G6, and each  
line is ended with an angular measure of fit, in  
degrees. Input types

In general, there are 5 types of input lines, see the  
list below. Except for ”END”, they can be combined in any order.

These are case-insensitive. If a particular input is   
invalid, it is rejected with a message. Input type  
must appear in the first column of an input line.  
Blank lines are ignored.

        **g** for G6 vectors
        **s** for S6, Delone/Selling scalars  
        **C3** for C input (without parentheses or commas,  
            “C” would be interpreted as a C-centered unit cell)
        **U** for DC7 unsorted
        **RANDOM**: Random (valid) unit cell generated  
        Crystal lattice input: “A”, “B”, “C”, “P”, “R”, “H”,“F”, “I”  
            followed by three axis lengths and three angles (in degrees)  
        **semicolon**: lines beginning with a semicolon  
            are treated as comments
        **END**: ends the data input section

## Build:
All of LatticeRepLib is written in C++. As of 2023,  
the entire package is compiled in Visual Studio 2022.  
The solution file is LatticeRepLib.sln. Two  
library files are included and required for  
all programs: LatticeRepresentationLib and LRL_Tools.  
	
Compiling in g++ requires at least C++11 level.  
	
The source code for CmdLM is located at:  
   https://github.com/duck10/CmdLM  
The function main is located in the file CmdLM.cpp.  
There are 83 source files (as of 2023/02/07).  
Project files for Visual Studio 2022 are also included. 

The intention is that a release link for CmdLM will  
be created soon (2023/02).

## Input types:

In general, there are 5 types of input lines, see Table 1.  
Except for ”END”, they can be combined in any order.

These are case-insensitive. If a particular input is  
invalid, it is rejected with a message. Input type  
must appear in the first column of and input line.  
Blank lines are ignored.

**g** for G6 vectors

**s** for S6, Delone/Selling scalars

**C3** for C input (without parentheses or commas,  
“C” would be interpreted as a C-centered unit cell)

**U** for DC7 unsorted

**RANDOM** Random (valid) unit cell generated

Crystal lattice input:  
**“A”**, **“B”**, **“C”**, **“P”**, **“R”**, **“H”**, **“F”**, **“I”**  
followed by three axis lengths and three angles (in degrees)

**semicolon**: lines beginning with a semicolon (;) are treated as comments

**END**: ends the data input section


Examples of unit cell inputs

	P 10 20 30 90 111 90  
	G 100 400 900 0 -215.02 0  
	S6 0 -107.51 0 7.51 -400 -792.49 ignored text  
	; this is a comment


## Building CmdLM

The source code for CmdLM is located at:  
 https://github.com/duck10/CmdLM.  
The function main is located in the file CmdLM.cpp.  
There are 83 source files (as of 2023/02/07).  
Project files for Visual Studio 2022 are also  
included. All these source files are required,  
but many might be removed with small adjustments  
in the source code.

## Examples:

Lawton & Jacobson (1965) give the example of two  
primitive unit cells that look quite different,  
but are from similar lattices.

6.490 10.358 10.359 60.520 71.750 71.761  
6.490 10.360 10.360 108.254 108.246 107.223  

The results for the two Lawton and Jacobson unit cells.

C:\Users\lca\Source\Repos\LatticeRepLib\x64\Release>cmdlm  
; Lattice Matching  
; Input  
p 6.490 10.358 10.359 60.520 71.750 71.761  
p 6.490 10.360 10.360 108.254 108.246 107.223  
end  
## output:  
P    6.490  10.358  10.359  60.520  71.750  71.761 ( 0  degrees)   REFERENCE  
P    6.49000  10.36082  10.36000  60.08752  72.77700  71.74024 ( 1.23473  degrees)  

Repeating, but reversing the two input.

C:\Users\lca\Source\Repos\LatticeRepLib\x64\Release>cmdlm  
; Lattice Matching  
; Input  
p 6.490 10.360 10.360 108.254 108.246 107.223  
p 6.490 10.358 10.359 60.520 71.750 71.761  
end  
## output:  
P    6.490  10.360  10.360 108.254 108.246 107.223 ( 0  degrees) REFERENCE  
P    6.4900 10.358  10.360 107.219 108.25983 108.239 ( 1.91417  degrees)  

