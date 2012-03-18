# Echo Workflow Manager

## Workflow design

A workflow here defined as a state machine which has single entry and exit entry points
 
### Stage Designs:

Workflow consists of multiple stages. Each stage performs certain actions and then 
handover the task with or without a result to the next stage. There are two types of default stages
in a workflow : Start Stage and the End Stage. The parallel threads of the workflow always ends in 
the End Stage. 
             
And example stage...
<pre>
             /--------> [Stage 1.1] ---- > [Stage 1.2]----------\  
[Start Stage] ---------- > [Stage 2.1] ----- > [Stage 2.2]---- >[End Stage]

</pre>

While constructing each stage is provided the parent stage and the next stage in the workflow

- Workflow will contain four types of stages apart form default End and Start stage
    - Simple Stage  
      <pre> ----> [Stage] ---- >  </pre>
	
	- Threaded Stage  
          <pre>
	                 /-----> [Thread1] ---\
	  -----> [Stage] ---> [Thread 2] ---> [Aggregator] --- >
	  </pre>

	- Remote Service Stage  
          <pre>
          -----> [Stage] ----> [Remote Service Accessor] ---->
	  </pre>

	- Encapsulated Workflow Stage  
          <pre>
	                                                             /--------> [Stage 1.1] ---- > [Stage 1.2]----------\
          ------> [Stage] ---> [Workflow Manager] ---> [Start Stage] ---------- > [Stage 2.1] ----- > [Stage 2.2]---- >[End Stage] ---> [Workflow Manager] ----->
	  </pre>

- Whenever a stage is given the pointer to the End stage then it keeps in itself the track of all the stages from where it will end to this stage.


