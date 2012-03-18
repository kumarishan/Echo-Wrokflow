# Echo Workflow Manager

## Workflow design

A workflow here defined as a state machine which has single entry and exit entry points
 
### Stage Designs:

Workflow consists of multiple stages. Each stage performs certain actions and then 
handover the task with or without a result to the next stage. There are two types of default stages
in a workflow : Start Stage and the End Stage. The parallel threads of the workflow always ends in 
the End Stage. 
             
And example stage...

             /--------> [Stage 1.1] ---- > [Stage 1.2]----------\
[Start Stage] ---------- > [Stage 2.1] ----- > [Stage 2.2]---- >[End Stage]


While constructing each stage is provided the parent stage and the next stage in the workflow

- Workflow will contain four types of stages apart form default End and Start stage
    - Simple Stage
      ----> [Stage] ---- > 
	
	- Threaded Stage
	               /-----> [Thread1] ---\
	  -----> [Stage] ---> [Thread 2] ---> [Aggregator] --- >
	  
	- Remote Service Stage
	  -----> [Stage] ----> [Remote Service Accessor] ---->
	
	- Encapsulated Workflow Stage
	                                                   /--------> [Stage 1.1] ---- > [Stage 1.2]----------\
      ------> [Stage] ---> [Workflow] ---> [Start Stage] ---------- > [Stage 2.1] ----- > [Stage 2.2]---- >[End Stage] ---> [Workflow Manager] ----->
	  
- Whenever a stage is given the pointer to the End stage then it keeps in itself the track of all the stages from where it will end to this stage.


