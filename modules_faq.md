# ArchieJs Modules - FAQ

### Q. How are Archiejs modules are different from npm modules?

Ans: Not very different - are an enhancement. 

Your business logic/services require some lifecycle management, which NPM modules 
dont provide out of the box. So we wrote a thin wrapper over NPM modules to make
them better for writing business logic. 

We added following :-

1. Support for lifecycle events of initialization and termination. 
2. Automatic depenency injection of modules into one-another based on `produce` and `consumes` tags
3. Enchance modules by specifying `enhancer` tag


### Q. How to write an Archiejs module?

_You will also need to read the next Q&A, `How to club archiejs modules in a dependency tree`?_

1. Create a directory for your module 
    
    ```
    $ mkdir -p modules/mymodule
    $ cd modules/mymodule
    $ npm init
    $ touch service1.js service2.js
    ```
    
2. Change the contents of `package.json` as follows. 
    
    Remove `main` from  package file.
    
    ```
    main: 'index.js',
    ```
    
    Instead add a `plugins` to package file.
    
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
    }
    ```
    
3. In file `service1.js`;
    
    we can use es5 classes
    
    ```
    module.exports = function setup(options, imports) {
     // return a promise (that returns this/object) or a simple function
    }
    
    setup.prototype.doSomething = function() {}
    ```
    
    or es6 classes
    
    ```
    class Service1 {
      constructor(options, imports) {
          // return a promise (that returns this/object) or a simple function
       }
    
       doSomething() {}
    }
    ```
    
Now we are ready to consume `Service1` and `Service2`, as we named them under `plugin.provides`.


### Q. How to establish are provide/consume relationship between Archiejs module?

_todo_


### Q. How to do TDD with archiejs modules?

_todo_


### Q. What are enhancers?

_todo_


### Q. How to apply enhancers to Archiejs modules?

_todo_

