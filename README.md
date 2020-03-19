# cpsc479_project1
Project 1: Leaders Election

## Group members:
Liem Tran
liem005@csu.fullerton.edu

# How to run the program


# Problem Description
- In this project you will design and implement one algorithm related to leader election on a ring topology.
## Brief description of the project: Variant of Leader Election on a Ring Topology
## Design and implement one algorithm related to leader election on a ring topology.
### 1. Let N be the size of the distributed system, i.e. run your program with N identical copies.
# Pseudocode
- a) The value of N must be greater than 5.
- b) Choose the value of N to be between 6 and 20.
- c) Each run of a program must terminate within 60 minutes if N=10.
### 2. The even-odd-counting problem on a ring
- a) the process of rank k (k>0) receives the message from the process of rank (k-1) modulo n and 
- b) the process of rank k (k 0) sends a message to the process of rank (k+1) modulo n.
- c) Each process generates a single random integer value and does some computations on it before sending it:
   - i) The value needs to be positive, so if the value is negative, then take the absolute value of it. 
   - ii) The value needs to be greater than 10 and less than 100, so if the value is less than 10, then add 10 to it.
   - iii) If the value is greater than 100, then take modulo 100. 
   - iv) For example, if the process of rank 0 generates the random value 15, then the new value is 1150 (1 concatenated with 15                  concatenated with 0). Another example: if process of rank 2 generates the random value of 78 then the new value is 1782 (1              concatenated with 78 concatenated with 2).
### 3. Leader Election Problem in a Ring
- a) Our algorithm selects two leaders, which we can call them as the president and the vice-president. The president will be the            smallest odd value and the vice president will be the smallest even value.
- b) The value received finally at process 0 after it traverses the entire ring will be the smallest generated value in the ring              and will be declared by process 0 as the leader.
### 4. Our Leader Election Problem in a Ring (to be implemented)
- a) Concurrent two leader election algorithm
- b) Sequential two leader election algorithm
   - i) Election of the odd leader:
      1) If process 0 has an odd computer value, it sends it to process 1; if process 0 has an even computed value then it                        sends the value of 19990 to process 1 and does the same comparision for others processes.
      2) The smallest value received at process 0 is declared as the odd leader.
   - ii) Election of the even leader:
      1) If process 0 has an even computer value, it sends it to process 1; if process 0 has an odd computed value then it                        sends the value of 19990 to process 1 and does the same comparision for others processes.
      2) The smallest value received at process 0 is declared as the even leader.
## Two snapshots of code executing for some two distinct values of N.     




