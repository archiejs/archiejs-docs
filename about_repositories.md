# Description of repositories

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

