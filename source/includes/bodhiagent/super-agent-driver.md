Installation
---------

This library lives in artifactory now and will become public soon

````
npm install bodhi-rest-superagent
````

Basic API
---------

var api      = require('bodhi-rest-superagent')
var Client   = api.Client;
var Basic    = api.BasicCredential;
var Bearer   = api.BearerToken;
var agent    = api.createAgentClient('token', 'my-ns');
var user     = api.createUserClient('username', 'password', 'my-ns');

````
var api      = require('bodhi-rest-superagent')
var Client   = api.Client;
var Basic    = api.BasicCredential;
var Bearer   = api.BearerToken;
var agent    = api.createAgentClient('token', 'my-ns');
var user     = api.createUserClient('username', 'password', 'my-ns');
````

###Simple Setup

Let the package do the standard setup and supply the credentials plus the namespace

var agent    = api.createAgentClient('token', 'my-ns');
var user     = api.createUserClient('username', 'password', 'my-ns');

````
var agent    = api.createAgentClient('token', 'my-ns');
var user     = api.createUserClient('username', 'password', 'my-ns');
````

###Custom Setup

Take control of the entire setup process.

var Client   = api.Client;
var Basic    = api.BasicCredential;

var client = new Client({
    uri          : 'https://local:1337'
    namespace    : "miles",
    credentials  : new Basic('me', 'secret')
});

````
var Client   = api.Client;
var Basic    = api.BasicCredential;

var client = new Client({
    uri          : 'https://local:1337'
    namespace    : "miles",
    credentials  : new Basic('me', 'secret')
});
````

###Resource Identifiers

The api is tolerant of both absolute and relative URLs. 

####Relative URIs

A relative URIs can be specified as a string or an array of path elements. Relative URIs are relative to the namespace.

client.[<http-operation>]('relative/url', function(err, data, ctx){})
client.[<http-operation>](['resources', 'Store', id], function(err, data, ctx){})

