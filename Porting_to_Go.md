# Integrating Go into ArchieJS code

Archiejs is a polyglot coding environment, where the HTTP layer is
primarily handled by NodeJs.

This document describes an analysis of porting/integrating go with
Archiejs.

We will get more implementation specific as we advance in the document.


## Goals of polyglot architecture

Below are the goals of the polyglot architecture.

* Different programming languages can call each other seamlessly
  * example, IDLs written in JSON
* Modules in different programming languages have similar structure.
  * Similarity in how modules are written/loaded/executed.
* Common code can be shared across implementation languages
  * example, Models and Validations


## Overview of Archiejs core module

This is an overview of Archiejs core module, what are the main
functionalities it provides on the node.js platform and how would
they translate into go.

The core node.js module for Archiejs does following things,

* Static dependency management of plugins
* Configuration management for plugins
* Wrappers for plugin to make them into different services
  * DB layers
  * Microservices (RPC)
  * (todo) IPC calls on same machine

In addition, Archiejs provides a way to write less cohesive code
for your business and application logic.


### Static dependency management of plugins

The dependencies are stored in json files. In future, we also expect this
to evolve into a package manager for microservices and supporting modules.

In case of nodejs, this does bridge a gap, that all dependencies are checked at
initialization time. If dependencies are not me, the code would not run, rather
than breaking in the runtime (as with require).

Here are the conflicting points :-

1. In case of go, the dependencies are by default managed by import(..) statement.
Go is a statically checked/compiled language, so we really dont have to worry
about checking the dependencies.
2. However, if we use provides/consumes with the go module, then js code will know
the services exported by the go module.

#### Planned solution

For the momenent we will go with 1. The solution would be to have 2 for autogeneration of js wrapper
logic on the client side. Also go code will need to be put in a different directory.

#### Future plans

We could implement a full provides/consumes logic in 'go' in future.


### Passing configurations to go module

In node.js plugins, the configuration options are passed via archiejs dependency manager to
the plugin. These configs are plugin specific.

Now in case of go, we can explore following options.

1. Go imports a module which helps it manage configuration. These config options would
not be plugin specific.
2. Go also has a plugin like structure.


### Wrappers for plugins

To be continued...
