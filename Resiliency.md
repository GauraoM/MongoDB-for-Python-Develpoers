### Connection Pooling
Connection pool allows for reuse of connections.
Subsequent requests appear faster to the client.
Default size of 100.

### Robust Client Configuration
Always use connection pooling.
Always specify a wtimeout with majority writes.
Always handle serverSelectionTimeout errors.

### Change Stream


### Questions

1.Which of the following are benefits of connection pooling?

Ans:
A large influx of operations can be handled more quickly with a pool of existing connections.
New operations can be serviced with pre-existing connections, so a new connection doesn't have to be created each time.

2.When should you set a wtimeout?

Ans:
When our application is using a Write Concern more durable than w: 1.

3.What of the following is true about Change Streams in Pymongo?

Ans:
They can be used to log changes to a MongoDB collection.
They output cursors, which contain change event documents.
They accept pipelines, which can be used to filter output from the change stream.

4. Connection Pooling Ticket?

Ans: 5ad4f4f58d4b377bcf55d742

5. Timeouts Ticket?

Ans: 5addf035498efdeb55e90b01

6. Handling errors Ticket?

Ans: 5ae9b76a703c7c603202ef22

