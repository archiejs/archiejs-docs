# ArchieJS - a dependency injection framework

ArchieJS is a dependency injection framework in NodeJS and is a fork of ArchitectJs (developed by C9) .

If you ever wanted to break your nodejs code into a loosely coupled modular structure, like below :-

```
project
  |
  +-- modules +-- module1
  .           | 
  .           +-- module2
  .           |
  .           ...  
  .   
  +-- dependency tree in a json
```

... you should read about Archiejs. This structure or architecture is also very popular in Java world.

Many organizations and enterprises have used similar architecture to create large manageable Nodejs projects. [ArchitectJs Presentation](http://www.slideshare.net/sergimansilla/architecting-large-nodejs-applications-14912706)

These modules are better containers for business logic than NPM modules. A section below covers these differences.

