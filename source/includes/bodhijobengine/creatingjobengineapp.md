**Work Functions** <br>
Jobs must be built in a specific format in order for Bodhi Job Engine to recognize and run them properly. The job should contain an **index.js** file that follows this structure:

> **index.js**

```
module.exports = function work(context, done){
    //the work of your job
    done(errThatOccurred, messageToReport, stateToSave);
};

```

**Context Object** <br>

Key        | Type            | Description
-----------|-----------------|------------
connection | bodhi-js-client | [https://www.npmjs.com/package/bodhi-driver-superagent](https://www.npmjs.com/package/bodhi-driver-superagent)
settings   | Object          | immutable configuration options associated with this job
state      | Object          | mutable persistent state from previous runs
meta       | Object          | immutable metadata about the job

> **meta**

```
{

}

```

**Job Metadata** <br>


Key       | Type   | Description
----------|--------|------------
name      | String | name of the job
package   | String | package name
version   | String | semantic package version
namespace | String | namespace of the job
lastRun   | Data   | last time the job ran

**Callback** <br>
A job must be completed by calling the callback

arg     | type   | required | description
--------|--------|----------|----------
err     | Error  | optional | if err != null then the job did not process properly
message | String | optional | a string to be recorded in the message
state   | Object | optional | the state to persist for the next run


**Example Job: Hello World**

> **This is a very basic Hello World job.**

```
module.exports = function(options, done){
  console.log('HELLO WORLD!');

  if(err){
    done(err);
  }
  else{
    done();
  }
};
```

**Example Job: Get and Use Some Data**
> **Get and use data**

```
module.exports = function(options, done){

  var client = options.connection;
  var data   = options.state;
  data.storestuff = [];

  client.get(['resources', 'Store'].join('/'), function(err, data, ctx){
    if(err){
      done(err);
    }
    else{
      data.forEach(function(store){
        data.storestuff.push(store.store_name + ' is an awesome store!');
      });
    }
  });

  var json = {

    "data1": "some data you need to post",
    "data2": "also data you need to post"
  };

  client.post(['resources', 'aCustomType'].join('/'), json, function(err, data, ctx){

    if(err){
      done(err);
    }
    else{
      console.log('Server says: ', ctx);
      done();
    }
  });
};

```

This is a less basic example job that uses HTTP requests and stores data in the "state" property of the options object. Data stored in the state property persists between jobs and is available in the next execution of the job.