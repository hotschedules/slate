####Creating an Agent Extension

Returns an Agent extension object.

Property | Type     | Description
---------|----------|-------------
name     | String   | Name of extension used primarily for debugging purposes 
attach   | Function | Attach the specified extension to this instance, extending the `ReactiveContext` with new functionality with the implicit registerPlugin method



> **Sample Code:**

```
module.exports = {
    name        : 'plugin',

    attach      : function (overloads, done) {

        /** LOAD HANDLERS **/
        this.registerPlugin(['handler', 'monitor'   ], require('./handlers/monitor.js'  ));
        this.registerPlugin(['handler', 'update'    ], require('./handlers/update.js'   ));

        done();
    }
};
```