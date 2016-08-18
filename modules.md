# Coding with Archiejs

This is a tutorial about creating archiejs modules. The tutorial has below parts, where we will :-

Part 1. Explore creating a module using different semantics.
Part 2. Describle linking together the modules to create an application.
Part 3. Explore unit testing of archiejs modules.


## Part 1 - Different semantics of Archiejs modules

In this part of the tutorial, we will explore how we can create an X module with provides services X1 and X2. And also consumes a service Y1 (which is provided in another module Y).

### Modules in points

  * A module is container for one or many services, which the module `provides` to others. 
   * The services modules are are specified in `plugin.provides` key in `package.json` . This is usually the recommended technique.
   * A module with only one service to provide (and none to consume), can be just an `index.js` file with a `setup` function.
   * A module can also consume other services by specifing them in `consumes` tag in `package.json`.
  * A number of services inside modules are aggregated together as a list to run as an application.
   * If some service is consumed, but not provided, it will result in appropriate `error` and the application will not run.


### Multiple ways of writing Archiejs modules

There are multiple ways of creating archiejs modules. They are listed as below :-

  1. es5 classes
  2. es6 classes
  3. single index.js file

#### es5 classes

_todo_

#### es6 classes

_todo_ 

#### single index.js file

_todo_
