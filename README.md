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
  +-- dependency tree (in json file)
```

you should read about Archiejs. This structure or architecture is also very popular in Java world.

You can find examples for a [module directory](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/tree/master/modules) and [dependency tree (see var `exports.app`)](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/blob/master/deptree.js) in our demo app.


## Benefits

* Offers better handling of complex nodejs projects. [ArchitectJs presentation](http://www.slideshare.net/sergimansilla/architecting-large-nodejs-applications-14912706) is a good source for understanding the benefits of the architecture.
* Offers a way to write business logic in isolated modules - thin wrappers over NPM modules. 
* Modules have a lifecycle and are initialized in proper sequence, as per the dependency injection tree.


## Demo apps

1. [Reciept scanner](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner) 
  A demo application which runs on terminal and scans the reciepts (using google cloud vision APIs). You could build an IoT device with a camera and modify this demo app to give it capabilities of a scanner.

2. [Ticket booking microservice](https://github.com/archiejs/demo-webapp-mongo-redis-ticket_booking) 
  A demo web application, which also demonstrates using `enhancers` (or decorators) to convert a module (named: `booking`) into a microservice (with redis pub-sub wrappers).


## Boilerplate

Install archiejs cli

```
npm install -g yo
npm install -g generator-archiejs
```

Create boilerplate code

```
yo archiejs project-name
```

## Quick read

1. [ArchieJs Modules FAQ](https://github.com/archiejs/archiejs-docs/blob/master/modules_faq.md)
  1. How are Archiejs modules are different from npm modules?
  2. A short gist on how to code an Archiejs module?
2. Enhancers (_todo_)
  1. What are enhancers?
  2. How can we create our own enhancers?
3. [Description of repositories](https://github.com/archiejs/archiejs-docs/blob/master/about_repositories.md)


## A detailed guide to archiejs (modules)

[Coding in Archiejs is explained here in detail](https://github.com/archiejs/archiejs-docs/blob/master/modules.md).
We cover :-

1. Different ways of coding archiejs modules
2. Linking (in runtime) them together to build node apps
3. Unit testing of modules
4. Version control of modules


## Roadmap 

Currently, I am interested in seeing feedback on Archiejs from various members of the open source community. The biggest advantage of this architecture is being able to write the code in isolated modules. It can be easily broken up into microservices, as in the web demo app.

Another feature on the roadmap, would be to introduce @provides and @consumes annotations directly in `js` files (outside of package.json).

It would also be interesting to see if `archiejs modules` can be seamlessly converted into serverless lamdas or if there are interesting usecases in IoT for archiejs depedency injection. 


## Comments, questions and criticisms

Please send them to navalnovel at gmail dot com
