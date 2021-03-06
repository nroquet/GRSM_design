MATLAB (MathWorks) based software for automated design of GRSM registers for user-specified, two-input gene regulation programs.


reference paper: N. Roquet et al., Synthetic recombinase-based state machines in living cells. Science. 353, aad8559 (2016).

Please cite the reference paper when using this repository for your research. 


Contents of this repository:
LICENSE- MIT License.
README.txt- instructional file.
grsmDB.mat- GRSM database create with MATLAB R2013b. For a detailed explanation of the contents of this file and how it was created please consult the reference paper (above). 
searchGRSM.m- Function written in MATLAB 2013b that accepts a user-specified gene regulation program and searches for its corresponding GRSM registers in grsmDB.mat.
registerRank.m- Function written in MATLAB 2013b that is called upon by searchGRSM.m


Instructions on how to use this repository to search for GRSM registers:
1.	Copy the contents of this repository to any directory on your computer.
2.	Open MATLAB and navigate the working directory to the directory of the repository (from step 1). 
3.	Type output = searchGRSM(input) into the MATLAB command line, where output is the variable to which the output registers will be stored, and input is your desired gene regulation program (as specified below).


Instructions on creating the input:
Specify your input (gene regulation program) as a 5xM matrix. Each row (row 1 to row 5) represents a state S1 to S5 (respectively) corresponding to Fig. 3A of the reference paper. Each column represents a distinct gene. You can specify anywhere up to M = 14 genes. Each element of the matrix should be a "0" or "1" corresponding to whether or not you want that gene to be expressed (1) or not expressed (0) in that state.


Interpreting the output: 
The output is a Nx7 matrix. Each row of the matrix represents a register that can be used to implement the input gene regulation program. Columns (column 1 to column 7) of a register represent DNA regions, “r1” to “r7” (respectively), separated by recognition sites on the register template corresponding to Fig. 5 from the reference paper. 

Each element of the matrix specifies a part for that register (row) in that DNA region (column). Parts are numbers "1" through "25" (with some also appearing as negative) as defined in Table S9 of the reference paper. A more in depth explanation of the parts can be found in the Materials and Methods section and supplementary Text S6 of the reference paper.

The output registers are ordered (ranked) with the following 4 steps:
1. rank by the (least to greatest) number of parts necessitating promoter read-through 
2. subrank by the (least to greatest) number of parts necessitating terminator read-through
3. subrank by the (greatest to least) number of empty parts (part “5”)
4. subrank by the (least to greatest) number of promoters


Example:
input = [0 0 0 0 1; 0 0 0 1 0; 0 0 1 0 0; 0 1 0 0 0; 1 0 0 0 0]
output = 
   -1    5    8    2    2    5  -14
   -1    5    5    8   -3   -9    1
   -1    3    5   -9    8    5    1
   -1    9    5   -3    8    5    1
   14    9    5    1    8    5    1
    9    3    5    1    8    5    1
   -1    5    8    1    9    5  -14
   -1    5    8    1   14    5   -9
   -1    5    5    8   -9   -3    1
   -1   -7    8    2   14    5   -9
   14   -1   10   -1  -12    5    1
   -1   -7  -12    2    5    5   -9
   -1    7    5    8   -3   -9   -9
   -1    3    5   -9    8   -7   -9
   -1    9    5   -3    8   -7   -9
    9    3    5   -9    8   -7    1
    9    9    5   -3    8   -7    1
   -1   -7  -12    1    9    5  -14
   -1   -7  -12    1   14    5   -9
   -1    7    5    8   -9   -3   -9
    5   -7   12    5    8   -7   -9
    9   -7    5   -9    8   -7   -9
    9    7    5    8   -9    7   -9

For more examples, Table S8 of the reference paper shows the inputs to and outputs from the search function used to implement the two-input, five-state GRSMs tested in the paper. 
