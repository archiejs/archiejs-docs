# Introduction

ArchieJS is a nodejs dependency injection framework, which allows you to break your nodejs project into loosely coupled modules, that are injected into each other during application startup. Archiejs is specially useful for managing large nodejs projects.

## Modules are loosely coupled

Modules clearly define their boundaries, have their own test-suits, npm modules, configs, etc and this makes them more maintainable and reusable across the lifecycle of the project.

## Modules are different from npm modules

The difference with npm modules is that archiejs modules are a place for your business logic. They have interdependencies (provide and consume relationships) with other archiejs modules, which are specified in their package.json files (using a new plugin keyword) and in a project wide js or json (which reads the dependency tree).

Modules (ArchieJS) can have a lifecycle (ex. modules are initialized in the right sequence when your application starts). If one of the modules is missing, a flag is raised even before the application starts running. Modules are also like java packages in some regards - ie. they expose some specific functions, while hide the others.

## Enhancers for modules

Enhancers are wrappers over archiejs modules.

Enhancers is a not entirely a new concept. Enhancers are to Archiejs modules; what libraries like Promisify is to a function (ie. add wrappers over functions).

We have used them in following ways :-

* Wrap modules such that they can be seamlessly called over redis-pub sub (like making normal function calls)
* Integrate mongodb schema files as archiejs services in a cleaner fashion

## Demo apps

1.  https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner
    
    A demo desktop app (which uses google apis). 
    NOTE: I have attached a file with my google credentials (and private key) to the mail; so that you dont have to go into the trouble of creating your own to try the project (i will keep them alive for next few days).

2. https://github.com/archiejs/demo-webapp-mongo-redis-ticket_booking
    
    A demo webapp


## Tools and boilerplate

1. generator-archiejs (currently broken - needs repair)

   A generator for archiejs.
   
2. boiler boiler-archiejs-express-mongo-redis
   
   Boilerplate code for archiejs webapp.


## Repositories for core developers

1. archiejs

   The core archiejs module.

2. archiejs-kue-enhancer

   An enhancer which converts a module into a microservice accessible via redis pub-sub (kue).

3. archiejs-mongodb-enhancer

   An enhancer which converts db tables into archiejs services, so that other modules can
   specifiy their dependency on particular db tables in a more fine grained manner.

