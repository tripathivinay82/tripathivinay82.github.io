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
		* You can slice sequences to create new sequences of the same type containing subsets of the original elements. 
		* Slice operations can modify mutable sequences—those that do not modify a sequence work identically for lists, tuples and strings.
		* Specifying a Slice with Starting and Ending Indices
			* The slice copies elements from the starting index to the left of the colon (2) up to, but not including, 
			the ending index to the right of the colon (6). The original list is not modified.
				```sh
				numbers = [2, 3, 5, 7, 11, 13, 17, 19]
				numbers[2:6]
				[5, 7, 11, 13]
				```
		* Specifying a Slice with Only an Ending Index:
			* If you omit the starting index, 0 is assumed. So, the slice numbers[:6] is equivalent to the slice numbers[0:6]
				```sh
				numbers[:6]
				[2, 3, 5, 7, 11, 13]
				numbers[0:6]
				[2, 3, 5, 7, 11, 13]
				```
		* Specifying a Slice with Only a Starting Index
			* If you omit the ending index, Python assumes the sequence’s length (8 here), so snippet [5]’s slice contains the 
			elements of numbers at indices 6 and 7:
				```sh
				numbers[6:]
				[17, 19]
				numbers[6:len(numbers)]
				[17, 19]
				```
		* Specifying a Slice with No Indices
			* Omitting both the start and end indices copies the entire sequence:
				```sh
				numbers[:]
				[2, 3, 5, 7, 11, 13, 17, 19]
				```
		* Slicing with Steps
			* The following code uses a step of 2 to create a slice with every other element of numbers:
			* We omitted the start and end indices, so 0 and len(numbers) are assumed, respectively.
				```sh
				 numbers[::2]
				 [2, 5, 11, 17]
				 ```
		* Slicing with Negative Indices and Steps
			* You can use a negative step to select slices in reverse order. The following code concisely creates a new list in reverse order:
				```sh
				numbers[::-1]
				[19, 17, 13, 11, 7, 5, 3, 2]
				```
			* This is equivalent to:
				```sh
				numbers[-1:-9:-1]
				[19, 17, 13, 11, 7, 5, 3, 2]
				```
		* Modifying Lists Via Slices
			* You can modify a list by assigning to a slice of it—the rest of the list is unchanged. 
			* The following code replaces numbers’ first three elements, leaving the rest unchanged:
				```sh
				numbers[0:3] = ['two', 'three', 'five']
				numbers
				['two', 'three', 'five', 7, 11, 13, 17, 19]
				```
			* The following deletes only the first three elements of numbers by assigning an empty list to the three-element slice:
				```sh
				numbers[0:3] = []
				numbers
				[7, 11, 13, 17, 19]
				```
	* DEL STATEMENT:
		* The del statement also can be used to remove elements from a list and to delete variables from the interactive session
		* Deleting the Element at a Specific List Index
			```sh
			numbers = list(range(0,   10))
			numbers
			[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
			del numbers[-1]
			numbers
			[0, 1, 2, 3, 4, 5, 6, 7, 8]
			```
		* Deleting a Slice from a List
			* The following deletes the list’s first two elements:
				```sh
				del numbers[0:2]
				numbers
				[2, 3, 4, 5, 6, 7, 8]
				```
	* PASSING LISTS TO FUNCTIONS:
		* Earlier we mentioned that all objects are passed by reference and demonstrated passing an immutable object as a function argument.
		* Here, we discuss references further by examining what happens when a program passes a mutable list object to a function.
		* Passing an Entire List to a Function
			* Consider the function modify_elements, which receives a reference to a list and multiplies each of the list’s element values by 2:
				```sh
				In [1]: def modify_elements(items):
				   ...:     """"Multiplies   all element values in items by 2."""
				   ...:     for i in range(len(items)):
				   ...:         items[i] *= 2
				   ...:
				In [2]: numbers = [10, 3, 7, 1, 9]
				In [3]: modify_elements(numbers)
				In [4]: numbers
				Out[4]: [20, 6, 14, 2, 18]
				```
			* Function modify_elements’ items parameter receives a reference to the original list, 
			so the statement in the loop’s suite modifies each element in the original list object.
		* Passing a Tuple to a Function
			* When you pass a tuple to a function, attempting to modify the tuple’s immutable elements results in a TypeError:
	
	* SORTING LISTS:
		* Sorting enables you to arrange data either in ascending or descending order.
		* Sorting a List in Ascending Order
			```sh
			In [1]: numbers = [10, 3, 7, 1, 9, 4, 2, 8, 5, 6]
			In [2]: numbers.sort()
			In [3]: numbers
			Out[3]: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
			```
		* Sorting a List in Descending Order
			```sh
			In [4]: numbers.sort(reverse=True)
			In [5]: numbers
			Out[5]: [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
			```
		* Built-In Function sorted
			* Built-in function sorted returns a new list containing the sorted elements of its argument sequence—the original sequence is unmodified. 
			The following code demonstrates function sorted for a list, a string and a tuple:
				```sh
				In [6]: numbers = [10, 3, 7, 1, 9, 4, 2, 8, 5, 6]
				In [7]: ascending_numbers = sorted(numbers)
				In [8]: ascending_numbers
				Out[8]: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
				In [9]: numbers
				Out[9]: [10, 3, 7, 1, 9, 4, 2, 8, 5, 6]
				In [10]: letters = 'fadgchjebi'
				In [11]: ascending_letters = sorted(letters)
				In [12]: ascending_letters
				Out[12]: ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
				In [13]: letters
				Out[13]: 'fadgchjebi'
				In [14]: colors = ('red', 'orange', 'yellow', 'green', 'blue')
				In [15]: ascending_colors = sorted(colors)
				In [16]: ascending_colors
				Out[16]: ['blue', 'green', 'orange', 'red', 'yellow']
				In [17]: colors
				Out[17]: ('red', 'orange', 'yellow', 'green', 'blue')
				```
	* SEARCHING SEQUENCES:
		* Often, you’ll want to determine whether a sequence (such as a list, tuple or string) contains a value that matches a particular key value. 
		* Searching is the process of locating a key.
		* List Method index
			* List method index takes as an argument a search key—the value to locate in the list—then searches through the list from index 0 
			and returns the index of the first element that matches the search key:
				```sh
				In [1]: numbers = [3, 7, 1, 4, 2, 8, 5, 6]
				In [2]: numbers.index(5)
				Out[2]: 6
				```
		* Specifying the Starting Index of a Search
			* Using method index’s optional arguments, you can search a subset of a list’s elements. 
			* You can use *= to multiply a sequence—that is, append a sequence to itself multiple times.
				```sh
				In [3]: numbers *= 2
				In [4]: numbers
				Out[4]: [3, 7, 1, 4, 2, 8, 5, 6, 3, 7, 1, 4, 2, 8, 5, 6]
				```
			* The following code searches the updated list for the value 5 starting from index 7 and continuing through the end of the list:
				```sh
				In [5]: numbers.index(5, 7)
				Out[5]: 14
				```
		* Specifying the Starting and Ending Indices of a Search
			* Specifying the starting and ending indices causes index to search from the starting index up to but not including the ending index location
				* numbers.index(5, 7)
		* Operators in and not in
			* Operator in tests whether its right operand’s iterable contains the left operand’s value:
				```sh
				In [7]: 1000 in numbers
				Out[7]: False
				In [8]: 5 in   numbers
				Out[8]: True
				```
			* operator not in tests whether its right operand’s iterable does not contain the left operand’s value:
				```sh
				In [9]: 1000 not in numbers
				Out[9]: True
				In [10]: 5 not in numbers
				Out[10]: False
				```
	* OTHER LIST METHODS:
		* Lists also have methods that add and remove elements.
			* color_names = ['orange', 'yellow', 'green']
		* Inserting an Element at a Specific List Index
			* Method insert adds a new item at a specified index. The following inserts 'red' at index 0:
				* color_names.insert(0, 'red') ==> ['red', 'orange', 'yellow', 'green']
		* Adding an Element to the End of a List
			* You can add a new item to the end of a list with method append:
				* color_names.append('blue') ==> ['red', 'orange', 'yellow', 'green', 'blue']
		* Adding All the Elements of a Sequence to the End of a List
			* Use list method extend to add all the elements of another sequence to the end of a list:
				* color_names.extend(['indigo', 'violet']) ==> ['red', 'orange', 'yellow', 'green', 'blue',   'indigo', 'violet']
			* This is the equivalent of using +=. 
		* Removing the First Occurrence of an Element in a List
			* color_names.remove('green') ==> ['red', 'orange', 'yellow', 'blue', 'indigo',   'violet']
		* Emptying a List
			* color_names.clear()
		* Reversing a List’s Elements
			* color_names = ['red', 'orange', 'yellow', 'green', 'blue']
			* color_names.reverse()
			* ['blue', 'green', 'yellow', 'orange', 'red']
		* Copying a List
			* copied_list = color_names.copy() ==> ['blue', 'green', 'yellow', 'orange', 'red']
	
	* LIST COMPREHENSIONS:
		* List comprehensions—a concise and convenient notation for creating new lists. 
		* List comprehensions can replace many for statements that iterate over existing sequences and create new lists
		* Mapping: Performing Operations in a List Comprehension’s Expression
			* A list comprehension’s expression can perform tasks, such as calculations, that map elements to new values (possibly of different types). 
			* Mapping is a common functional-style programming operation that produces a result with the same number of elements as 
			the original data being mapped. The following comprehension maps each value to its cube with the expression item ** 3:
				*  list3 = [item ** 3 for item in range(1, 6)] ==> list3 = [1, 8, 27, 64, 125]
		* Filtering: List Comprehensions with if Clauses
			* Another common functional-style programming operation is filtering elements to select only those that match a condition. 
			* This typically produces a list with fewer elements than the data being filtered. To do this in a list comprehension, use the if clause. 
			* The following includes in list4 only the even values produced by the for clause:
				* list4 = [item for item in range(1, 11) if item % 2 == 0] ==> list4 = [2, 4, 6, 8, 10]
				
	* GENERATOR EXPRESSIONS:
		* A generator expression is similar to a list comprehension, but creates an iterable generator object that produces values on demand. 
		* This is known as lazy evaluation. List comprehensions use greedy evaluation—they create lists immediately when you execute them. 
		* For large numbers of items, creating a list can take substantial memory and time. 
		* So generator expressions can reduce your program’s memory consumption and improve performance if the whole list is not needed at once.
		* Generator expressions have the same capabilities as list comprehensions, but you define them in parentheses instead of square brackets.
			```sh
			In [1]: numbers = [10, 3, 7, 1, 9, 4, 2, 8, 5, 6]
			In [2]: for value in (x ** 2 for x in numbers if x % 2 != 0):
			   ...:     print(value, end='  ')
			   ...:    
			9  49  1  81  25 
			```
		* To show that a generator expression does not create a list, let’s assign the preceding snippet’s generator expression to a variable and evaluate the variable:
			```sh
			In [3]: squares_of_odds = (x ** 2   for x in numbers if x % 2 != 0)
			In [3]: squares_of_odds
			Out[3]: <generator object <genexpr> at   0x1085e84c0>
			```
		* The text "generator object <genexpr>" indicates that square_of_odds is a generator object that was created from a generator expression (genexpr).
	
	* FILTER, MAP AND REDUCE:
		* Filtering a Sequence’s Values with the Built-In filter Function
			* Like data, Python functions are objects that you can assign to variables, pass to other functions and return from functions. 
			* Functions that receive other functions as arguments are a functional-style capability called higher-order functions. 
			* For example, filter’s first argument must be a function that receives one argument and returns True if the value should be included in the result. 
			* The function is_odd returns True if its argument is odd. 
			* The filter function calls is_odd once for each value in its second argument’s iterable (numbers). 
			* Higher-order functions may also return a function as a result.
			* Function filter returns an iterator, so filter’s results are not produced until you iterate through them. 
			* This is another example of lazy evaluation. In snippet [3], function list iterates through the results and creates a list containing them.
				```sh
				In [1]: numbers = [10, 3, 7, 1, 9, 4, 2, 8, 5, 6]
				In [2]: def is_odd(x):
				   ...:     """Returns   True only if x is odd."""
				   ...:     return x % 2 != 0
				   ...:
				In [3]: list(filter(is_odd, numbers))
				Out[3]: [3, 7, 1, 9, 5]
				```
		* Using a lambda Rather than a Function:
			* For simple functions like is_odd that return only a single expression’s value, you can use a lambda expression (or simply a lambda) 
			   to define the function inline where it’s needed—typically as it’s passed to another function:
			   	```sh
				list(filter(lambda x: x   % 2 != 0, numbers))
				[3, 7, 1, 9, 5]
				```
			* A lambda expression is an anonymous function—that is, a function without a name. In the filter call
				* filter(lambda x: x % 2 != 0, numbers)
			* the first argument is the lambda
				* lambda x: x % 2 != 0
			* A lambda begins with the lambda keyword followed by a comma-separated parameter list, a colon (:) and an expression. 
			* In this case, the parameter list has one parameter named x. A lambda implicitly returns its expression’s value. 
			* So any simple function of the form:
				* def function_name(parameter_list):
                		*     return expression
			* may be expressed as a more concise lambda of the form
				* lambda parameter_list: expression
		* Mapping a Sequence’s Values to New Values
			* Function map’s first argument is a function that receives one value and returns a new value—in this case, a lambda that squares its argument. 
			* The second argument is an iterable of values to map. Function map uses lazy evaluation. 
			* So, we pass to the list function the iterator that map returns. This enables us to iterate through and create a list of the mapped values. 
				```sh
				In [6]: numbers
				Out[6]: [10, 3, 7, 1, 9, 4, 2, 8, 5, 6]
				In [7]: list(map(lambda x: x ** 2, numbers))
				Out[7]: [100, 9, 49, 1, 81, 16, 4, 64, 25, 36]
				```
			* Here’s an equivalent list comprehension:
				* [item ** 2 for item in numbers] ==> [100, 9, 49, 1, 81, 16, 4, 64, 25, 36]

			

