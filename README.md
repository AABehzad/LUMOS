Computer Organization _ Final Project
==============================================================
### Project Title = design an 8-bit multiplier 
- Name: AmirAliBehzadi
- Date:1403/11/05

## Project introduction

 - In this project, an 8-bit multiplier module is to be designed on the "LUMOS" processor and ultimately simulated according to the specified TEST_BENCHS.

First ,  download the project from GitHub and according to the description , in the file "Fixed_Point_Unit.v" and on line '241', we find the "module Multiplier". Note that the inputs and outputs are already specified and we only need to design the multiplier circuit in the next section of the module. We need to multiply the input 'operand_1' by the input 'operand_2' and put it in the output 'product'.

       module Multiplier
    (
        input wire [7 : 0] operand_1,
        input wire [7 : 0] operand_2,
    
        output reg [15 : 0] product
    );
    
        always @(*)
        begin
            product <= operand_1 * operand_2;
        end
    endmodule

## Multiplication Module:
As mentioned in the project description, there are different ways to do this. Next, we will use the method of an adder, and the Shift-Register .

First, we define an integer variable because it is necessary to determine which step of the loop we are in and which bit we should multiply by ‘operand_1’. 

Now, to specify that whenever the inputs change, the output also changes, we use the ‘always’ block and the ‘*’ symbol. (We also know that we use ‘begin’ and ‘end’ at the beginning and end of each block to start and end it.) Next, before creating the loop, we set the ‘product’ register, which is the output of the module, to ‘16'b0’, which is the 16-bit zero descriptor . The reason for this is that if the inputs change, the result of the previous multiplication operation in the ‘product’ register should not affect this new sum.

 Now we define a loop that is executed 8 times and each time adds one to the variable ‘i’. The reason for this is that this operation should be performed for every 8 bits of ‘operand_2’. Now in this loop, using a condition, we check whether the bit of ‘operand_2’ pointed to by the loop counter or ‘i’ is 0 or 1 (we know that each bit can only have two states 0 or 1). If this bit was zero, it has no effect on the result of the multiplication (0 multiplied by anything is 0) but if it was 1, we should add the value of ‘operand_1’ to the ‘product’ register. 
 The point in this addition is that depending on the position of the bit being multiplied from ‘operand_2’ which was specified by the counter ‘i’, the value of the digits being added from ‘operand_1’ with the ‘product’ register changes. To do this, we shift the bits of ‘operand_1’ to the left by the amount of the counter ‘i’. To do this, we use the ‘<<’ operator. Finally, we add this value with the current value of the ‘product’ register and put it in the new value of the ‘product’ register. 
 
 Finally, this loop checks all 8 bits and the result of the multiplication puts in the ‘product’ register.


???????????????

How the multiplier works for a typical example :   

????????????

Now we enter the simulation commands in the console:

???????????????

It can be seen that we do not receive any warning from the executor and the multiplier output is correct for all input values, because according to the code written in the ‘LUMOS_Testbench.v’ file, if the result is wrong, we receive a warning.

???????????????

Now we execute the simulation command:

<img src="https://github.com/AABehzad/LUMOS/blob/main/Images/p2.png" alt="Image"  style="vertical-align:middle">

It can be seen in the figure that, as stated in the project description, the f0 register has taken the value 1126.295.

