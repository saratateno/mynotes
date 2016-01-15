How to Set Up MEN
=================
* `brew update` and `brew install node`
* `npm update`
* Either:
  * `npm init` OR:
  * `$ npm install -g express-generator` and then `$ express myAppName`

Express generator is a package that can build the whole scaffolding for your project, a la `rspec-sinatra`. Using `npm init` will only generate the `package.json` file. It contains metadata about the program and the list of npm dependencies, which can also be grouped for development packages. It is similar to a Ruby `Gemfile` and specifies all the modules your app requires.

To add another `npm` module, use `$ npm install --save-dev [package name]` or `$ npm install --save [package name]` to install it locally, and run it again using the `-g` flag to install it globally. (Global install allows relevant commands to be run from the Command Line).

Some likely packages you will need are shown below.

```
"dependencies": {
  // these ones are added by express-generator:
    "body-parser": "~1.12.4",
    "cookie-parser": "~1.3.5",
    "debug": "~2.2.0",
    "express": "~4.12.4",
    "jade": "^1.11.0",
    "morgan": "~1.5.3",
    "serve-favicon": "~2.2.1"

  // these ones are for using MongoDB:
    "mongodb": "^1.4.40",
    "mongoose": "^4.3.5",
    "monk": "~1.0.1",
  },
  "devDependencies": {
    "grunt": "^0.4.5",
    "grunt-contrib-jshint": "^0.11.3",
    "grunt-contrib-watch": "^0.6.1",
    "grunt-webdriver": "^1.0.0",
    "chai": "^3.4.1",
    "mocha": "^2.3.4",
    "nodemon": "^1.8.1",
    "selenium-standalone": "^4.8.0",
    "webdriverio": "^3.4.0"
  }
```

* `$ npm install`

This is the same as running `bundle` in Ruby. It installs all of the package dependencies named in your `package.json`

* Install MongoDB

Use Homebrew (brew install mongodb).
Set up database..
https://docs.mongodb.org/manual/tutorial/install-mongodb-on-os-x/
`$ sudo mkdir -p /data/db`
`$ chown owmer-user /data/db`
`$ mongod` to fire up the DB server
`$ mongo` to access the Mongo shell (analogous to running `$ psql` for postgresDB)

Set Up for Testing
------------------
* Create `Gruntfile.js`

This is like Rake where you can set up tasks to run with a name space, a command, description etc using `registerTask`. (It is also possible to register multiple tasks in one line.) There are lots of grunt modules that can be installed. Useful ones are: `grunt-contrib-jshint`, `grunt-contrib-watch`, `grunt-webdriver`.

There is a configuration section (grunt.initConfig) where the options can be set for each task - follow the documentation for each of the packages to check the options.

The most likely default setting you'll need is:
  `grunt.registerTask('default', ['jshint', 'webdriver'])``

* Set up Webdriver by running `$ wdio config`

Follow the onscreen instructions. (>On my local machine, >Mocha framework, >spec reporter, >silent logging).

This creates the `wdio.conf.js` file which is similar to `spec_helper.rb`.

Change the default browser to be `chrome`.

In `Gruntfile.js` within ```grunt.initConfig``` add the following code, ensuring that ```configFile``` is set to the directory where your ```wdio.conf.js``` is located:

```
webdriver: {
 test: {
  configFile: './wdio.conf.js'
  }
 },
```

Also make sure you task is loaded by adding the following line to your Gruntfile:
``` grunt.loadNpmTasks('grunt-webdriver');```

If you have set up webdriver as a default Grunt task, you can run your tests by running `$ grunt`, otherwise `$ wdio wdio.conf.js`

Fire it All Up
--------------
* `$ selenium-standalone start` -> runs selenium server
* `$ npm start` (or `nodemon`) -> starts the server

What are all those packages?
----------------------------
* chai -> test assertions library
* mocha -> test driver
* mongoDB -> node driver for Mongo
* mongoose -> create schemas for your MongoDB (like DataMapper)
* nodemon -> allows you to keep your server running between file changes
* selenium -> allows your tests to drive the website (like when we did the Capybara click buttons exercise)
* webdriver.io -> equivalent to Capybara library?
