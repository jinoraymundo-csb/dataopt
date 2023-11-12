# Introduction to MongoDB

## I. Database and Collections

MongoDB stores data records as **documents** (specifically BSON documents) which are gathered together in **collections**. A **database** stores one or more collections of documents.

## II. Documents

MongoDB stores data records as BSON documents. BSON is a binary representation of JSON documents, though it contains more data types than JSON. 

BSON
: is a binary serialization format used to store documents and make remote procedure calls in MongoDB.

| Type| Number | Alias |
| --- | --- | --- |
| Double | 1 | "double" |
| String | 2 | "string" |
| Object | 3 | "object" |
| Array | 4 | "array" |
| Binary Data | 5 | "binData" |
| ObjectId | 7 | "objectId" |
| Boolean | 8 | "bool" |
| Date | 9 | "date" |
| Null | 10 | "null" |
| Regular Expression | 11 | "regex" |
| JavaScript | 13 | "javascript" |
| 32-bit integer | 16 | "int" |
| Timestamp | 17 | "timestamp" |
| 64-bit integer | 18 | "long" |
| Decimal28 | 19 | "decimal" |
| Min key | -1 | "minKey" |
| Max key | 127 | "maxKey" |

## III. MongoDB Query API

The Query API comprises of two ways to query data in MongoDB:

1. CRUD operations
2. Aggregation Pipelines

* connect to the `dataopt` database inside the docker container
* use `shift+enter` to enter new lines

### A. Create

```
db.getCollection('nakama').insertOne({
  name: "Tony Tony Chopper",
  role: "Doctor"
});

db.getCollection('nakama').insertMany(
  {
    name: "Nefertari Vivi",
    hometown: "Alabasta"
  },
  {
    name: "Nico Robin",
    role: "Archaeologist"
  },
  {
    name: "Franky",
    role: "Shipwright"
  },
  {
    name: "Brook",
    role: "Musician"
  }
);
```

### B. Read

```
db.getCollection('nakama').find({ name: "Monkey D. Luffy"});
```

### C. Update

```
db.getCollection('nakama').updateOne(
  {
    _id: ObjectId("<get ObjectID from previous query>")
  },
  {
    $set: {
      roles: ["Captain"]
    }
  }
)
```

### D. Delete

```
db.getCollection('nakama').deleteOne({ hometown: "Alabasta" });
```