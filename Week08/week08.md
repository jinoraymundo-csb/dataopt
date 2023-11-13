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

---

## IV. Filter Documents

### A. Select All Documents

To select all documents in the collection, pass an empty document as the query filter parameter to the find method. The query filter parameter determines the select criteria:

```
db.inventory.find();
```

### B. Specify Equality Condition

To specify equality conditions, use `<field>:<value>` expressions in the query filter document:

```
{ <field1>: <value1>, ... }
```

for example:

```
db.inventory.find( { status: "D" } )
```

This operation uses a filter predicate of `{ status: "D" }`, which corresponds to the following SQL statement:

```
SELECT * FROM inventory WHERE status = "D"
```

### C. Specify Conditions using Query Operators

A query filter document can use the query operators to specify conditions in the following form:

```
{ <field1>: { <operator1>: <value1> }, ... }
```

for example:

```
db.inventory.find( { status: { $in: [ "A", "D" ] } } )
```

The operation uses a **filter predicate** of `{ status: { $in: [ "A", "D" ] } }`, which corresponds to the following SQL statement:

```
SELECT * FROM inventory WHERE status in ("A", "D")
```

### D. Specify `AND` Conditions

A compound query can specify conditions for more than one field in the collection's documents. Implicitly, a logical AND conjunction connects the clauses of a compound query so that the query selects the documents in the collection that match all the conditions.

```
db.inventory.find( { status: "A", qty: { $lt: 30 } } )
```

The operation uses a filter predicate of `{ status: "A", qty: { $lt: 30 } }`, which corresponds to the following SQL statement:

```
SELECT * FROM inventory WHERE status = "A" AND qty < 30
```

### E. Specify `OR` Conditions

Using the `$or` operator, you can specify a compound query that joins each clause with a logical OR conjunction so that the query selects the documents in the collection that match at least one condition.

```
db.inventory.find( { $or: [ { status: "A" }, { qty: { $lt: 30 } } ] } )
```

The operation uses a filter predicate of `{ $or: [ { status: 'A' }, { qty: { $lt: 30 } } ] }`, which corresponds to the following SQL statement:

```
SELECT * FROM inventory WHERE status = "A" OR qty < 30
```

### F. Specify `AND` as well as `OR` Conditions

```
db.inventory.find( {
     status: "A",
     $or: [ { qty: { $lt: 30 } }, { item: /^p/ } ]
} )
```

The operation uses a filter predicate of:

```
{
   status: 'A',
   $or: [
     { qty: { $lt: 30 } }, { item: { $regex: '^p' } }
   ]
}
```

which corresponds to the following SQL statement:

```
SELECT * FROM inventory WHERE status = "A" AND ( qty < 30 OR item LIKE "p%")
```

---

## APPENDIX

### Query Selectors

#### Comparison

| Name | Description |
| --- | --- |
| `$eq` | Matches values that are equal to a specified value. |
| `$gt` | Matches values that are greater than a specified value. |
| `$gte` | Matches values that are greater than or equal to a specified value. |
| `$in` | Matches any of the values specified in an array. |
| `$lt` | Matches values that are less than a specified value. |
| `$lte` | Matches values that are less than or equal to a specified value. |
| `$ne` | Matches all values that are not equal to a specified value. |
| `$nin` | Matches none of the values specified in an array. |

#### Logical

| Name | Description |
| --- | --- |
| `$and` | Joins query clauses with a logical AND returns all documents that match the conditions of both clauses. |
| `$not` | Inverts the effect of a query expression and returns documents that do not match the query expression. |
| `$nor` | Joins query clauses with a logical NOR returns all documents that fail to match both clauses. |
| `$or` | Joins query clauses with a logical OR returns all documents that match the conditions of either clause. |

#### Element

| Name | Description |
| --- | --- |
| `$exists` | Matches documents that have the specified field. |
| `$type` | Selects documents if a field is of the specified type. |

#### Evaluation
| Name | Description |
| --- | --- |
| `$expr` | Allows use of aggregation expressions within the query language. |
| `$jsonSchema` | Validate documents against the given JSON Schema. |
| `$mod` | Performs a modulo operation on the value of a field and selects documents with a specified result. |
| `$regex` | Selects documents where values match a specified regular expression. |
| `$text` | Performs text search. |
| `$where` | Matches documents that satisfy a JavaScript expression. |

#### Geospatial

| Name | Description |
| --- | --- |
| `$geoIntersects` | Selects geometries that intersect with a GeoJSON geometry. The 2dsphere index supports $geoIntersects. |
| `$geoWithin` | Selects geometries within a bounding GeoJSON geometry. The 2dsphere and 2d indexes support $geoWithin. |
| `$near` | Returns geospatial objects in proximity to a point. Requires a geospatial index. The 2dsphere and 2d indexes support $near. |
| `$nearSphere` | Returns geospatial objects in proximity to a point on a sphere. Requires a geospatial index. The 2dsphere and 2d indexes support $nearSphere. |

#### Array

| Name | Description |
| --- | --- |
| `$all` | Matches arrays that contain all elements specified in the query. |
| `$elemMatch` | Selects documents if element in the array field matches all the specified $elemMatch conditions. |
| `$size` | Selects documents if the array field is a specified size. |

#### Bitwise

| Name | Description |
| --- | --- |
| `$bitsAllClear` | Matches numeric or binary values in which a set of bit positions all have a value of 0. |
| `$bitsAllSet` | Matches numeric or binary values in which a set of bit positions all have a value of 1. |
| `$bitsAnyClear` | Matches numeric or binary values in which any bit from a set of bit positions has a value of 0. |
| `$bitsAnySet` | Matches numeric or binary values in which any bit from a set of bit positions has a value of 1. |

### Projection Operators

| Name | Description |
| --- | --- |
| `$` | Projects the first element in an array that matches the query condition. |
| `$elemMatch` | Projects the first element in an array that matches the specified $elemMatch condition. |
| `$meta` | Projects the document's score assigned during $text operation. |
| `$slice` | Limits the number of elements projected from an array. Supports skip and limit slices. |

### Miscellaneous Operators

| Name | Description |
| --- | --- |
| `$comment` | Adds a comment to a query predicate. |
| `$rand` | Generates a random float between 0 and 1. |
