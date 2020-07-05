## Python: 

**Before you start:**
- Python is world's most popular prgramming language: 
    - https://pypl.github.io/PYPL.html
- Python Coding Guildelines:
  - https://www.python.org/dev/peps/pep-0008/

**Python Basics** 
- Variables:
  - variable name, such as x, is an identifier. Identified may consist of digit, letters and underscores but may 'not' begin with "digit". 
- Type:
  - Each value in python has a type that indicates the kind of data the value represents. 
    Ex: Type(x) => int : in this case x contains interger 

- Arthemtic Operator:
  -  **: The exponentiation (**) operator raises one value to the power of another:
  - True Division (/) vs. Floor Division (//):
    - True division (/) divides a numerator by a denominator and yields a floating-point number with a decimal point, as in:
      - 7 / 4 => 1.75
    - Floor division (//) divides a numerator by a denominator, yielding the highest integer that’s not greater than the result.
      - 7 // 4 => 1
    - Remainder Operator (%): yields the remainder after the left operand is divided by the right operand:
      - 17 % 5 => 2

- Print function:
  - using single or double quote produces same result
  
- docstrings:
  - three single or double quotes are used for stating script's purpose/documentation

- objects:
  - Values such as 7 (an integer), 4.1 (a floating-point number) and 'dog' are all objects. Every object has a type and a value:
    - type(7) => int; type(4.1) => float; type('dog') => str
    
    
    
    

### Steps to setup and start Telemetry using gRPC/SSL

``` sh
	- Generate the root/client(Ubuntu) and router/server certificate
	- Copy the router’s local certificate and root CA certificate to the router 
	- Configure the local certificate and CA profile on MX
	- Load the root CA certificate into the CA profile 
	- Configure the telemetry service 
	- Subscriber sensors from Client 
```
