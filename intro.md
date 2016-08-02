# ArchieJS - a dependency injection framework

ArchieJS is a dependency injection framework in NodeJS and is a fork of ArchitectJs (developed by C9) .

If you ever wanted to break your nodejs code into a loosely coupled modular structure, like below :-

```
project
  |
  +-- modules +-- module1
  .           | 
  .           +-- module2
  .           |
  .           ...  
  .   
  +-- dependency tree in a json
```

... you should read about Archiejs. This structure or architecture is also very popular in Java world.

Many organizations and enterprises have used similar architecture to create large manageable Nodejs projects. [ArchitectJs presentation](http://www.slideshare.net/sergimansilla/architecting-large-nodejs-applications-14912706) is a good source for understanding the benefits of the architecture.

These modules are **better** containers for business logic than NPM modules. A section below covers these differences.

# Demo apps written with Archiejs

1. [Reciept scanner](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner) 
  A demo application which runs on the commandline and scans the reciepts using google cloud vision APIs.

2. [Ticket booking microservice](https://github.com/archiejs/demo-webapp-mongo-redis-ticket_booking) 
  A demo application which demonstrates using `enhancers` (see below) to convert `booking` module into redis pub-sub microservice.

# Sub-topics

1. [Modules](#tbd) or ArchieJs modules
  1. Archiejs modules are different from npm modules
  2. How to write an Archiejs module
3. [Description of repositories](#tbd)
4. [Boilerplate code generation](#tbd)
5. [Advanced concepts](#tbd)
   1. Enhancers
5. [Roadmap](#tbd)

# Comments, questions and criticisms

Please send them to navalnovel at gmail dot com
