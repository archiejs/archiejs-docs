# ArchieJs Modules - FAQ

## Q&A about modules

### Q. How are Archiejs modules are different from npm modules?

Ans: Not very different - are an enhancement. 

Your business logic/services require some lifecycle management, which NPM modules 
dont provide out of the box. So we wrote a thin wrapper over NPM modules to make
them better for writing business logic. 

We added following :-

1. Support for lifecycle events of initialization and termination. 
2. Automatic depenency injection of modules into one-another based on `provides` and `consumes` tags
3. Enchance modules by specifying `enhancer` tag

### Q. How to write an Archiejs module?

_You will also need to read the next Q&A, `How to club archiejs modules together in an application`?_

1. Create a directory for your module 
    
  ```
  $ mkdir -p modules/mymodule
  $ cd modules/mymodule
  $ npm init
  $ touch service1.js service2.js
    ```
    
2. Change the contents of `package.json` as follows. 

  Remove
  
  ~~main: 'index.js',~~
  
  Add or replace with
  
  ```
  plugin: {
     provides: {
        Service_1: 'service1.js',
        Service_2: 'service2.js'
     },
     consumes: [
        'Optional_Some_Service_We_Consume',
        'Optional_Another_Service_We_Consume'
     ]
  },
  ```
    
3. In file `service1.js`;
    
  we can use es5 classes
    
  ```
  module.exports = function setup(configs, imports) {
    // return a promise (that returns this/object) or a simple function
  }
    
  setup.prototype.doSomething = function() {}
  ```
    
  or es6 classes
    
  ```
  class Service1 {
    constructor(configs, imports) {
      // return a promise (that returns this/object) or a simple function
    }
     
    doSomething() {}
  }
     
  module.exports = Service1;
  ```
    
Now we are ready to consume `Service1` and `Service2`, as we named them under `plugin.provides`.

Other semantics can be used to define module services can be found with the [testcases](https://github.com/archiejs/archiejs/tree/master/test).


### Q. How to club archiejs modules together in an application?

This is an explaination of `provides` and `consumes` dependency in archiejs modules. 

Add modules into a list, see [line 29 ie. `exports.app` here] (https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/blob/master/deptree.js).

In below example, we define two ways to link a module into the dependency tree created by archiejs. The first one below if a long form one (which also allows us to pass config options to the module). The second one below, is the shortform method.

```
var theAppModules = [
  {
    packagePath: 'modules/mymodule1',
    ... config options ...
  },
  'modules/mymodule2'
]
```

Next, pass the `linked_modules` to archiejs, for loading them ([see line 17 here](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/blob/master/app.js)).

```
var servicesTree = Archie.resolveConfig(theAppModules, process.cwd()); 
Archie.createApp(servicesTree, function(err, archie) {
    if(err){
        throw err;
    }
    // ready
});
```

NOTE: the second argument in resolveConfig (above) is the root path, relative to which all packagePath's are loaded.

Also, when we reach `ready` comment above, all the modules have been initialized (in the order derviced from their `produces` and `consumes` tags).


### Q. How to do TDD with archiejs modules?

Each of the module should be sufficiently isolated from other modules and have their own testcase folder. 

We the `test` folder in [example app](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/tree/master/modules/googledrive).

Also see the file [`test/archie-unit.js`](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/blob/master/modules/googledrive/test/archie-unit.js) which loads the dependencies for testcases.


### Q. What are enhancers?

`Enhancers` allow us to add a modify the services just before they are loaded. 

Enhancers is a not entirely a new concept. Enhancers are to Archiejs modules; what libraries like Promisify is to a function (ie. add wrappers over functions).

Some examples of enhancers are provided in demo apps,

1. [A mongodb enhancer](https://github.com/archiejs/archiejs-mongo-enhancer) and its usage in [demo application (models directory)](https://github.com/archiejs/demo-webapp-mongo-redis-ticket_booking/blob/master/models/package.json). It makes it convenient to provide mongoose models as archiejs services (which can be individually/explicitly consumed by other services ([see `consumes` here](https://github.com/archiejs/demo-webapp-mongo-redis-ticket_booking/blob/master/modules/bookings/package.json)).
2. [A kue enhancer](https://github.com/archiejs/archiejs-kue-enhancer) and its usage [demo application (microservice)](https://github.com/archiejs/demo-webapp-mongo-redis-ticket_booking). It makes it convenient to break models into separate microservices. You should see files `deptree.js` and `modules/bookings/package.json` to see semantics or usage of this particular enhancer.

Right now, archiejs does not have many `Enhancers`. Some were added for demo purposes.

We would be writing more about `enhancers` in future. 

# Summary of main points

* Modules are containers for services it `provides`.
* Modules are dependent on services it `consumes`.
* To create an app, all its constituent modules are specied in an array of constituting modules.
* The above array is consumed by Archiejs api `resolveConfig`, into a dependency tree.
* The dependency tree returned by resolveConfig is used to create an app with `createApp`
 


