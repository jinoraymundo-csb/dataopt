# DATAOPT Final Exams

1. Start with `finals` directory
2. Download the sample dataset [here](https://raw.githubusercontent.com/IronPTSolutions/mongo-examples/master/datasets/companies.json) and save it on `finals` folder
3. add a `scripts` folder under `finals` folder
4. name your file as `FE_<lastname>_<firstname>.js` e.g. `FE_raymundo_jinopaulo.js`
5. execute the following docker commands on the terminal:
```
docker run --name dataopt-finals --rm -p 27017:27017 -v ${PWD}/scripts:/scripts -d mongo:latest
docker cp companies.json dataopt-finals:/tmp/companies.json
docker exec -it dataopt-finals bash
mongoimport --db company --file /tmp/companies.json
```

> 300 documents should have been inserted

## Questions
1. Find all `company` that has `category_code` == "web", get only the "name" field (127 documents)
2. Find all `company` that has more than 100 "employees", get only the "name" and "number_of_employees" fields (45 documents)
3. Find all `company` that "Peter Thiel" has worked with, get only the "name" and "permalink" fields (4 documents)
4. Find all company names that is a competitor of "Facebook" (7 documents)
5. Find all `company` that has an office in city: "Seattle" and state_code: "WA", get only the "name" and "description" fields (16 documents)

## Deliverables
1. on the file `scripts/FE_raymundo_jinopaulo.js` (example):

```
db = db.getSiblingDB('company');

var query01Filter = {};
var query01Options = {};
var query01 = db.companies.find(query01Filter, query01Options)
printjson(query01);
print(`Question 01 count: ${query01.count()}`);

...

var query10Filter = {};
var query10Options = {};
var query10 = db.companies.find(query10Filter, query10Options)
printjson(query10);
print(`Question 10 count: ${query10.count()}`);
```

2. To test your answers:
```
docker exec -it dataopt-finals bash
mongosh scripts/FE_raymundo_jinopaulo.js
```


## Cleanup
1. Once done with the exam, issue the following commands:
```
docker stop dataopt-finals
```

2. (optional) to start the container again:
```
docker start dataopt-finals
```
