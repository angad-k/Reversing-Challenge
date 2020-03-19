# Reversing-Challenge

So, we have this executable named glowwine. <br>
Running it without any argument returns the following : <br>
` usage: ./glowwine <key>` <br>
Running it with any random key, say 'aaaaa', returns: <br>
` wrong key, try again :/ ` <br>
Now, to investigate further, I opened it with gdb. Disassembling the main gives us : <br>
![Screen-shot](https://github.com/angad-k/Reversing-Challenge/blob/master/Screenshot%20from%202020-03-19%2021-39-08.png) <br>
So,from this disassembled code, I deduced the basic control flow as shown below.
(Note : The flowchart also contains elements which are results of deductions that I'll explain later.)<br>
![flow-chart](https://github.com/angad-k/Reversing-Challenge/blob/master/New%20Doc%202020-03-19%2021.21.41(2).jpg) <br>
A little about the flowchart : <br>
- Every jump statement is where I end that block and start a new one. <br>
- Blocks marked A0, A1, A2 and A3 are the blocks where the given key is checked for various conditions. <br>
- Other blocks which are not labelled basically print something to the screen. <br>
Now, lets start with **A0**. It has a JG jump at the end which is a jump that will take place if the sign flag and zero flag both are not set. The compare statement before it compares the value of whatever's stored at [rbp - 0x4] with 0x1. All of this and the fact that running the executable without any argument gave us the usage instructions point to the fact this check must be for whether an argument is given or not. Sure enough, if we set the breakpoint at the start of main by `break *main` and then run the program, it doesn't jump and goes into the next block thus printing the usage instructions. So, we are now pretty sure about A0's work.<br>
**A0 checks for whether we have given an argument or not.**<br>
Let's move on to A1 now. A quick glance at it reveals to us that there's a call to some <strlen@plt> procedure. strlen must be returning us with length of some string. And which string are we focusing on in this program? No brownie points for guessing, THE KEY'S LENGTH!!! So, yeah. We might me checking the length of the string here. Also, the comparison with 0x5 in the next line points to the thought that key's length must be 5. And sure enough, running the code with the key "aaaaa" allows us to jump to the next block while using 'a' leads to us moving into a type of block that calls a procedure called "sorrybro". What does sorrybro do, you ask? A quick disassembly of the sorrybro function yields : <br> 






