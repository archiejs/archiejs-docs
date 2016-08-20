# Coding with Archiejs

This is a tutorial about creating archiejs modules. The tutorial has below parts, where we will :-

* Part 1. Explore creating a module using different semantics.
* Part 2. Describle linking together the modules to create an application.
* Part 3. Explore unit testing of archiejs modules.


### Modules semantics in points

  * A module is container for one or many services, which the module `provides` to others. 
   * The services modules are are specified in `plugin.provides` key in `package.json`.
   * A module with only one service to provide (and none to consume), can be just an `index.js` file with a `setup` function.
   * A module can also consume other services by specifing them in `consumes` tag in `package.json`.
  * A number of services inside modules are aggregated together as a list to run as an application.
   * If some service is consumed, but not provided, it will result in appropriate `error` and the application will not run.


## Part 1 - Different semantics of Archiejs modules

There are multiple ways of creating archiejs modules. In below example, we will start with a very simple module (which does nothing and is composed in a single function) and move towards more complex examples. This might be lengthy, because its comprihensive. You may not need to read this word by word.


#### One function module - does nothhing

We will create a very simple module which does not provide or consume anything.

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

### Providing a service for other modules 

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

### A module with two services

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

### A module with two javascript files

We may want to spread services across multiple js files. Now, each js file can export a 
`setup` function. Note, how `package.json` changes.

modules/theTime/package.json
```
{
  ...
  plugin: {
    provides: {
      'earth.js': [ 'theTimeNow', 'isItLate' ],
      'space.js': 'theSpaceTimeNow'
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

### Consuming an Archiejs service inside a module

Modules consume services provided by other modules. (Note: sometimes we may 
confuse module name and the services it provides)


### Injecting other modules into theModule

Lets create a key with the timeNow and 

modules/theModuleName/package.json
```
{
  ...
  plugin: {
    consumes: []
  }
}
```

### An es6 example

### 

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

#### es5 classes

_todo_

#### es6 classes

_todo_ 

#### single index.js file

_todo_
