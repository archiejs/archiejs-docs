# Coding with Archiejs

This is a tutorial about creating archiejs modules. The tutorial has below parts, where we will :-

* Part 1. Creating modules - different semantics of archiejs modules
* Part 2. Starting the application - loading all archiejs modules
* Part 3. TDD - Explore unit testing of archiejs modules


### Modules semantics in points

  * A module is container for one or many services, which the module `provides` to others. 
   * The services modules are are specified in `plugin.provides` key in `package.json`.
   * A module with only one service to provide (and none to consume), can be just an `index.js` file with a `setup` function.
   * A module can also consume other services by specifing them in `consumes` tag in `package.json`.
  * A number of services inside modules are aggregated together as a list to run as an application.
   * If some service is consumed, but not provided, it will result in appropriate `error` and the application will not run.


## Part 1 - Creating modules - Different semantics of Archiejs modules

There are multiple ways of creating archiejs modules. In below example, we will start with a very simple module (which does nothing and is composed in a single function) and move towards more complex examples. This might be lengthy, because its comprihensive. You may not need to read this word by word.


### Simple Modules

#### One function module - does nothhing

We will create a very simple module which does not provide or consume any service (can be
a function, an object or even a primitive).

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

#### Passing options to modules

Says hello _name_ ; where name is passed via `options`.

modules/theModuleName/index.js
```
module.exports = function setup(options, imports) {
  console.log(`Hello {options.name}`);
}
```
./app.js
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

#### Providing a service for other modules 

We will create a new module file `time.js` that provides a service `theTimeNow` . The service `theTimeNow` tells the time.

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

modules/theTime/package.json
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
modules/theTime/earth.js
```
module.exports = function setup(options, imports) {
  return {
    'theTimeNow': () => new Date(),
    'isItLate': () => new Date().getHours() > 22 
  }
}
```
modules/theTime/space.js
```
module.exports = function setup(options, imports) {
  return {
    'theSpaceTimeNow': () => 'about five billion years'
  }
}
```

#### Dependency Injection using the cosumes tag

Modules consume services provided by other modules. 

In above 'time' example, lets suppose that, the output depends on 'locationService'.

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
`{ earthTime }` and `{ spaceTime }` services respectively (like above examples). 

Another module, say with a name `theLocationModule`, provides a service known as `locationService`.
(Below example uses a format where the code will be located in `index.js`).

modules/theLocationModule/package.json
```
{
  ...
  plugin: {
    consumes: [],
    provides: [ 'theLocationService ' ]
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

For now, this gets our app running. We can also access the loaded services from `app.services`.

We will explore passing `options` to setup functions in the module via `theAppConfig` in
*Part 2* of this tutorial.


### Using es5 and es6 objects as services

#### es5 objects

modules/theModuleName/package.json
```
{
  ...
  plugin: {
    provides: [],
    consumes: []
  }
}
```

#### es6 classes

_todo_ 


#### using a promise in service setup function

_todo_ 


### Part 2 - Starting the application - loading all archiejs modules

_todo_ 


### Part 3 - TDD - Explore unit testing of archiejs modules

_todo_ 
