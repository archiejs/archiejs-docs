# ArchieJS - writing modular code in nodejs

Archiejs enforces the tenets of modular design on nodejs codebases.

* Strong encapsulation
* Well defined interfaces
* Explicit dependencies 

Archiejs is also a nodejs dependency chaining framework. Its unique because your it allows breaking application logic into independent loosely coupled modules. The same also greatly increases reuse of modules across similar types of projects/sub-projects.

These modules are different from npm modules (actually are a thin layer of logic above npm's); one - they have a lifecycle (initialization and termination), and two - form dependency trees from an external JSON/JS file. These are more similar to npm modules that have peerDependencies specified between them. Also archiejs modules are also different from npm modules in below respects :-

1. dependency tree (pointing to of modules) resides outside of the code, 
2. configurations can be passed to modules in a standard manner, 
and 
3. all this makes it easier to assemble modules for writing comprehensive testcases (or mocking entire modules).

That said, when it comes to code, archiejs modules dont contain any proprietary APIs for registration or setup. All they need is an entry point or a setup function - where from they are injected into each other (without need for an explicit require).


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
  +-- dependency tree (to create app runtime)
```

you should read about Archiejs. This structure or architecture is also very popular in Java world.

You can find examples for a [module directory](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/tree/master/modules) and [dependency tree (see var `exports.app`)](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner/blob/master/deptree.js) in our demo app.


## Advantages recap

1. Loose coupling: Organizing nodejs project into small independent modules using dependency
   injection. The modules act like Java packages, where they make limited functionality 
   publicaly available.
2. Manage lifecycle of modules: Archiejs knows the dependencies between different modules in 
   the project and initializes them in the right sequence. (In the next versions, this can be 
   built on to manage lifecycle events of modules).
3. Better testing: Each module will have its own suite of testcases. Its easier to mock modules becuase
   service boundaries are better defined.
4. Better maintainablity: Each module can have its own versioning of npm modules. One archiejs module
   can use an older version of an npm module, while the newer written once use newer versions.
   (see section on differences with npm modules below)
5. Lesser boilerplate: Applying enhancers to modules and reduce boiler plate code. For example,
   we can can convert objects into db-tables or wrap them using microservices,
   using existing enhancers (see `demo-webapp-mongo-redis-ticket_booking`).
6. Reusablity: Because service boundaries are better defined, its easier to split a modular monolith
   into microserveces when the need arises; and also reuse the modules in different projects.
7. All your codebase is in one place. 

## Who should use it

* Will your project grow bigger and perhaps you would need to break it into microservices. Archiejs offers better handling of complex nodejs projects. [ArchitectJs presentation](http://www.slideshare.net/sergimansilla/architecting-large-nodejs-applications-14912706) is a good source for understanding the benefits of the architecture.

* Do you care about code reusablity across several client projects. Archiejs offers a better and consistent way to write business logic in isolated/reusable modules - with clear service boundaries.


## Demo apps

1. [Reciept scanner](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner) 
  A demo application which runs on terminal and scans the reciepts (using google cloud vision APIs). You could build an IoT device with a camera and modify this demo app to give it capabilities of a scanner.

2. [Ticket booking microservice](https://github.com/archiejs/demo-webapp-mongo-redis-ticket_booking) 
  A demo web application, which also demonstrates using `enhancers` (or decorators) to convert a module (named: `booking`) into a microservice (with redis pub-sub wrappers).


## Boilerplate

(THIS IS LIKELY TO BE BROKEN CURRENTLY - mail me and I will upload a new boilerplate or download it from here - https://bitbucket.org/navalsaini/dimagi_interview - will require minor changes)

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
