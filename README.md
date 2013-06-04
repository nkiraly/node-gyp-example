# Node-Gyp-Example

Example how to use [node-gyp](https://github.com/TooTallNate/node-gyp) addon compiling, for instance on Heroku.

## How does it work?
In `package.json` a script for the `install` event is defined.
This event is fired [after the command](https://npmjs.org/doc/scripts.html) `npm install`, which is used to install all the npm dependencies.
The script starts the node-gyp compiling, by providing (by convention) a `binding.gyp` file.

This works, for instance, on Heroku, because after a push to your master branch Heroku automatically performs a `npm install` call.
The nicety is that Heroku has a `gcc` compiler available, and thus your `c/c++` code can be compiled for their platform.
Using the same setup, you can compile your code for any platform and use it as a normal Node package with `require`.

## Where is my compiled object?
The node-gyp package compiles your binaries to `build/Release`.
You should put the `build` folder in `.gitignore`, unless you want to ship binaries (but then you won't need this approach...).

## How do I use the compiled object in my Node script?
You can just require it from the build location:`var myModule = require(./build/Release/MyModule);`.
See [hello.js](hello.js) for an example.