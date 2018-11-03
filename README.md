<p align="center"><img src="https://image.ibb.co/mMyMQ0/NodeGard.png" height="128" alt="NodeGard"></p>
<h3 align="center">NodeGard</h3>
<p align="center"><i>My own Node.JS Framework / Boilerplate</i><p>



<p align="center">
  <a href="https://forthebadge.com">
    <img src="https://forthebadge.com/images/badges/made-with-javascript.svg"
         alt="Javascript">
  </a>
  <a href="https://forthebadge.com">
      <img src="https://forthebadge.com/images/badges/powered-by-water.svg">
  </a>
  <a href="https://paypal.me/Leafgard">
    <img src="https://img.shields.io/badge/$-donate-ff69b4.svg?maxAge=2592000&amp;style=for-the-badge">
  </a>
</p>

<p align="center">
  <a href="#key-features">Key Features</a> •
  <a href="#installation">Installation</a> •
  <a href="#usage">Usage</a> •
  <a href="#tests">Tests</a> •
  <a href="#contribution">Contribution</a> •
  <a href="#license">License</a>
</p>

## Key Features

* Ability to choose for single/multi-core application
* Works with separated modules
* Globally declared modules for inter-modules communication (Ex: WebServer -> Database)
* .ENV configuration ready
* Pre-installed ExpressJS webserver
* Loading, preparing and running phases
* Easy to adapt modules

## Installation

```bash
$ git clone https://github.com/Leafgard/NodeGard.git yourProjectName
```

### Update the `package.json`

Update the `package.json` with your own informations.

```diff
- "name": "nodegard",
+ "name": "yourpackagename",
  "version": "1.0.0",
- "description": "My own Node.JS Framework / Boilerplate",
+ "description": "Your package description",
  "main": "./src/app.js",
  "scripts": {
    "start": "node ./src/app.js",
    "test": "jest --detectOpenHandles --forceExit"
  },
  "repository": {
    "type": "git",
-   "url": "git+https://github.com/Leafgard/NodeGard.git"
+   "url": "git+https://github.com/yourName/yourRepository.git"
  },
- "author": "Yann SEGET <dev@leafgard.fr>",
+ "author": "Full NAME <yourName@mail.com>",
  "license": "MIT",
  "bugs": {
-   "url": "https://github.com/Leafgard/NodeGard/issues"
+   "url": "https://github.com/yourName/yourRepository/issues"
  },
- "homepage": "https://github.com/Leafgard/NodeGard#readme",
+ "homepage": "https://github.com/yourName/yourRepository#readme",
  "dependencies": {
    "dotenv": "^6.1.0",
    "express": "^4.16.4"
  },
  "devDependencies": {
    "jest": "^23.6.0"
  }
```

## Usage

### Configure the application in `config.js` file

#### Add a module to application:

By default, application is running with the built-in WebServer.

```js
/**
 * All the modules should be declared here.
 * NB: Application won't run if empty !
 * 
 * WebServer is here already declared.
 * It's the built-in webserver provided by the framework.
 */
  module.exports.Modules = {
    'WebServer': require('./src/Modules/WebServer')
  }
```

You just have to add your own modules like that:

```diff
  module.exports.Modules = {
-    'WebServer': require('./src/Modules/WebServer')
+    'WebServer': require('./src/Modules/WebServer'),
+    'myModule': require('./src/Modules/MyModule')
  }
```

`myModule` is the keyname to call in your whole application through all your modules.

For example, if you have a `Database` module and you want to call one of his function, you may just:

`Database.callMyFunction()` from anywhere in the app ! It will work !

`require('./src/Modules/..')` is the location to your module folder.

#### Single/Multi-Cores application

By default, application in running in single-core.

```js
/**
 * Ability to run on multiple cores or not:
 * true = Uses multiple cores
 * false = Uses only one core
 */
  module.exports.useMultipleCores = false
```

### Create a module

This framework is based on modules.

All your modules should be located at `./src/Modules/YourModule/index.js` (Each module has his own directory).

All modules should have this architecture:

```js
  module.exports = new ( class yourModule {

    /**
     * (Requires the packages and) Instanciate the main components and variables
     */
    constructor() {
      const express = require('express')
      this.app = express()
      this.webPort = process.env.WEB_PORT || 3000
      ...
    }

    /**
     * Prepares the module to be runned (Settings, routes, etc..)
     * @returns {Promise} Resolve = module prepared, reject = problem while preparing module
     */
    prepare() {
      return new Promise((resolve, reject) => {
        this.app.get('/', (req, res) => {
          res.send('Hello World!')
        })
        ...
        resolve()
      })
    }

    /**
     * Runs the module (Listening, etc..)
     */
    run() {
      this.app.listen(this.webPort, () => {
        console.log(`Example app listening on port ${this.webPort}!`)
      })
      ...
    }

  } )
```

You **absolutely** need the `prepare()` and `run()` functions, and the `prepare()` function should return a *Promise* !

If there is a problem during `prepare()`, return `reject`, else return `resolve`.

This *prevent* application to run without everything working.

## Tests

Create your tests (using JEST) in `./tests` and run:

```bash
$ npm test
```

## Contribution

* Fork the repository, use the development branch and please pull requests to contribute to this project.
* Follow the same coding style as used in the project. Pay attention to the
  usage of tabs, spaces, newlines and brackets. Try to copy the aesthetics the
  best you can.
* Write [good commit messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html),
  explain what your patch does, and why it is needed.
* Keep it simple: Any patch that changes a lot of code or is difficult to
  understand should be discussed before you put in the effort.

## Members

* **Yann SEGET** - *Main author* - *dev@leafgard.fr*

[https://github.com/Leafgard/NodeGard](https://github.com/Leafgard/NodeGard)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.