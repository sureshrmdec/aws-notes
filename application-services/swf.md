### SWF - Simple Workflow Service 

- allows for the coordination of work across different application components
- tasks included web service calls, executable code, human interaction
- retention period of work in the queue: 1 year for workflow executions 
- uses task-orientated API instead of message orientated (SQS)
- ensures that a task is only executed once and never duplicated
- SWF keeps track of all tasks and events in an application

Actors:
- Workflow starters: application that can initiate a work flow (e.g. a e-commerce app placing an order)
- Deciders: controls the flow of activity in workflow execution 
- Activity workers: carries out the activities of the workflow