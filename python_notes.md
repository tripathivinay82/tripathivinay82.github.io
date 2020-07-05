## Python: 

**Before you start:**
- Python is world's most popular prgramming language: 
    - https://pypl.github.io/PYPL.html
- Python Coding Guildelines:
  - https://www.python.org/dev/peps/pep-0008/
- Python Standard Libraries:
    - https://docs.python.org/3/library/index.html
    
**Python: Basics** 
- Variables:
  - variable name, such as x, is an identifier. Identified may consist of digit, letters and underscores but may 'not' begin with "digit". 
- Type:
  - Each value in python has a type that indicates the kind of data the value represents. 
    Ex: Type(x) => int : in this case x contains interger 

- Arthemtic Operator:
  -  The exponentiation (**) operator raises one value to the power of another:
  - True Division (/) vs. Floor Division (//):
    - True division (/) divides a numerator by a denominator and yields a floating-point number with a decimal point, as in:
       - 7 / 4 => 1.75
    - Floor division (//) divides a numerator by a denominator, yielding the highest integer that’s not greater than the result.
       - 7 // 4 => 1
    - Remainder Operator (%): yields the remainder after the left operand is divided by the right operand:
      - 17 % 5 => 2

- Print function:
  - using single or double quote produces same result
  - Keywod: 'end':
  	```
	for number in range(10, 0, -2):
       	    print(number, end=' ')
       
	o/p: 10 8 6 4 2
	```
  - keyword: 'sep'
  	```
	print(10, 20, 30, sep=', ')
	10, 20, 30
	```
- Docstrings:
  - three single or double quotes are used for stating script's purpose/documentation

- Objects:
  - Values such as 7 (an integer), 4.1 (a floating-point number) and 'dog' are all objects. Every object has a type and a value:
     -type(7) => int; type(4.1) => float; type('dog') => str
    
  - An object’s value is the data stored in the object. The snippets above show objects of built-in types int (for integers), 
    float (for floating-point numbers) and str (for strings).
    
  - Variables Refer to Objects: 
  
  	- Assigning an object to a variable binds (associates) that variable’s name to the object. As you’ve seen, 
	  you can then use the variable in your code to access the object’s value:
	  e.g: 	1) x = 7 => 7; 
	  	2) x + 10 => 17; 
		3) x => 7
	  After snippet step#1 assignment, the variable x refers to the integer object containing 7. 
	  As shown in snippet step#3, snippet step#2 does not change x’s value. You can change x as follows:
	  x = x + 10 => x = 17
	  
   - Dynamic Typing
   
    	Python uses 'dynamic typing' - it determines the type of the object a variable refers to while executing your code. 
	We can show this by rebinding the variable x to different objects and checking their types:
	e.g: 	4) type(x) => int
		5) x = 4.1 
		6) type(x) => float
		7) x = 'dog' 
		8) type(x) => str    

- Garbage Collection:

	Python creates objects in memory and removes them from memory as necessary. After snippet step#5, the variable x now refers to a float object. 
	The integer object from snippet step#3 is no longer bound to a variable. Python automatically removes such objects from memory. 
	This process—called garbage collection—helps ensure that memory is available for new objects you create.
	

- Build-in-functions:
    - min(36, 27, 12) => 12
    - max(36, 27, 12) => 36
    - decimal ( precise monetary calculations): 
    	https://docs.python.org/3.7/library/decimal.html
    - random (generate random numbers)
    - math (performing various common mathematical calculations)
    
    
 - Controls

    -  print(10, 20, 30, sep=', ') => 10, 20, 30
    
    -  Iterables, Lists and Iterators
	```sh
		total = 0
		for number in [2, -3, 0, 17, 9]:
		    total = total + number
		total
		25
	```
	
	The sequence to the right of the for statement’s in keyword must be an iterable—that is, an object from which the for statement can take 
	one item at a time until no more items remain. Python has other iterable sequence types besides strings. 
	One of the most common is a list, which is a comma-separated collection of items enclosed in square brackets ([ and ])
	Each sequence has an iterator. The for statement uses the iterator “behind the scenes” to get each consecutive item until there are no more to process. 
	The iterator is like a bookmark—it always knows where it is in the sequence, so it can return the next item when it’s called upon to do so. 

    - Augmented Assignment:
    
    	Abbreviate assignment expressions in which the same variable name appears on the left and right of the assignment’s =
	  e.g 	total = total + number => total += number 
	  	c += 7; d -= 4; e *= 5; f **= 3, etc
		
   - Break and Continue: 
   
       1) Executing a break statement in a while or for immediately exits that statement
       2) Executing a continue statement in a while or for loop skips the remainder of the loop’s suite

