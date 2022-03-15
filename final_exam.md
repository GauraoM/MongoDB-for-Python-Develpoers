{
  "year" : 1828,
  "winner" : "Andrew Jackson",
  "winner_running_mate" : "John C. Calhoun",
  "winner_party" : "Democratic",
  "winner_electoral_votes" : 178,
  "total_electoral_votes" : 261
}

1.Which of the following queries will retrieve all the Republican winners with at least 160 electoral votes?

Ans:
db.elections.find( { "winner_party": "Republican",
                     "winner_electoral_votes": { "$gte": 160 } } )

2.There is an update required for phones with software_version earlier than 4.0. Anyone still using a version older than 4.0 will be asked to update.

{
  "model": 5,
  "date_issued" : ISODate("2016-07-27T20:27:52.834Z"),
  "software_version": 4.8,
  "needs_to_update": false
}

Ans:

db.phones.update_many( { "software_version": { "$lt": 4.0 } },
                       { "$set": { "needs_to_update": True } } )

3.Please find the documentation on Connection String URI Format here. The variable representing our client, mongo_client, will:

from pymongo import MongoClient
uri = "mongodb+srv://m220-user:m220-pass@m220-test.mongodb.net/test"

mongo_client = MongoClient(
  uri,
  connectTimeoutMS=50,
  retryWrites=True,
  authSource="admin"
)  

Ans:

automatically retry writes that fail.
wait at most 50 milliseconds for timing out a connection.

4.Suppose a client application is sending writes to a replica set with 3 nodes:Before returning an acknowledgement back to the client, the replica set waits.When the write has been applied by the nodes marked in stripes, it returns an acknowledgement back to the client.What Write Concern was used in this operation?

Ans: w: majority

5.Which of the insert operations in requests will succeed?

requests = [
  InsertOne({ '_id': 11, 'name': 'Edgar Martinez', 'salary': "8.5M" }),    # Insert #1
  InsertOne({ '_id': 3, 'name': 'Alex Rodriguez', 'salary': "18.3M" }),    # Insert #2
  InsertOne({ '_id': 24, 'name': 'Ken Griffey Jr.', 'salary': "12.4M" }),  # Insert #3
  InsertOne({ '_id': 11, 'name': 'David Bell', 'salary': "2.5M" }),        # Insert #4
  InsertOne({ '_id': 19, 'name': 'Jay Buhner', 'salary': "5.1M" })         # Insert #5
]

response = employees.bulk_write(requests)

Ans: Insert #1, Insert #2, Insert #3

4.Suppose a client application is sending writes to a replica set with three nodes, but the primary node stops responding.Assume that none of the connection settings have been changed, and that the client is only sending insert statements with write concern w: 1 to the server.
After 30 seconds, the client still cannot connect to a new primary. Which of the following exceptions will be raised by Pymongo?

Ans:

ServerSelectionTimeoutError

5.Which of the following queries will find only the 4th- and 5th-tallest people in the people_heights collection?

{
  "name": "Ada",
  "height": 1.7
}

Ans:
    db.people_heights.find().sort("height", -1).skip(3).limit(2)