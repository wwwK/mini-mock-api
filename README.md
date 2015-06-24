# mini-mock-api
Lightweight node.js API mock server, route calls to static JSON files

## What does it do?

Mini-Mock-API was written to mock a simple API in a few minutes. API calls are routed to static JSON files.
As an example if your mock directory looks like this: 
```
+ mock-files
  - cars.json
  - trains.json
  + oldschool
    - carriages.json
```

with cars.json
```
[
  {id: 1, name: 'Porsche 911'},
  {id: 2, name: 'Tesla S'}
]
```

`GET localhost:8080/cars`

returns all cars inside cars.json

`GET localhost:8080/cars/1`

returns one car with the id == 1

`GET localhost:8080/oldschool/carriages`

returns all items from oldschool/carriages.json


## Installation

`npm install mini-mock-api`

## Usage

```
var API = require('mini-mock-api');
var myApi = new API({
  basePath: '/api/v1',
});
myApi.start();
```

see examples/example.js

## Options
```
{
  mockPath: 'mocks', //directory to mock files relative to path of script
  basePath: '/api',  //base path for api calls -> localhost:8080/api/...
  port: 8080,
  idAttribute: 'uuid', //the id property to search for when requesting api/cars/123
  sortParameter: 'sortOrder' //the GET parameter for sort orders e.g. api/cars?sortOrder=+name
}
```

## Decorate

All API responses can be decorated by defining a `decorate` function. In this example all returned collections are wrapped into `results` and a total count is added.

```
myApi.decorate = function(data){
  if(data.length){
    return {
      results: data,
      total: data.length
    };
  }
  return data;
};
```

## Can i use this in production?

Hell no!