- Functions:


    - Custom Functions
  
		* function defination begins with keyword 'def' followed by name of the functions, a set of parentheses and a colon (:).
		* function name should begin with lowercase letter and in multiword names underscore should seperate each word
		* The required parentheses contain the function’s parameter list—a comma-separated list of parameters representing the data that the function needs to perform its task.
		*  If the parentheses are empty, the function does not use parameters to perform its task.

    - Custom Function’s Docstring:
    
		* the first line in a function’s block should be a docstring that briefly explains the function’s purpose:
			```sh
			 """Calculate the square of number."""
			 ```
		 
    - Returning a Result to a Function’s Caller:
  
		 * When a function finishes executing, it returns control to its caller—that is, the line of code that called the function.
		 * Example:  'return number ** 2'
			* first squares number, then terminates the function and gives the result back to the caller.
		 * Executing a return statement without an expression terminates the function and implicitly returns the value None (or False) to the caller.
		 * When there’s no return statement in a function, it implicitly returns the value None after executing the last statement in the function’s block.

    - Local and Global Scope:
     
		* A function’s parameters and variables defined in its block are all local variables—they can be used only inside the function and 
		exist only while the function is executing. Trying to access a local variable outside its function’s block causes a NameError, 
		indicating that the variable is not defined.
		
		* A local variable’s identifier has local scope. It’s “in scope” only from its definition to the end of the function’s block. 
		It “goes out of scope” when the function returns to its caller. So, a local variable can be used only inside the function that defines it.
		
		* Identifiers defined outside any function (or class) have global scope—these may include functions, variables and classes. 
		Variables with global scope are known as global variables. Identifiers with global scope can be used in a .py file or 
		interactive session anywhere after they’re defined.
		
		* By default, you cannot modify a global variable in a function—when you first assign a value to a variable in a function’s block, 
		  Python creates a new local variable
		* To modify a global variable in a function’s block, you must use a "global" statement to declare that the variable is defined in the global scope:
	 
		
    - Function Parameters:

		* default parameter value: 
			When calling the function, if you omit the argument for a parameter with a default parameter value, 
			the default value for that parameter is automatically passed
			e.g: def rectangle_area(length=2, width=3):
		* Keyword Arguments:
			* When calling functions, you can use keyword arguments to pass arguments in any order.
		* Arbitrary Argument List:
			* The parameter name args is used by convention, but you may use any identifier. 
			If the function has multiple parameters, the *args parameter must be the rightmost parameter.
			```
			def average(*args):
			    return sum(args) /   len(args)
			average(5, 10)
			7.5
			average(5, 10, 15)
			10.0
			```
		* Passing an Iterable’s Individual Elements as Function Arguments
			* You can unpack a tuple’s, list’s or other iterable’s elements to pass them as individual function arguments. 
			The * operator, when applied to an iterable argument in a function call, unpacks its elements. 
			The following code creates a five-element grades list, then uses the expression *grades to unpack its elements as average’s arguments:
			```
			grades = [88, 75, 96, 55, 83]
			average(*grades)   # this program calulates avergare of all numbers passed as argument
			79.4
			```
			The call shown above is equivalent to average(88, 75, 96, 55, 83).
		
		* METHODS: FUNCTIONS THAT BELONG TO OBJECTS
			* A method is simply a function that you call on an object using the form:  "object_name.method_name(arguments)"
			* For example, the following session creates the string variable s and assigns it the string object 'Hello'. 
			Then the session calls the object’s lower and upper methods, which produce new strings containing all-lowercase and 
			all-uppercase versions of the original string, leaving s unchanged:
			```
			1: s = 'Hello'
			2: s.lower() 
			  'hello'
			3: s.upper()
			  'HELLO'
			4: s
			  'Hello'	
			```
			
		
    
