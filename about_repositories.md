# Description of repositories

The archiejs project currently has about 7 repositories (excluding this one). Below is a description of the repositories.

## Demo apps

1.  [Demo desktop app - basic](https://github.com/archiejs/demo-basicapp-googlecloudvision-reciept-scanner)
    
    A commandline app for converting scanned reciepts into text - using google cloud services. NOTE: setting up permissions on GCM should take 30 mins (or so) if you follow the steps.

2. [Demo web app - microservices](https://github.com/archiejs/demo-webapp-mongo-redis-ticket_booking)
    
    A demo webapp, where one of the module is loaded as a microservice. This also demos the use of enhancers.


## Tools and boilerplate

1. [Archiejs commandline generator](https://github.com/archiejs/generator-archiejs)

   A `yo` generator for archiejs.
   
2. [Boilerplate for webapp](https://github.com/archiejs/boiler-archiejs-express-mongo-redis)

   Boilerplate code for archiejs webapp - archiejs, express, mongo, redis.


## Repositories for core developers

1. [Archiejs core module](https://github.com/archiejs/archiejs)

   The core archiejs module.

2. [Archiejs kue enhancer](https://github.com/archiejs/archiejs-kue-enhancer)

   An enhancer which converts a module into a microservice accessible via redis pub-sub (kue).

3. [Archiejs mongodb enhancer](https://github.com/archiejs/archiejs-mongo-enhancer)

   An enhancer which converts db tables into archiejs services, so that other modules can
   specifiy their dependency on particular db tables in a more fine grained manner.

