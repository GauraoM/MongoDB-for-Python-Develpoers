### Aggregation

1.Aggregation is a pipeline:

Pipelines are composed stages, broad unit of work.
Within stages,expressions are used to specify individual units of work

2.Expressions are functions

{"$add":["$a", "$b"]}

### writeConcern{w:1}
Only requests an acknowledgement that one node applied the write.
This is the default writeConcern in MongoDB.

### writeConcern{w:'majority'}
Request acknowledgement that a majority of nodes in the replica set applied the write.
slower but durable than w:1.
Useful for ensuring vital writes are majority-committed.

### writeConcern{w:0}
Does not ensure that a write was committed by any node. Very fast but less durable.

### $lookup
Expressive lookup allows us to apply aggregation pipelines to data-before the data is joined.
Let allows us to declare variables in our pipeline, referring th document field in our source collection.
Compass' Export-to-Language feature produces aggregations in our applications native language.

### DeleteOne and DeleteMany

delete_one is a lot like find_one. It takes a predicate to match the document you want to delete, finds the document, and deletes it. If multiple documents match the predicate, delete_one will only delete the first document matched.

Unlike delete_one, delete_many deletes all documents that match the supplied predicate. Because of this behavior, delete_many is a little more "dangerous".

The number of documents deleted can be accessed via the "deleted_count" property on the DeleteResult object returned from a delete operation.

### Questions

1.Which of the following aggregation stages have equivalent cursor methods?

Ans: $limit, $sort. $skip

2.Which of the following is true about InsertOneResult?

Ans:

It contains the _id of an inserted document.
It can tell us whether the operation was acknowledged by the server.

3.Which of the following Write Concerns are valid in a 3-node replica set?

Ans:  w:0, w:1, w:majority

4.Which of the following write concerns are more durable than the default?

Ans: w:2, w:majority

5.Which of the following are valid update operators in Pymongo?

Ans: $inc, $set, $push

6.Why did we use a let expression with expressive $lookup, when joining the comments and the movies collection?

Ans:
To use fields from the movies documents in the pipeline.

7.Which of the following is true about deleting documents in Pymongo?

Ans:

delete_many() can delete any number of documents.
DeleteResult objects contain the number of deleted documents(by acknowledgement).
delete_one() can only delete one document.

8.Paging Ticket?

Ans: 5a9824d057adff467fb1f526

9.Faceted search Ticket?

Ans: 5aa7d3948adcc3fb770f06fb

10. User Management Ticket?

Ans: 5a8d8ee2f9588ca2701894be

11. User Preference Ticket?

Ans: 5aabe31503ac76bc4f73e267

12. Get Comments Ticket?

Ans: 5ab5094fb526e43b570e4633

13. Create/ update comments Ticket?

Ans: 5aba8d5113910c25d7058f8f

14. Delete Comments Ticket?

Ans: 5ac25c280a80ed6e67e1cecb

