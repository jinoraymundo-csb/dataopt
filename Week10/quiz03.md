# Quiz 03: Document Filtering in MongoDB

1. Start with `quiz03` directory under `Week10`
2. Download the sample dataset [here](https://raw.githubusercontent.com/IronPTSolutions/mongo-examples/master/datasets/restaurants.json) and save it on `Week10` folder
3. add a `scripts` folder under `Week10` folder
4. name your file as `<lastname>_<firstname>.js` e.g. `raymundo_jinopaulo.js`
5. execute the following docker commands on the terminal:
```
docker run --name dataopt-quiz03 --rm -p 27017:27017 -v ${PWD}/scripts:/scripts -d mongo:latest
docker cp restaurants.json dataopt-quiz03:/tmp/restaurants.json
docker exec -it dataopt-quiz03 bash
mongoimport --db restaurant --jsonArray --file /tmp/restaurants.json
```


## Questions

1. Get all fields from `restaurant` collection where `borough` == "Queens"
2. Get all fields from `restaurant` collection where `borough` == "Brooklyn"
3. Get `name`, `restaurant_id` from `restaurant` collection where `borough` == "Staten Island"
4. Get `address` from `restaurant` collection where `borough` == "Manhattan"
5. Get `name`, `cuisine` from `restaurant` collection where `borough` == "Bronx"
6. Get `name`, `grades` from `restaurant` collection where `grade` == "A" and `score` is less than 10
7. Get `name`, `grades` from `restaurant` collection where `grade` == "B" and `score` is greater than or equal to 15 and less than 25
8. Get `name` from `restaurant` where `cuisine` == "Steak" and one of the `grades`.`grade` is "A"
9. Get `name`, `address` from `restaurant` where `cuisine` is either "Filipino", "Thai", or "Japanese" that is within 40 to 41 latitude, and -73 to -74 longitude
10. Get `name`, `address.coords` from `restaurant` where `cuisine` is either "French", or "Italian" that is within 40 to 41 latitude, and -73 to -74 longitude

## Delivarables
1. on the file `scripts/raymundo_jinopaulo.js` (example):

```
db = db.getSiblingDB('restaurant');

var query01 = db.find();  // this is where you should write your answers to 
print(`Question 01: `);
printjson(query01);

...

var query10 = db.find();  // this is where you should write your answers to 
print(`Question 10: `);
printjson(query10);
```

2. To test your answers:
```
docker exec -it dataopt-quiz03 bash
mongosh scripts/raymundo_jinopaulo.js
```


## Cleanup
1. Once done with the quiz, issue the following commands:
```
docker stop dataopt-quiz03
```

2. (optional) to start the container again:
```
docker start dataopt-quiz03
```
