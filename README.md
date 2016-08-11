# ArchieJS - a dependency injection framework

ArchieJS is a dependency injection framework in NodeJS. It allows breaking up the code into modules and enforces developers to write code as a sum of isolated services. 

The modules in ArchieJS are very similar to NPM modules, except that a thin wrapper gives them some lifecycle events (such as initialization or termination) and they are injected into each other automatically (without a need for an explicit require). 

## History

It is derviced from ArchitectJs (developed by C9). It written with a goal to mordernize, simplify and build more capabilities into older ArchietectJs. We have added support for promises in module setup functions, improved error messages and made the code inside the library simpler (& about half in loc).

## Usecase

If you ever wanted to break your nodejs code into a loosely coupled modular structure (like below),

```
project
  |
  +-- modules +-- module1
  .           | 
  .           +-- module2
  .           |
  .           ...  
  .   
  +-- dependency tree
```

you should read about Archiejs. This structure or architecture is also very popular in Java world.

You can find examples for a [module directory](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/tree/master/modules) and [dependency tree (see var `exports.app`)](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/blob/master/deptree.js) in our demo app.

## Benefits

* Offers better handling of complex nodejs projects. [ArchitectJs presentation](http://www.slideshare.net/sergimansilla/architecting-large-nodejs-applications-14912706) is a good source for understanding the benefits of the architecture.
* Offers a way to write business logic in isolated modules - thin wrappers over NPM modules. Modules have a lifecycle and are initialized as per the dependency tree.



## Demo apps

1. [Reciept scanner](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner) 
  A demo application which runs on terminal and scans the reciepts (using google cloud vision APIs). You could build an IoT device with a camera and modify this demo app to give it capabilities of a scanner.

2. [Ticket booking microservice](https://github.com/archiejs/demo-webapp-mongo-redis-ticket_booking) 
  A demo application which demonstrates using `enhancers` (see below) to convert `booking` module into redis pub-sub microservice.


## Subtopics

1. [Modules](#tbd) or ArchieJs modules
  1. How are Archiejs modules are different from npm modules? (Ans: They are not, they are thin wrappers over the same.)
  2. How to write an Archiejs module?
  3. Enhancers and usecases?
3. [Description of repositories](#tbd)
4. [Boilerplate code generation](#tbd)
5. [General](#tbd)
  1. Benefits of depenency injection
  2. Other dependency injection frameworks in Nodejs
  3. Comparision with Architectjs
5. [Roadmap](#tbd)
  1. Serverless architectures
  2. Microservices architectures
  3. IoT applications


## Comments, questions and criticisms

Please send them to navalnovel at gmail dot com
