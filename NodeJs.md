# Fundamentals of Node
- The scripts or codes can be written and reused in 2 major ways . One of them is using the type commonjs which was the earlier one , the issue that was noted is that it would give many warnings and in order to prevent it in the next iterations with the launch of ES6 came the ES modules about which is written in the next major section
## What is Node.js
- It is a js runtime built on chromes ***v8 engine*** to run the ***javascript code outside the browser*** - on the servers , CLI's and desktop tools
- It is ***open source and cross-platform***
- It has ***event-driven , non-blocking I/O model***
- It is ***single threaded***
- It is ideal for ***scalable network applications and APIs***
- It powers ***CLIs servers , real-time apps , and build tools***
## Event Loop
A single threaded event loop delegates heavy work so it never block
```
Client Req -> Event Queue -> Event Loop -> Thread Pool / OS -> Callback/Response
```
## Core Built-in objects
- **`process`** : Info and control over the current node.js process - env variables , args , exit codes
- **`global** `: The top level namespace 
-  **`__dirname / __filename`** : absolute path of the current modules directory and file
- **`module / exports`** : Represents current module and what it shares with others
- **`buffer`** : handles raw binary data
- **`setTimeout / setInterval`** : Schedule work in event loop

# npm and Modules
- npm stands for Node Package Manager
- It **installs , updates and manages the packages a Node.js** project depends on . It ships bundled with Node.js and connects to the punlic npm registery
- Some of the mainly used npm commands
	- `npm init` : Create a new package.json
	- `npm install <pkg> ` or  `npm i <pkg>` : Used to add a dependency
	- `npm install -D <pkg>` or `npm i -D <pkg>` : Used to install a developer dependency
	- `npm run <script>` : Run a script for package.json
	- `npm update` : Updates the installed packages
	- `npm publish` : Publish a package to the repository
### Anatomy of package.json
```json
{
	"name" : "my-app",
	"version" : "1.0.0",
	"main" : "index.js",
	"scripts" : {
		"start" : "node index.js",
		"test" : "jest"
	},
	"dependencies" : {
		"express" : "^4.19.0"
	},
	"devDependencies" : {
		"nodemon" : "^3.1.0"
	}
}
```
- name / version : Gives the identity of the package
- main : Entry point of the project
- script : Create shortcuts that run with `npm run `
- dependencies : Needed at the runtime
- devDependencies : Needed only for development
### CommonJS vs ES modules
#### CommonJs
- It is the nodes original default module format (.js)
```javascript
const fs = require('fs');

function add(a , b){
	return a + b 
}

module.exports = { add };
```
- It gives 
	- Synchronous loading
	- Default in .js files
	- Widely supported in older tools
#### ES Modules
- These are the standard js modules - .mjs or "type" : "module" in package.json
```javascript
import fs from 'fs';

export function(a , b){
	return a + b;
}
```
- It is Asynchronous and has static loading
- Native browser and node support
- Enables tree shaking in bundlers

#### Creating and Using Modules
- The way its done using the commonjs method

```javascript
//Creating 
//math.js
function add(a , b){
	return a + b;
}
function multiply(a , b){
	return a * b;
}
module.exports = { add , multiply };

//Using 
//app.js
const { add , multiply } = require('./math')
console.log(add(4,3)) // Output : 7
console.log(multiply(2,3)) // Output : 6
```

# Debugging Techniques
- Its a method of identifying bugs and fixing them 
- Basic method is using console.log()
- Some of the methods are 
	- Console methods : log , error , warn , info ; also called trace levels
	- Debugger statement : Drop a breakpoint in code , pause execution when it attaches
	- node --inspect : Exposes a debugging protocol so external tools can attach to running process
	- Chrome DevTools : Full breakpoints , call stack , watch expressions via `chrome://inspect`
	- IDE Debugger : Integrated breakpoints , variable inspection and step through in the editor
	- Logging and tracing : Structured logs and stack traces for issues that obly show up in production
## node --inspect
- Start with inspector flag  
	Example : `node --inspect app.js`
- opens the inspect 
- set breakpoints
- step through execution
## Best Practices
- Use structured levelled logging instead of scattered console.log() calls
	Using console.warn() , console.info() etc
- Reproduce a bug with minimal , isolated test case
- Always handle promise rejections - catch async errors explicitly
- Watch for unhandledRejection and unhandledException events
- Use env specific config to avoid debugging prod-only issues
- Keep Source maps enabled when debugging transpiled or bundled code

# Additional Notes
- Http is stateless and the states are managed ussing sessions or session tokens
