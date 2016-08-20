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

In this part of the tutorial, we will explore how we can create an X module with provides services X1 and X2. And also consumes a service Y1 (which is provided in another module Y).

### Multiple ways of writing Archiejs modules

There are multiple ways of creating archiejs modules. They are listed as below :-

| Module type                           | Name             | Provides             | Consumes             |
|---------------------------------------|------------------|----------------------|----------------------|
| One function module, one js file      | SimpleOneFunc    | | | |
| Single index.js file, one js file     | SimpleOneFile    | | | |
| es5 class module, many js files       | Es5Example       | | | |
| es6 class module, many js files       | Es6Example       | | | |


#### One function module

We will create a very simple module which does not provide or consume anything.

modules/doesNothing/index.js
```
module.exports = function setup(options, imports) {
  console.log('doesNothing initialized');
}
```
modules/doesNothing/package.json
```
{
  ...
  plugin: {
    provides: [],
    consumes: []
  }
}
```
./app.js
```
const archie = require('archiejs');
const theModules = [ 'modules/doesNothing' ];
const theDependencyTree = archie.resolveConfig(theModules);
archiejs.createApp(theDependencyTree, (err) => {...});
```



#### es5 classes

_todo_

#### es6 classes

_todo_ 

#### single index.js file

_todo_
