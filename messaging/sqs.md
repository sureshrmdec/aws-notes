### SQS 

- web service that gives access used to store messages in a queue for processing by a computer
- allows for distributed processing by applications that generate and consume messages
- decouples components of an application so they can run independently
- SQS is a fail-safe queue 
- messages can contain up to 256Kb of text in any format
- Components of the application can retrieve the SQS messages via the SQS API
- acts as a buffer between producers, computation and saving of data
- SQS is a pull based system
- SQS guarantees that a message will be processed at least once; but may be processed more than once
- long polling: only poll queue when there is a message or when the long poll times out (saves on costs); short polling polls queue even if it is empty
- messages can be kept in a queue from 1 minute up to 14 days (default is 4 days)
- Visibility Time Out: is the time the message is invisible in the SQS queue after the reader pulls the message; if the job is not processed within the Visibility Time the job will become visible again for other processes to get the message
    + visibility time out maximum is 12 hours

Two queue types:
1. standard queue:
- unlimited number of transactions per second; 
- guarantee that a message is delivered at least once
- best effort ordering, some messages might come out before earlier received messages
2. fifo queue: 
- the same as standard queues, but guarantee first in, first out ordering
- limited to 300 transactions per second