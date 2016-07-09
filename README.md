# Introduction 

* TODO * 

We are currently looking for reviewers and plan to create more documentation soon. For now, the boiler-XX code (or demo-XX code), has several README.md files in different directories, explaining the purpose of code organization and the files present in that directory. 


## Repositories for starters

1. demo-webapp-mongo-redis-ticket_booking

   An extensive demo application which demonstrates using archiejs to build web applications and use of
   kue and mongodb enhancers.

2. demo-basicapp-googlecloudvision-reciept-scanner

   A basic demo application which demonstrates chanining together modules in archiejs. 


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

