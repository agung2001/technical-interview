<iframe width="560" height="315" src="https://www.youtube.com/embed/SDROba_M42g" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## History
<iframe width="560" height="315" src="https://www.youtube.com/embed/Sh6lK57Cuk4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Modules
In JavaScript, there are three main module formats:

1. CommonJS (CJS): This is the default module format in Node.js. It uses the require function to import dependencies and the module.exports object to export values or functions from a module.
2. Universal Module Definition (UMD): This is a module format that is designed to work with a variety of module loaders, such as AMD, CommonJS, and global script tags. It uses a wrapper function to detect the environment and export the module in a way that is compatible with that environment.
3. ECMAScript (ES): This is a modern module format that is natively supported in modern browsers. It uses the import and export keywords to import and export values or functions from a module.

Here are a few key differences between these module formats:
- Importing dependencies: CJS uses the require function to import dependencies, while ES uses the import keyword. UMD can use either require or define (an AMD function) to import dependencies, depending on the environment.
- Exporting values or functions: CJS uses the module.exports object to export values or functions from a module, while ES uses the export keyword. UMD can use either module.exports or exports (a CJS object) to export values or functions, depending on the environment.
- Compatibility: CJS is natively supported in Node.js, but is not supported in the browser. UMD is designed to be compatible with a variety of environments, but can be more difficult to work with than CJS or ES. ES is natively supported in modern browsers, but may require a transpiler like Babel to be used in older environments.

## Concepts
- Building Blocks
	- [Event](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)
		- [[Event Loop]]
	- Functions
		- [[Arrow Function]]
		- [[Generator Function]]
		- [[High Order Function]]
			- filter()
			- map()
			- reduce
			- sort()
			- etc
- [[Map and Set]]
- Object
	- [Object Prototypes](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)
- [[Asynchronous]]
	- [[Async Await]]
	- [Promise](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Promises)
	- [Worker](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing_workers)
- Intermediete
	- [[Closure]]
- Extras
	- [[ECMAScript (ES)]]
	- [[Immediately Invoked Function Expression (IIFE)]]
	- [[Hoisting]]

## Tutorial
- [Developer Mozilla - Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- Modern Javascript
	- [JAVASCRIPT FRAMEWORKS - ( REACT PROJECT LIFECYCLE )](https://www.youtube.com/playlist?list=PLyQXlWxYAh8_S7YGeii9KPBSO85qD7-3W)

## Tricks
- [How to wait until an element exists?](https://stackoverflow.com/questions/5525071/how-to-wait-until-an-element-exists)

## Resources
- Design Pattern
	- [[Module Pattern]]
- Lint
	- [[Eslint]]
	- [[Javascript Standard Style]]
- [Official Website](https://www.javascript.com/)
- Unit Testing
	- [[Jest]]

## Contributor
- [[Muhammad Agung Sundoro]]