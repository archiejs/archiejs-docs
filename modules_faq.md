# ArchieJs Modules - FAQ

### Q. How are Archiejs modules are different from npm modules?

Ans: Not very different - are an enhancement. 

Your business logic/services require some lifecycle management, which NPM modules 
dont provide out of the box. So we wrote a thin wrapper over NPM modules to make
them better for writing business logic. 

We added following :-

1. Support for lifecycle events of initialization and termination. 
2. Automatic depenency injection of modules into one-another based on `produce` and `consumes` tags
3. Enchance modules by specifying `enhancer` tag


### Q. How to write an Archiejs module?

_todo_


### Q. How to establish are provide/consume relationship between two Archiejs module?

_todo_


### Q. What are enhancers?

_todo_


### Q. How to apply enhancers to Archiejs modules?

_todo_
