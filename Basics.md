
## Project structure


ArchieJS has following main parts.


* /routes has all routes. New route files need to be added in /config/env/routes.js file.
* /controllers has all controller code.
* /models is the default models directory. New models are added to /models/package.json file (see how User.js is added).
* /test has mocha unit testcases.
* /plugins has logic blocks that can be arranged in pipelines, exposed as microservies, or written in other programming languages than javascript (such as go).
* /config directory has all initialization code and more.
** /config/plugins breaks up archie logical blocks (or plugins) into different services.
** /config/env has all config variables
** /config/init has various initialization libraries
** /config/archiejs does all orchestration in archiejs
** /config/archiejs/wrappers has various wrappers/decorators of plugins.
* /app.js is the file which launches different webapps and microservices.


## Plugins in archiejs


Plugins are independent modules that can do anything from sending a mail to running a machine learning algo. The most important thing about plugins is that :-


1. Plugins are polyglot (nodejs or go)
2. Plugins can be grouped together to form complex logic.
3. Wrappers can be applied to plugins, which can add some standard additional functionality to a plugin - such as make them independent microservers, etc.


## Wrappers in archiejs


Wrappers (or decorator patten) can be applied to plugins to enhance their functionality. For example, adding a kue-wrapper to a plugin makes it a microservice, which is called via redis-kue. You can easily add and register your own wrappers.

The are ployglots, and can be written in javasript/nodejs or Go. The plugins can be grouped together to form pipelines and complex logic.


