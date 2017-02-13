####Configuring Agent Application 

###Parameters
Mutable environmental variables that can be modified in Agent Manager. Values can overwrite default settings.

Property    | Type    | Description
------------|---------|-----------
description | String  | Description in Agent manager application
type        | String  | Expected data type of parameter value
setting     | String  | Assigend variable name to this parameter
required    | Boolean | True or False
default     | String  | The default value of the parameter if not set

> **Parameters example**

```
parameters : {
        master_id: {
            description : 'System ID of Master Agent',
            setting     : 'master_id',
            type        : 'string',
            required    : true
        },
        role: {
            description : 'Role of Master Agent for Slave to assume',
            type        : 'string',
            setting     : 'role',
            required    : true
        }
}
```

###Extensions
Extensions are injected dependencies that your application can refer to. Your application may use one or more extensions. Extensions can provide potential configuration components or actual runtime components. Extensions are a good way to design resuable components that can be shared and reused across projects. Extensions are loaded in the order in which they are specified.

Property | Type    | Required | Description
---------|---------|----------|-----------
module   | String  | Yes      | By default seraches node_modules folder. Relative path also accepted


> **Extensions example**

```
extensions  : [
        { module: './lib/plugin.js' },
        { module: 'agent-ext-timers' }
]
```


###Settings
An array of environmental variables that have assigned default values. Parameters can overwrite a setting if the property matches a parameter key.
These values will take the highest precedence in the processing of settings. The precedence rules are:

1. Agent.json settings object (highest precedence)
2. Any settings within the js/json files in the settings folder
3. Any settings added by an extension (lowest precedence)


Property | Type   | Required | Description
---------|--------|----------|------------
property | String | Yes      | Name of your property
value    | String, Function, Boolean, Number, Object | Yes | The value of your setting


> **Settings example**

```
settings: [
        {
            property: 'master_id',
            value: '588f9fc508a94349cc1ad3b8'
        },
        {
            property: 'role',
            value   : 'pos-monitor'
        }
]
```


###Counters
Tracks the number of times specific application events occur and are logged in the Agent heartbeat. Each event can subscribe to an array of application events. 

> **Counters example**

```
 counters: {
        activations : ['app:monitor'],
        success     : ['app:success'],
        stopped     : ['app:stopped'],
        failed      : ['app:failed' ]
}
```



###Sources
An object that sources external events. Sources bind events to listeners and emits application level events. Any counters, handlers and pipelines subscribed to source events are initiated.

Property | Type   | Required | Description
---------|--------|----------|-----------
name     | String | Yes      | Name of your service
provider | String or Function | Yes      | A function or reference to a plugin that creates an object
args     | Array of Strings, Functions, Objects, Booleans | Optional | A list of dependencies used by the service
bindings | Object | Optional | Map of internal source events to application level events


> **Sources example**

```
sources: [ 
		{
		   name: 'sampleSource',
		   provider: 'compris:dir',
		   args: ['$settings:rootPath'],
		   bindings: { 'created' : 'read' }
		} 
]
```




###Services
Services are singletons. They are functions that return an object that is reusable across your application. It's an object that represents a concrete extension of the API.

Property |	Type |	Required|	Description
---------|--------|----------|--------------
name     | String |	Yes      |	Your name of your service
provider | String or Function |	Yes      |	A function or reference to a plugin that creates an object
args     | Array of Strings, Functions, Objects, Booleans | Optional | A list of the dependencies used by the service
factory	| string (constructor, function, literal) |	Optional |	An enumeration that describes alternate instantiation behavior for the service

> **Services example**

```
services: [
        {
            name: 'cloud',
            provider: 'connection:resources'
        }
]
```


###Handlers
Handlers subscribe to event(s) and executes its one function.

Property      |	Type   | Required |	Description
--------------|--------|----------|--------------
name          | String | Yes      | Name of your handler
subscriptions | Array  | Yes      | String of application level events that will initiate this handler
fn            | String or Function| Yes | A function or reference to a plugin function
props         | Object | Optional | Key value pair that will be injected into the function context referenced in the keyword "this"        


> **Handlers example**

```
handlers: [
        {
            name            : 'Monitor Master Agent',
            subscriptions   : ['app:monitor'],
            fn              : '$plugins:handler:monitor',
            props           : {
                master_role : '$setting:role',
                conn        : '$service:cloud',
                master_id   : '$setting:master_id',
                getInfo     : '$plugins:core:info',
                identity    : '$plugins:core:identity',
            }
        },
        {
            name            : 'Update Agent Role',
            subscriptions   : ['app:update'],
            fn              : '$plugins:handler:update',
            props           : {
                conn        : '$service:cloud',
            }
        }
]
```



###Pipelines
Similar to handlers, pipeline(s) are subscribed to event(s). The difference being that pipelines execute a series of steps rather than just one function. 
Each pipeline step should follow the single responsiblity principle. Each step is given two arguments - input and a callback.


Property      |	Type   | Required |	Description
--------------|--------|----------|--------------
name          | String | Yes      | Name of your pipeline
subscriptions | Array  | Yes      | String of application level events that will initiate this pipeline
steps         | Array  | Yes      | Takes an array of objects that refer to function plugin references as well as an optional injected props referenced by the keyword "this"
stopped       | String | Optional | Emits mapped event based on the state of the pipeline
failed        | String | Optional | Emits mapped event based on the state of the pipeline
success       | String | Optional | Emits mapped event based on the state of the pipeline
done          | String | Optional | Emits mapped event based on the state of the pipeline

> **Pipelines example**

```
// pipeline breakdown of handlers

    pipelines: [
        {
            name: 'Monitor Master Agent',
            subscriptions: ['app:monitor'],
            steps: [
                { fn: '$plugins:core:identity:addAgentInfo'     },
                { fn: '$plugins:main:checkMasterAgentStatus'    },
                { fn: '$plugins:main:processAgentStatus'        }
            ],
            stopped : 'app:stopped',
            failed  : 'app:failed'
        },
        {
            name: 'Update Status',
            subscriptions: ['app:update'],
            steps: [
                { fn: '$plugins:main:patchAgentRole'    },
                { fn: '$plugins:main:syncAgent'         }
            ],
            stopped : 'app:stopped',
            failed  : 'app:failed'
        }
]
```




###Init

Init is a function that is given a callback as its only argument 
This callback must be invoked in order to intialize the application. 
The keyword "this" refers to the application's reactive context

> **Init example**

```
init: function(done){

        this.publish('app:initialized');

        console.log('###################################');
        console.log('## ' + pkg.name.toUpperCase());
        console.log('## v' + pkg.version);
        console.log('###################################');

        done();
}
```