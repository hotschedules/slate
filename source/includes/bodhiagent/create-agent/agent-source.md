####Creating an Agent Source

Returns a function that instantiates an Agent source. See sample code that watches for any directory changes using npm watch.

> **Sample Code:**

```
var fs      = require('fs-extra');
var watch   = require('watch');

module.exports = function dirSrc() {
    var path        = arguments[0];
    var source      = {};
    source.routers  = {};

    var bind = function bindDir(bindings, emitter, done) {
        var logger = this.logger;

        logger.info('Ensuring ', path, 'exists...');

        if (!path) return done('Expected path to exist. Please ensure args array is properly configured.');

        fs.ensureDir(path, function (err) {
            if (err) return done(err);

            logger.info(path, 'ensured.');
            /*
                bindings = { 'created' : 'read' }
                emitter = fn()  { context.emit.apply(context, arguments); }
                done = fn()      { return exit(done, source); }

                YOU HAVE TO CALL DONE OR ELSE THE REST OF THE APP WILL NOT LOAD
                KICK LISTEN OR IT WILL NOT HEAR
            */

            // routes = ['created']
            var routes = Object.keys(bindings);

            /*
                routers = {

                        emitter(event, arguments);
                    }
                }
            */
            routes.forEach(function (event) {
                source.routers[event] = function () {
                    emitter(bindings[event], { path: arguments[0], detail: arguments[1] });
                }
            });

            done();
        });
    };

    /*
        SOURCES GET LOADED BEFORE INIT
            ENSURE DIR BEFORE SETTING MONITORS
    */
    var listen = function listenDir(cb) {
        watch.createMonitor(path, function (monitor) {
            source.monitor = monitor;
            ['created', 'changed', 'removed'].forEach(function (e) {
                if (source.routers[e]) {
                    source.monitor.on(e, function (file, detail) {
                        source.routers[e](file, detail);
                    });
                }
            });
        });
    };

    var close = function closeDir() {
        source.monitor.stop();
    };

    return function (cb) {
        cb(null, { bind: bind, listen: listen, close: close})
    }
};
```


Property | Type     | Description
---------|----------|-------------
bind     | Function | Responsible for binding application level events when a source level event occurs 
listen   | Function | Creates EventEmitter that emit application level events based on bind
close    | Function | Destroy existing EventEmitter for the source
