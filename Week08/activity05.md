# Activity 05: MongoDB local development environment

## 1. Start with the following `docker-compose.yml` file:
```
version: '3.8'
services:
  mongo:
    image: mongo
    container_name: dataopt_mongodb
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: example
    volumes:
      - ./db:/data/db
    ports:
      - 27017:27017
  mongo-express:
    image: mongo-express
    container_name: dataopt_mongodb_express
    restart: always
    ports:
      - 8081:8081
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: root
      ME_CONFIG_MONGODB_ADMINPASSWORD: example
      ME_CONFIG_MONGODB_URL: mongodb://root:example@mongo:27017/
      ME_CONFIG_BASICAUTH_USERNAME: admin
      ME_CONFIG_BASICAUTH_PASSWORD: password
```

## 2. build the containers
```
docker compose up -d --build
```

## 3. use `mongosh` (mongo shell)
```
docker exec -ti dataopt_mongodb mongosh -u root -p example
```

--- 

## 4. access the mongo-express app via http://localhost:8081

## 5. Create a **database** named "dataoptFirstDB"

## 6. Create a **collection** named "nakama" with the following data:

```
name: Monkey D. Luffy
age: 19
devilFruit: Gomu Gomu no mi
role: Captain

name: Roronoa Zoro
age: 21
weapon: swords
role: First Mate

name: Nami
age: 20
weapon: clima tact
role: Navigator

name: Usopp
age: 19
alternateEgo: Sogeking
role: Sniper

name: Sanji
age: 21
role: Cook
```

## 7. Create a **database** named "sampleDB"
## 8. download the dataset [here](https://github.com/ozlerhakan/mongodb-json-files/blob/master/datasets/restaurant.json)
## 9. copy the data from the host unto the docker container:
```
docker cp restaurant.json dataopt_mongodb:/tmp/restaurant.json
```
## 10. "bash" into the mongo container
```
docker exec -ti dataopt_mongodb bash
```
## 11. run `mongoimport` to import the data into mongodb:
```
mongoimport -u root -p example --authenticationDatabase admin --db restaurant  --type json --file /tmp/restaurant.json
```

---

# using `mongosh`
```
docker exec -ti dataopt_mongodb mongosh -u root -p example

use restaurant
```
