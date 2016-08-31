# Coding with Archiejs

This is a tutorial about creating archiejs modules. The tutorial has below parts, where we will :-

* Part 1. Creating modules - different semantics of archiejs modules
* Part 2. Starting the application - loading all archiejs modules
* Part 3. TDD - Explore unit testing of archiejs modules
* Part 4. Version control - Version control of archiejs modules


### Modules semantics in points

  * A module is container for one or many services, which the module `provides` to others. 
   * The services modules are are specified in `plugin.provides` key (in `package.json`).
   * A module with only one service to provide (and none to consume), can be just an `index.js` file with an `export`'ed function (we usually name `setup`).
   * A module can also consume other services by specifing them in `consumes` tag (in `package.json`).
   * A service is usually a function or an object; but can also be a primitive.
  * Given a number of services, archiejs will orchestrate their initialization sequence as per the dependeny tree.
   * On initialization completion (success/failure), a callback function is initiated. 
   * If some service is consumed, but not provided, it will result in appropriate `error` and the application will not run.


## Part 1 - Creating modules - Different semantics of Archiejs modules

There are multiple ways of creating archiejs modules. In below example, we will start with a very simple module (which does nothing and is composed in a single function) and move towards more complex examples. This might be lengthy, because its comprihensive. You may not need to read this word by word.


### Simple Modules

#### One function module - does nothhing

We will create a very simple module which does not provide or consume any service.

modules/theModuleName/index.js
```
module.exports = function setup(options, imports) {
  console.log('module initialized');
}
```
./app.js
```
const archie = require('archiejs');
const theModules = [ 'modules/theModuleName' ];
const theDependencyTree = archie.resolveConfig(theModules, __dirname);
archiejs.createApp(theDependencyTree, (err) => {...});
```

When we run `node app.js`, the (1) setup function is called and 
followed by (2) the callback function in `createApp`.

#### Passing options to modules

Says hello _name_ ; where name is passed via `options`.

modules/theModuleName/index.js
```
module.exports = function setup(options, imports) {
  console.log(`Hello {options.name}`);
}
```
./app.js (line number 4 added)
```
const archie = require('archiejs');
const theModules = [ {
  packagePath: 'modules/theModuleName',
  name: 'Raghu'
];
const theDependencyTree = archie.resolveConfig(theModules, __dirname);
archiejs.createApp(theDependencyTree, (err) => {...});
```

Outputs, Hello Raghu.

In examples examples so far, our module was not providing any services. We
will now make a module which will `provide` a service. Again, there are multiple
formats for this and we will start with a simple one.

#### Providing a service for other modules 

We will create a new module file `time.js` that provides a 
service `theTimeNow` . The service `theTimeNow` tells the time. Note,
we are no longer using the default name - `index.js`, for the main
file.

modules/theTime/package.json
```
{
  ...
  main: 'time.js',
  plugin: {
    provides: 'theTimeNow'
  }
}
```
modules/theTime/time.js
```
module.exports = function setup(options, imports) {
  return {
    'theTimeNow': () => new Date()  
  }
}
```
Next, lets add one more service into `time.js`

#### A module with two services

modules/theTime/package.json
```
{
  ...
  main: 'time.js',
  plugin: {
    provides: [ 'theTimeNow', 'isItLate' ]
  }
}
```
modules/theTime/time.js
```
module.exports = function setup(options, imports) {
  return {
    'theTimeNow': () => new Date(),
    'isItLate': () => new Date().getHours() > 22 
  }
}
```
Next, we can create a module with two `js` files.


### Complex modules

#### A module with two javascript files

A module can also have many javascript file, each file exports a service in its `setup` function.
Notice, how `package.json` changes (ie provides becomes a hashmap of `serviceName : fileName.js` pairs).

modules/theTimeModule/package.json
```
{
  ...
  plugin: {
    provides: {
      'earthTime': 'earth.js',
      'spaceTime': 'space.js'
    }
  }
}
```
modules/theTimeModule/earth.js
```
module.exports = function setup(options, imports) {
  return {
    'theTimeNow': () => new Date(),
    'isItLate': () => new Date().getHours() > 22 
  }
}
```
modules/theTimeModule/space.js
```
module.exports = function setup(options, imports) {
  return {
    'theSpaceTimeNow': () => 'about five billion years'
  }
}
```

#### Dependency Injection using the cosumes tag

Modules consume services provided by other modules. 

The time depends on the location of person. Therefore, `theTimeModule` now consumes a
service `locationService`; which is provided by `theLocationModule`. (Notice, module names
are different from the services they provide. It can be confusing for some)

modules/theTimeModule/package.json
```
{
  ...
  plugin: {
    consumes: [ 'locationService' ],
    provides: {
      'earthTime': 'earth.js',
      'spaceTime': 'space.js'
    }
  }
}
```

In above, `earth.js` and `space.js` will have a function `setup` function each - which returns
`{ earthTime }` and `{ spaceTime }` services respectively (like in some previous examples). 

Another module, say with a name `theLocationModule`, provides a service known as `locationService`.
(Below example uses a format where the code will be located in `index.js`).

modules/theLocationModule/package.json
```
{
  ...
  plugin: {
    consumes: [],
    provides: [ 'locationService ' ]
  }
}
```

Now we have two modules (with names) `theTimeModule` and `theLocationModule`. They form an archiejs
app, by using below APIs :-

