# Introduction 

In future, it will have documents related to archiejs.


## Repositories for starters

1. demo-webapp-mongo-redis-ticket_booking

   An extensive demo application which demonstrates using archiejs to build web applications and use of
   kue and mongodb enhancers.

2. demo-basicapp-googlecloudvision-reciept-scanner

   A basic demo application which demonstrates chanining together modules in archiejs. 


## Tools and boilerplate

1. generator-archiejs (currently broken - needs repair)

   A generator for archiejs.

Todo add boiler plate code repos for basic and webapps.


## Repositories for core developers

1. archiejs

   The core archiejs module.

2. archiejs-kue-enhancer

   An enhancer which converts a module into a microservice accessible via redis pub-sub (kue).

3. archiejs-mongodb-enhancer

   An enhancer which converts db tables into archiejs services, so that other modules can
   specifiy their dependency on particular db tables in a more fine grained manner.

