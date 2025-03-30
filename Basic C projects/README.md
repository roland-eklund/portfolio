# Basic C Projects

### dining_philosophers.c  
This is my implementation of the commonly known challenge where you have 5 mutexes and 5 threads.
Every thread need to lock two specific mutexes before being able to continue.
Traditionally you would print the states of the philosophers, not here.  
  
I just simulate work with a usleep() and collect some data from the threads.
Data for each thread is collected in a struct, which in turn is monitored by a separate monitor thread.  
  
With this "program" I'm able to run 1000 threads while monitoring shared resources.  
By adding structs and a monitor thread the difficulty of the standard challenge increased with me not just having to account for deadlocks but also race conditions.  

The program initally sets a few parameters that easily can be changed:
```c
 #define NUM_PHILOSOPHERS 1000 // Sets the number of threads you want to run
 #define ROUNDS 800            // Each thread runs for N rounds
 #define MONITOR_INTERVAL 40   // Set the interval for the monitor thread (in microseconds)
 #define TIME_UNTIL_DEAD 1000  // Set the time a thread is allowed to be starved in (microseconds)
 #define SIMULATE_WORK 1       // 1 or 0, If this is set to true, every thread will simulate work for a random amount of time.
```

### Project takeaways
With this project I got a initial understanding of multithreading, mutexes and deadlock.  
Without having a particular interest in the subject I found it really interesting to get a hang of the basics.
It was a fun challenge to get the program to work and I learned a lot about how threads work in C.
I also learned a lot about how to use thread sanitizer to debug my code.


### Possible improvements

 - Add a command line argument to set the parameters
 - Add the possibility to run multiple rounds with different parameters with summary of each round
 - Split the code into multiple files
 - Add a makefile

### How to run
Just run the following in a terminal:
```bash
clang -pthread dining_philosophers.c -o dining_philosophers
./dining_philosophers
```
To run the program with thread sanitizer, use the following command:
```bash
clang -fsanitize=thread -pthread dining_philosophers.c -o dining_philosophers
./dining_philosophers
```