./app.js
```
const archie = require('archie');
const theAppConfig = [
  'theTimeModule',
  'theLocationModule'
];
const deptree = archie.resolveConfig(theAppConfig', './');
archie.createApp(deptree, (err, app) => { // started });
```

For now, this gets our app running. The modules will be loaded in order of dependency injection -
(1) theLocationModule (2) theTimeModule. Their placement of theAppConfig is not relevant.

Also to access the loaded services from callback in createApp, we can use `app.services`.

We will explore passing `options` to setup functions in the module via `theAppConfig` in
*Part 2* of this tutorial.


### Using es5 and es6 singleton objects as services

When using objects as services, we are required to use below format in `package.json` provides.

theModuleName/package.json
```
{
  ...
  plugin: {
    provides: {
      'service1': 'file1.js',
      'service2': 'file2.js'
    },
    consumes: [ ... ]
  }
}
```

Where `file1.js` and `file2.js` are javascript class definitions. 

The `setup` functions, dont return service objects (like above examples). Archiejs
instantiates these classes into singleton objects and injects them into other modules
that consume these services.


file1.js
```
module.exports = ExampleClass = function(options, imports) {
   // constructor stuff
   this.myVariable = options.passedValue;
}

ExampleClass.prototype.doSomething = function() { ... }
```

or we could use es6 class,

```
class ExampleClass {
  constructor(options, imports) {
    // add code
  }
  
  doSomething() {
    // add code
  }
}

module.exports = ExampleClass;
```

#### using a promise in service setup function

Sometimes, we may want to do async operations in the constructor. 
In this case, we have to return a `promise` which resolves into
the service. 

The below example, shows such a setup function where some functions in 
the module are exported as services (`serviceA` and `serviceB`).

```
module.exports = function setup(options, imports) {
  return new Promise(resolvefn)
    .then(anotherfn)
    .then(() => {
      serviceA: serviceA_Fn,
      serviceB: serviceB_Fn
    });
}
```

Suppose we were providing an es5 object (ie. `this`) - this was covered in the 
section before. The solution is that last `then` of the promise, returns `this`.

```
module.exports = function setup(options, imports) {
  const obj = this; // ref to the service-object
  return new Promise(resolvefn)
    .then(anotherfn)
    .then(() => obj);
}
```

In both the cases, archiejs receives the service object from the final `then`
statement in the promise.


#### Injecting a class, instead of a singleton object

By default, when an archiejs module uses *es5 or es6 format*; archiejs
creates a singleton instance from the module using new operator. This can 
be a problem when we dont want to use new operator on the module exported
value (for example, when we want to inject mongoose schemas, we inject
schema classes, so that they can be used to create mongodb documents, etc).

We dont want to instantiate before injecting a class with es5/es6 format of `provides`
tag, we can add an `__instantiateBeforeInjection: false` setting to the `plugin` in `package.json`.

package.json (excerpt)
```
  plugin: {
    __instantiateBeforeInjection: false,
    provides: {
      ServiceAClass: 'moduleA.js'
    },
    consumes: [ ... ]
  }
```

If we had not added `__instantiateBeforeInjection: false`, archiejs would create an
instance of `moduleA`, name it `ServiceAClass`, before injecting it in consumers.


### Part 2 - Starting the application - loading all archiejs modules

_(is duplicate of content in module_faq.md...)_

An application in archiejs is a sum of a number of services (services are provided 
and consumed by modules). We make a list of all our modules and pass them to the
archiejs library - to make instances of modules and inject modules - thus instantiate
our application. Below is an example of such a list,

```
var theAppModules = [
  {
    packagePath: 'modules/mymodule1',
    ... config options ...
  },
  'modules/mymodule2'
]
```

Next, we the theAppModules to archiejs for creating the dependency tree.

```
var servicesTree = Archie.resolveConfig(theAppModules, process.cwd()); 
Archie.createApp(servicesTree, function(err, archie) {
    if(err){
        throw err;
    }
    // ready
});
```

There we hava a running archiejs application.

NOTE: the second argument in resolveConfig (above) is the root path, relative to which all packagePath's are loaded.

For a better example, refer [our demo appliaction](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner) (see the files [deptree.js](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/blob/master/deptree.js) and [app.js](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/blob/master/app.js)).



### Part 3 - TDD - Explore unit testing of archiejs modules

_(is duplicate of content in module_faq.md...)_

Each of the module should be sufficiently isolated from other modules and have their own testcase folder. 

For example, see `test` folder in the [example app](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/tree/master/modules/googledrive).

Also see the file [`test/archie-unit.js`](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/blob/master/modules/googledrive/test/archie-unit.js) which loads the dependencies for testcases.


### Part 4 - Version control - Version control of archiejs modules

_(is duplicate of content in module_faq.md...)_

Version control is specially important if we plan to use our modules as microservices. Here is one way
of supporting different versions of a module.

package.json extract the provider module (provides v1 and v2 of someService)
```
   provides: {
     v1: {
       someService: './v1/file.js'
     },
     v2: {
       someService: './v2/file.js'
     }
   }
```

package.json consumes v1 of someService
```
    consumes: [ 'v1.someService' ]
```

Other versions can be consumed in the same manner. Thus we have implemented a version control
using archiejs modules.

Also, you might find the [kue enhancer](https://github.com/archiejs/archiejs-kue-enhancer) interesting, if you want to
write microservices with archiejs.


### Conclusion

Archiejs modules are a bare minimum delta over npm modules.

We have learnt that archiejs modules can be written in many ways, depending on the
complexity of the module. They can be unit tested and versioned very conveniently.
