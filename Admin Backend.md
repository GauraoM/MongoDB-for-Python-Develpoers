### Read Concerns
The default read concern in MongoDB is "local". This does not check that data has been replicated.
The read concern "majority" allows for more durable reads. This only returns data that has been replicated to a majority of nodes.

### Ordered Bulk write
The default setting for bulk writes in MongoDB. Executes writes sequentially, will end execution after first write failure.

### Unordered Bulk Write
Has to be specified with the flag:{ordered: false}. Executes writes in parallel.

### Questions
1.Which of the following Read Concerns are valid in a 3-node replica set?

Ans: local , majority

2.Which of the following is true about bulk writes?

Ans:
By default, bulk writes are ordered.
Bulk writes decrease the effect of latency on overall operation time.

3. User report Ticket?

Ans: 5accad3272455e5db79e4dad

4. Migration Ticket?

Ans: 5ad9f6a64fec134d116fb06f
