Ex: client = MongoClient(uri, connectTimeoutMS=200, retryWrites=True)

Setting connectTimeoutMS=200ms, how the driver will allow attempt to  connect before erroring and setting retryWrites to True, signaling to the driver to retry a write in the event of a network error.
After instantiating the client, database handles can be created via property or dictionary accessors on the client object.
Collections handles are referenced from the database object.
Collection specific operations like querying or updating documents are performed on the collection object.


### Qusetions

1.During this course, which of the following files in mflix will you have to edit?

Ans: 
db.py

2.Implement the get_movies_by_country method in db.py to search movies by country and use projection to return the title and _id field. The _id field will be returned by default.

Ans:
5a94762f949291c47fa6474d

3.For this ticket, you will need to modify the method build_query_sort_project in db.py to allow the following movie search criteria:

genres: finds movies that include any of the wanted genres.
Already, the build_query_sort_project method is able to return results for two different types of movie search criteria:

text: performs a text search in the movies collection
cast: finds movies that include any of the wanted cast
You just need to construct the query that queries the movies collection by the genres field.

Ans:
5a96a6a29c453a40d04922cc