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
			```sh
			1: s = 'Hello'
			2: s.lower() 
			  'hello'
			3: s.upper()
			  'HELLO'
			4: s
			  'Hello'	
			```

	- IMPORT:
		* Import Module: "import module_name" then accessed their features via each module’s name and a dot (.)
		* Import a specific identifier from a module (such as the decimal module’s Decimal type) with a statement like: "from module_name import identifier"
		   then used that identifier without having to precede it with the module name and a dot (.)
		* Importing Multiple Identifiers from a Module: from math import ceil, floor
			```sh
			from math import ceil, floor
			ceil(10.3)
			11
			floor(10.7)
			10
			```
		* You can import all identifiers defined in a module with a wildcard import of the form: "from modulename import *"
			* This makes all of the module’s identifiers available for use in your code. 
			* Importing a module’s identifiers with a wildcard import can lead to subtle errors—it’s considered a dangerous practice that you should avoid
		* Binding Names for Modules and Module Identifiers
			import numpy as np
		* Typically, when importing a module, you should use import or import as statements, then access the module through the module name or 
		the abbreviation following the as keyword, respectively. This ensures that you do not accidentally import an identifier that conflicts with one in your code.
	
	- PASSING ARGUMENTS TO FUNCTIONS:
		* In many programming languages, there are two ways to pass arguments—pass-by-value and pass-by-reference 
		  (sometimes called call-by-value and call-by-reference, respectively):
		* With pass-by-value, the called function receives a copy of the argument’s value and works exclusively with that copy. 
		   Changes to the function’s copy do not affect the original variable’s value in the caller.
		* With pass-by-reference, the called function can access the argument’s value in the caller directly and modify the value if it’s mutable.
		* Python arguments are always passed by reference. Some people call this pass-by-object-reference, because “everything in Python is an object.”
		* When a function call provides an argument, Python copies the argument object’s reference — not the object itself—into the corresponding parameter. 
		  This is important for performance. Functions often manipulate large objects— frequently copying them would 
		  consume large amounts of computer memory and significantly slow program performance.
		* You interact with an object via a reference, which behind the scenes is that object’s address (or location) in 
		   the computer’s memory—sometimes called a “pointer” in other languages. After an assignment like: x = 7
		   the variable x does not actually contain the value 7. Rather, it contains a reference to an object containing 7 stored elsewhere in memory. 
		   might say that x “points to” (that is, references) the object containing 7
		   ```sh
		   Variable   		Object
		   	            +-----------
		   |x|------------->|	  7	|
		   	            +-----------
		   ```         
		* Built-In Function id and Object Identities:
			* Let’s consider how we pass arguments to functions. First, let’s create the integer variable x mentioned above—shortly 
			  we’ll use x as a function argument: x = 7
			* Now x refers to (or “points to”) the integer object containing 7. No two separate objects can reside at the same address in memory, 
			 so every object in memory has a unique address. Though we can’t see an object’s address, we can use the built-in id function to 
			 obtain a unique int value which identifies only that object while it remains in memory
			 id(x) => 4350477840
			* The integer result of calling id is known as the object’s identity.4 No two objects in memory can have the same identity. 

- Sequences: List and Dict:

     - LIST []
     
     	* Lists are mutable -- their elements can be modified; string and tuple sequences are immutable—they cannot be modified
     	* Lists typically store homogeneous data, that is, values of the same data type
	* They also may store heterogeneous data, that is, data of many different types. 
	* List Length : len(list-name)
	* Accessing Elements from the End of the List with Negative Indices
		* list's last element, can be accessed with c[-1] and its first element with c[-5]; assuming list 'c' has 5 elements.
	* Appending to a List with:
		* a_list += [number]
		* When the left operand of += is a list, the right operand must be an iterable;
	* Concatenating Lists with +:
		* concatenated_list = list1 + list2
		```sh
		list1 = [10, 20, 30]
		list2 = [40, 50]
		concatenated_list = list1 + list2
		concatenated_list
		[10, 20, 30, 40, 50]
		```
	* Comparison Operators
		* You can compare entire lists element-by-element using comparison operators:
		```sh
		a = [1, 2, 3]
		b = [1, 2, 3]
		a == b
		True
		```
		
     - TUPLE ():
     
     	* tuples are immutable and typically store heterogeneous data, but the data can be homogeneous. 
	* A tuple’s length is its number of elements and cannot change during program execution.
	* Accessing Tuple Elements
		* A tuple’s elements, though related, are often of multiple types. Usually, you do not iterate over them. 
		  Rather, you access each individually. Like list indices, tuple indices start at 0
		  e.g: time_tuple = (9, 16, 1); time_tuple[0] => 9
	* Adding Items to a String or Tuple
		* As with lists, the += augmented assignment statement can be used with strings and tuples, even though they’re immutable.
			```sh
			1: tuple1 = (10, 20, 30)
			2: tuple2 = tuple1
			3: tuple2
			(10, 20, 30)
			```
		* Concatenating the tuple (40, 50) to tuple1 creates a new tuple, then assigns a reference to it to the variable 
		  tuple1—tuple2 still refers to the original tuple:
			```sh
			4: tuple1 += (40, 50)
			5: tuple1
			(10, 20, 30, 40, 50)
			6: tuple2:
			(10, 20, 30)
			```
		* Appending Tuples to Lists
			* You can use += to append a tuple to a list:
				```sh
				1: numbers = [1, 2, 3, 4, 5]
				2: numbers += (6, 7)
				3: numbers
				  [1, 2, 3, 4, 5, 6, 7]
				```
		* Tuples May Contain Mutable Objects
			```sh
			1: student_tuple = ('Amanda',   'Blue', [98, 75, 87])
			2: student_tuple[2][1] = 85
			3: student_tuple
			   ('Amanda', 'Blue', [98, 85, 87])
			```
			
     - UNPACKING SEQUENCES:
	
		* Swapping Values Via Packing and Unpacking
			```sh
			1:number1 = 99
			2:number2 = 22
			3:number1, number2 = (number2, number1)
			4:print(f'number1 = {number1}; number2 = {number2}')
			number1 = 22; number2 = 99
			```
		* Accessing Indices and Values Safely with Built-in Function "enumerate"
			* The preferred mechanism for accessing an element’s index and value is the built-in function enumerate.
			* This function receives an iterable and creates an iterator that, for each element, returns a tuple containing the element’s index and value. 
			* The following code uses the built-in function list to create a list containing enumerate’s results:
			```sh
			1:colors = ['red', 'orange', 'yellow']
			2:list(enumerate(colors))
			[(0, 'red'), (1, 'orange'), (2, 'yellow')]
			```
			* Similarly the built-in function tuple creates a tuple from a sequence:
			```sh
			3:tuple(enumerate(colors))
			4:((0, 'red'), (1, 'orange'), (2, 'yellow'))
			((0, 'red'), (1, 'orange'), (2, 'yellow'))
			```
			* The following for loop unpacks each tuple returned by enumerate into the variables index and value and displays them:
			```sh
			for index, value in enumerate(colors):
			print(f'{index}: {value}')    
			0: red
			1: orange
			2: yellow
			```
	*  SEQUENCE SLICING:
		* 


	
	
		
    
