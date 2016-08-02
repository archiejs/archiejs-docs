# ArchieJS - a dependency injection framework

ArchieJS is a dependency injection framework in NodeJS.

It is derviced from ArchitectJs (developed by C9), and is written with a goal to mordernize and build more capabilities into it. We have added support for promises in module setup functions, improved error messages and made the code simpler/half in size.

# Usecase

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

You can find examples for a [module directory](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/tree/master/modules) and [depenency tree js](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/blob/master/deptree.js) in our demo app.

# Benefits

Many organizations and enterprises have used similar architectures for complex Nodejs projects. [ArchitectJs presentation](http://www.slideshare.net/sergimansilla/architecting-large-nodejs-applications-14912706) is a good source for understanding the benefits of the architecture.

These modules are **better** containers for business logic than NPM modules. 

These modules are has a lifecycle and are initialized as per the dependency tree.

These modules are more loosely coupled than if they were `require`d and kepts as js files in a directory. They are easier to maintain over the years, as some parts of the project are rewritten; while other parts are still legacy. 

# Demo apps

1. [Reciept scanner](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner) 
  A demo application which runs on the commandline and scans the reciepts using google cloud vision APIs.

2. [Ticket booking microservice](https://github.com/archiejs/demo-webapp-mongo-redis-ticket_booking) 
  A demo application which demonstrates using `enhancers` (see below) to convert `booking` module into redis pub-sub microservice.

# Subtopics

1. [Modules](#tbd) or ArchieJs modules
  1. How are Archiejs modules are different from npm modules?
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

# 

# Comments, questions and criticisms

Please send them to navalnovel at gmail dot com
