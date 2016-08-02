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

Many organizations and enterprises have used similar architecture to create large manageable Nodejs projects. [ArchitectJs Presentation](http://www.slideshare.net/sergimansilla/architecting-large-nodejs-applications-14912706)

These modules are better containers for business logic than NPM modules. A section below covers these differences.

# Demo apps written with Archiejs

1. (https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner) [Reciept scanner]
  A demo application which runs on the commandline and scans the reciepts using google cloud vision APIs.

2. (https://github.com/archiejs/demo-webapp-mongo-redis-ticket_booking) [Ticket booking microservice]
  A demo application which demonstrates using `enhancers` (see below) to convert `booking` module into redis pub-sub microservice.


