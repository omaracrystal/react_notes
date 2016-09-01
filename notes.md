#Webpack, ES6 and React Notes

##Webpack & browserify - 

##ES6 -

**Babele** - compiler for ES6 

1. Destructuring 
	- adding variables straight to an array or object
	- set up default values too (if you are passing in several arguments - order doesn’t matter - less errors)
	- reference variable within an array just by naming the variable
2. Strings and Variables 
	- Back tick ` single wrapper in order to add ``$(variable)`` and enters are equal to '\n '- a lot easier to create strings
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
	```

6. Generator Functions




