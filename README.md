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

 






