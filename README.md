# Distributed-Key-Value-Database

## High Level Approach

We designed our program level by level. After we thoroughly read the raft paper many times and the project spec, we implemented the algorithm by building methods of three main components: the follower, the candidate, and the leader. We first finish the put, followed by the heartbeat and so on. 

When designing the replica class, we added lots of additional field to store all the inforamtion required for the algorithm to perform correctly. For example, we added a list of dictionaries to store all the values and the keys when receiving messages (aka the log). After the leader stored all the information in its own field, it will broadcast to other relicas in the whole system. The followers will then commit this log.   

When followers receive requests from the client, instead of directly responding to the requests, the followers will redirect them to the cluster leader. 

The leaders will send heartbeat to other followers and the followers will have a time counter inside it. When a replica doesn't receive a heartbeat from the leader, it will soon timeout and start the election process, selecting a new leader and keep moving forward. 

The election process stricly complies with the procedures described in the raft paper in order to make sure the correctness of the leader elected. 


## Challenge Faced

Our most challenge faced during the process of finishing the project including two part: 

The first part is to read and understand how raft is working. Although the raft paper is relatively easy to read compare to other materials, it still take some time for us to read and fully understand the principle of all the parts of the raft. What's more, after we finish reading the paper, we also have to convert what we learned from the paper into code. This process is also very hard as understanding the paper doesn't mean that we can correctly implementing the program. We also referred to other sources such as the raft slides from UIUC.    

So thats the second challenge we faced here: We meet lots of problems when we implementing the raft. The majority of them are two: how to convert a part of the principle into the code and debugging that implementation. During the process, we find lots of bugs in our program which we spent lots of time to find out the problem. Debugging is particularly challenging as we cannot use the stepper. We had to pipe the result from STDOUT into a file to debug. Looking at the output of the simulator is also tedious.   

## Things that We Think is Good

1. builder pattern for constructing message and log
2. command pattern for the run method
3. all the functionalities is clearly divided in different methods
4. helpers to make the program readable and clear
5. highly abstract code to make the program looks clean and no redundant things
6. Modulized constants
7. Clear comments  

## Methods of Testing Program

We use the running configuration provided in the github to make sure our program has the functionality. 
Also, we print out some of the data in order to check what our program get is correct. We piped the output from STDOUT into a local test txt file to better observe what was going on.

