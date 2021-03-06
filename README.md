# cpsc479_project1
Project 1: Leaders Election

## Group members:
Liem Tran
liem005@csu.fullerton.edu

# How to run the program
### Algorithm in C using MPI commands to solve the problem.
## Compile the code 
- ``` mpicc ringLeader.c ```
## Execute the code
Run the executable number of processors of 12 with the following command:
- ``` mpirun -n 12 ./a.out ```
- Replace 12 with the number of processors you wish to test.
- Noted run with 10 procoessors will terminated the program.

# Problem Description
- In this project you will design and implement one algorithm related to leader election on a ring topology.
## Brief description of the project: Variant of Leader Election on a Ring Topology
# Pseudocode
### 1. Let N be the size of the distributed system, i.e. run your program with N identical copies.
- a) The value of N must be greater than 5.
- b) Choose the value of N to be between 6 and 20.
- c) Each run of a program must terminate within 60 minutes if N=10.

  if (size == 10) {
       exit(1);
  } else if (size >= 6 || size <= 20) {
      even_odd_election(rank, size);
  } else {
      printf("Choose the value of N or Number of processes to be between 6 and 20");
  }
  
### 2. The even-odd-counting problem on a ring
- a) the process of rank k (k>0) receives the message from the process of rank (k-1) modulo n and 
- b) the process of rank k (k 0) sends a message to the process of rank (k+1) modulo n.
- c) Each process generates a single random integer value and does some computations on it before sending it:
   - i) The value needs to be positive, so if the value is negative, then take the absolute value of it. 
   - ii) The value needs to be greater than 10 and less than 100, so if the value is less than 10, then add 10 to it.
   - iii) If the value is greater than 100, then take modulo 100. 
   - iv) For example, if the process of rank 0 generates the random value 15, then the new value is 1150 (1 concatenated with 15                  concatenated with 0). Another example: if process of rank 2 generates the random value of 78 then the new value is 1782 (1              concatenated with 78 concatenated with 2).
   
   if (random < 0)
      random = abs(random);

  if (random <= 10)
      random = random + 10;

  if (random > 100)
    random = random % 100;
    printf("\nProcess of rank 0 generates the random value %d\n",random);
    random = (100 + random) * 10;
  
  return random;
  
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
      
      if(random % 2 == 0) {
            even_odd_Election[0] = random; 
            even_odd_Election[2] = 19999;
	    frandom = frandom;
    	    printf("#########################################################################\n");
	    printf("---------------------Election of the even leader-------------------------\n");
            printf("#########################################################################\n");
        }
        // If random is odd append 19990
        else {
            even_odd_Election[0] = 19990; 
            even_odd_Election[2] = random;
	    printf("#########################################################################\n");
            printf("---------------------Election of the odd leader-------------------------\n");
	    printf("#########################################################################\n");
            
        }
        // Process of rank 0 sends values to rank 1 
        printf("Process of rank %d  generates the random value %d sends: %d, %d\n", rank, frandom, even_odd_Election[0], even_odd_Election[2]);
	MPI_Send(even_odd_Election, 4, MPI_INT, rank + 1, 0, MPI_COMM_WORLD);

        // Indicated the President and Vice-president
        MPI_Recv(even_odd_Election, 4, MPI_INT, size - 1, 0, MPI_COMM_WORLD, MPI_STATUS_IGNORE);
        printf("#########################################################################\n");
	printf("The President: rank %d with the smallest odd value: %d\nThe Vice-president: rank %d with the smallest even value: %d\n",
            even_odd_Election[1], even_odd_Election[2], even_odd_Election[3], even_odd_Election[0]);
    }
    
## Screenshots
### Full Screen
![alt text](https://github.com/liem005/liem1/blob/master/screen.PNG)
## Two snapshots of code executing for some two distinct values of N.     
### 8 processors
![alt text](https://github.com/liem005/liem1/blob/master/n8.PNG)
### 20 processors
![alt text](https://github.com/liem005/liem1/blob/master/n20.PNG)
### 10 processors
![alt text](https://github.com/liem005/liem1/blob/master/n10.PNG)