````
client.[<http-operation>]('relative/url', function(err, data, ctx){})
client.[<http-operation>](['resources', 'Store', id], function(err, data, ctx){})
`````

####Absolute URIs

Absolute URIs start with a '/' character. They ignore the established namespace but honor the authority. It can be used for public API calls , /me, anything that wants to bypass the namespace. When using arrays the first element MUST include the '/' character as the first character.

client.[<http-operation>]('/absolute/url', function(err, data, ctx){})
client.[<http-operation>](['/me'], function(err, data, ctx){})

````
client.[<http-operation>]('/absolute/url', function(err, data, ctx){})
client.[<http-operation>](['/me'], function(err, data, ctx){})
````

###Reading Data

fetch: Get a single document

client.fetch(uri, function(err, jsonObject, res))

````
client.fetch(uri, function(err, jsonObject, res))
````

get: get a set of documents

client.get(uri, function(err, jsonArray, res))

````
client.get(uri, function(err, jsonArray, res))
````


getPages: get a few pages of documents

client.getPages(uri, function(err, jsonArray, res))

````
client.getPages(uri, function(err, jsonArray, res))
````


getAll: get all pages of documents

client.getAll(resources/:type?where={/*scope*/}, function(err, jsonArray, res))

````
client.getAll(resources/:type?where={/*scope*/}, function(err, jsonArray, res))
````

gather: get several objects concurrently

var resources = {
  a: "resource/:type?where={/*scope*/},
  b: "resource/:type?where={/*scope*/},
  c: "resource/:type?where={/*scope*/},
}

client.gather(resources, function(err, json, res){
    console.log(json.a)  //= [/* results of a */]
    console.log(json.b)  //= [/* results of b */]
    console.log(json.c)  //= [/* results of c */]
})

````
var resources = {
  a: "resource/:type?where={/*scope*/},
  b: "resource/:type?where={/*scope*/},
  c: "resource/:type?where={/*scope*/},
}

client.gather(resources, function(err, json, res){
    console.log(json.a)  //= [/* results of a */]
    console.log(json.b)  //= [/* results of b */]
    console.log(json.c)  //= [/* results of c */]
})
````

gatherAll: get all pages of all object concurrently

client.getAll(resources, function(err, json, res){
    console.log(json.a)  //= [/* results of a */]
    console.log(json.b)  //= [/* results of b */]
    console.log(json.c)  //= [/* results of c */]
})

````
client.getAll(resources, function(err, json, res){
    console.log(json.a)  //= [/* results of a */]
    console.log(json.b)  //= [/* results of b */]
    console.log(json.c)  //= [/* results of c */]
})
````

###Sending Data

post: Create a new instance of the document

client.post('resources/:type' , {/* your data here */}, function(err, data, ctx){})

````
client.post('resources/:type' , {/* your data here */}, function(err, data, ctx){})
````

postAll: Create new instances of new types on the system

var bag = {
    'resources/MyType': {name: "name", uri: "http://localhost/a/b", system_v: true }
    'resources/AType' : [{a: 'A'}, {a: 'B'}, {a: 'C'}]
    'resources/DType' : [{d: 'D'}, {d: 'E'}, {d: 'F'}]
}

client.postAll(bag, function(err, data, ctx){
        data['resources/MyType'] //= header
        data['resources/AType'] //= [location, location, location]
        data['resources/DType'] //= [location, location, location]
})

````
var bag = {
    'resources/MyType': {name: "name", uri: "http://localhost/a/b", system_v: true }
    'resources/AType' : [{a: 'A'}, {a: 'B'}, {a: 'C'}]
    'resources/DType' : [{d: 'D'}, {d: 'E'}, {d: 'F'}]
}

client.postAll(bag, function(err, data, ctx){
        data['resources/MyType'] //= header
        data['resources/AType'] //= [location, location, location]
        data['resources/DType'] //= [location, location, location]
})
````

put: Replace an existing document by id

client.put('resources/:type/:id', {/* your updated resource here */}, function(err, data, ctx){})

````
client.put('resources/:type/:id', {/* your updated resource here */}, function(err, data, ctx){})
````

patch: Patch an exising document by id

client.patch('resources/:type/:id', {/* your patch document here */}, function(err, response, ctx){})

````
client.patch('resources/:type/:id', {/* your patch document here */}, function(err, response, ctx){})
````

upsert: Create new or update existing document. Will produce an error if the system encounters more than one matchin document.

client.upsert('/absolute/url?where={/*scope*/}', {/* your updated resource here */}, function(err, data, ctx){})

````
client.upsert('/absolute/url?where={/*scope*/}', {/* your updated resource here */}, function(err, data, ctx){})
````

####Composite Operations

Update one or multiple documents. 

client.fetchAndUpdate('/absolute/url?where={/*scope*/}', updateFunction, function(err, data, ctx){})

client.findAndUpdate('/absolute/url?where={/*scopt\e*/}', updateFunction, function(err, data, ctx){})

````
client.fetchAndUpdate('/absolute/url?where={/*scope*/}', updateFunction, function(err, data, ctx){})
client.findAndUpdate('/absolute/url?where={/*scopt\e*/}', updateFunction, function(err, data, ctx){})
````

Patch a document by query. Will produce an error if the system encounters more than one matchin document.

client.fetchAndPatch('/absolute/url?where={/*scope*/}', updateFunction, function(err, data, ctx){})

````
client.fetchAndPatch('/absolute/url?where={/*scope*/}', updateFunction, function(err, data, ctx){})
````

fetchAndExtend: grab a document and change the properties in the mergeObject then update it. Will produce an error if the system encounters more than one matchin document.

var mergeObject = {
    a: 'A',
    flag: true
    my_date: new Date().now()
}

client.fethcAndExtend('/absolute/url?where={/*scopt\e*/}', mergeObject, function(err, data, ctx){})

````
var mergeObject = {
    a: 'A',
    flag: true
    my_date: new Date().now()
}

client.fethcAndExtend('/absolute/url?where={/*scopt\e*/}', mergeObject, function(err, data, ctx){})
````

###Removing Data

Remove a document by sys_id

client.remove('/absolute/url/id' , {/* your data here */}, function(err, data, ctx){})

````
client.remove('/absolute/url/id' , {/* your data here */}, function(err, data, ctx){})
````

Remove document(s) that match a specific URL with scope

client.fetchAndRemove('/absolute/url?where={/*scope*/}' , function(err, data, ctx){})

````
client.fetchAndRemove('/absolute/url?where={/*scope*/}' , function(err, data, ctx){})
````

Remove a set of documents that mactch a specific URL with scope

client.findAndRemove('/absolute/url?where={/*scope*/}' , function(err, data, ctx){})

````
client.findAndRemove('/absolute/url?where={/*scope*/}' , function(err, data, ctx){})
````

Responses
---------

The service response is available via a callback of the form:

function(err, data, ctx)

````
function(err, data, ctx)
````

###Error Object

####System Errors

Same as before ... bad things happen at the infrastructure/runtime layer. The error will have a few elements added to it.

####Protocol Errors

Anything with a 4XX or 5XX error code

* err.api     true
* err.status  http status code (deprecated)
* err.statusCode  to be consistent with the other 
* err.source  method, resource, and representation of the request
* err.message the message from the API server error
* err.code    code from the api server
* err.context parameters returned by the api server

###Data Element

* for a 200 data        = the returned JSON
* for a 201 or 202 data = content of the location header
* for a 204 data        = null

###Context Element

1. ctx.statusCode,
2. ctx.headers,
3. ctx.request = the method, resource, and representation of the original request
