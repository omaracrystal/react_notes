#Webpack, ES6 and React Notes 

https://www.youtube.com/watch?v=MhkGQAoc7bc&list=PLoYCgNOIyGABj2GQSlDRjgvXtqfDxKm5b

##Webpack & browserify - 

##ES6 -

1. Destructuring 
	- adding variables straight to an array or object
	- set up default values too (if you are passing in several arguments - order doesn’t matter - less errors)
	- reference variable within an array just by naming the variable
2. Strings and Variables 
	- Back tick, single wrapper in order to add ``$(variable)`` and enters are equal to '\n '- a lot easier to create strings
3. Block scoping (similar to function scoping) 
	- **let** b = 2; > indicates something will be changed
	- **const** foo = 1 
		- pretty much the same as let - but it is immutable (cannot be changed), you can however change variables within the **const** object 
4. Classes
	```
		class Parent {

			contructor() {

			}

			static foo() {

			}

			bar() {

			}

		}

		class Child extends Parent {

			contructor() {
				super() // calls the contructor from Parent class
			}

			baz() {

			}

		}


		var child = new Child();
		child.foo(); // can't access since it's static
		child.bar(); // can access
	```
5. Arrow Functions
	- another way to define a function without actually writing "function"
	- similar to Coffee Script 
	- implicit returns (see below) - applies to one liners get's rid of brackets and return
	- lexical context binding (bind outside of immidiate 'this')

	```
		//before
		var foo = function(a,b) {
			return a + b;
		}

		//after (not too much different)
		var foo = (a, b) => {
			return a + b;
		}

		//most helpful when passing functions as arguments
		//implicit returns
		do.something((a, b) => ({ return a + b});
		do.something((a, b) => a + b);
		do.something(a => a++);
		[0,1,2].map(val => val++);

		//lexical context binding

		//before 
		var module = {
			age: 30,
			foo: function() {
				setTimeout(function() {
					console.log(this.age);
				}).bind(this), 100);
			}
		};

		module.foo();

		//after (arrow functions automatically binds 'this')
		var module = {
			age: 30,
			foo: function() {
				setTimeout(() => {
					console.log(this.age);
				}), 100);
			}
		};


	```
6. ES6 Modules
	- File 1 > require the module

	```
		var myModule = require("myModule");
	```

	- File 2 > define and export file of module

	```
		//before
		module.exports.foo = function() {

		}

		module.exports.bar = function() {

		}

		//after
		export function foo() {

		}

		export function bar() {

		}

		//or you can export and define something:
		export var foo = 3;

		//OR
		export default {
			//whole module if you want
		};
	```

	- File 3 > import this functions later in another file

	```
		//before
		import myModule from "myModule"; //at the top of file

		//after
		import { foo as foolish, //redifining the variable
				 bar } from "myModule";

		//or if you only want to import certain variables - usefule for libraries such as lodash 
		import { foo, bar } from "myModule"; //destructuring 

		import{ each, omit } from "lodash";
		omit(obj, "key");
	```

7. Generator Functions with Promises
	- traceur library
	- use with **Bluebird, co, q** libraries for promises
		- Bluebird = client side, browserside
			- you can yield variables, objects and arrays

			```

				Promise.coroutine(function* () {

					var tweets1 = yield $.get('tweets.json'); //yield variables

					//AND - OR
					var data = yield { //yield objects
						tweets: $.get('tweets.json'); 
						profile: $.get('profile.json');
					}

					//AND - OR 
					var [tweets, profile] = yield [
						$.get('tweets.json'), 
						$.get('profile.json')
					]

					console.log(data.tweets, data.profile);
					console.log(tweets1)
					console.log(tweets, profile)  //will wait until all above are successful before firing
				})

			```

		- co = node or backend
		- q = Angular
	- iterable function by using yield 
	- Async Functions > **async wait** syntax
		- returns one Promise
	```
		var myGen = function*() { // the * indicates a generator function
			var one = yield 1;
			var two = yield 2;
			var three = yeild 3;
			console.log(one, two, three); // console.log will be undefined, undefined, undefined
		}
		var gen = myGen();

		//how you run the gen funciton
		console.log(gen.next()); //{ value:1, done: false }
			//NOTE if you pass in a random agrument then the value of the that next variable will be redifined as such ie:
			console.log(gen.next(5)); // { value:5, done: false }
		console.log(gen.next()); //{ value:2, done: false }
		console.log(gen.next()); //{ value:3, done: false }
		console.log(gen.next()); //{ value:undefined, done: true }
		console.log(gen.next()); //errors because you can't call next() on a closed generator
	```

	- In you pass in a generator into a smarter function then it looks for promises (Looks like synchronous code - but it's actually asynchronous firing everything at once and then reading synchronously)

	```
		var myGen = function*() { // the * indicates a generator function
			var one = yield $.get('/api/friends');
			var two = yield $.get('/api/profile');
			var three = yield $.get('/api/tweets');
			console.log(one, two, three); // console.log will be undefined, undefined, undefined
		}
		var gen = myGen();

		//give me a generator
		function smartCode(generator) {

			//get the generator ready to run
			var gen = generator();

			//get my first yielded value
			var yieldedVal = gen.next();

			//if it's a promise, wait for it to fulfill and pass the value back into the generator
			if{(yieldedVal.then)} {
				//it's a promise!!!
				yieldedVal.then(gen.next);
			}


		}

	```


##React

- **Babel** - transpiler for Javascript code such as React JSX code and ES6
- **Webpack** - module bundler. Takes modules with dependencies and generates static assets representing those modules. As websites are evolving into web apps they are relying more and more on JavaScipt.
	- webpack-dev-server --content-base src (index.html will be route of load) > live load 
- everything is a component
	
- Render component as decorative tag > see folder basic-react
	```
		const app = document.getElementById('app'); 

		ReactDOM.render(<Layout/>, app); // this will render into index.html
	```
- 


