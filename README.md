# Node-Gyp-Example

Example how to use node-gyp component compiling, for instance on Heroku.

## How does it work?
In `package.json` a script for the `install` event is defined.
This event is fired after the command `npm install`, which is used to install all the npm dependencies.
The script starts the node-gyp compiling, by providing (by convention) a `binding.gyp` file.

This works, for instance, on Heroku, because after a push to your master branch Heroku automatically performs a `npm install` call.
The nicety is that Heroku has a `gcc` compiler available, and thus your `c/c++` code can be compiled for their platform.
Using the same setup, you can compile your code for any platform and use it as a normal Node package with `require`.