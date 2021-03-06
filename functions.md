Consider the following block of code:

```python
L = ['bubbles', 1, 1.3, "cats", "farmers", 'Yucutan', 9000, 'forest']

counter = 0
for item in L:
    if type(item) == str:
        counter += 1
print counter
```
First a variable equal to zero is instantiated before a _for_ loop.  The _for_ loop takes a list object "L" and iterates through it to check if an item is of type string.  If it is not of type string, the _if_ statememt is not entered.  If the _if_ statement is entered, a counter is increased by 1 for every item that is a string objecct.  After all objects have been iterated through, the number of string objects is printed via the variable "counter".  

This is a useful piece of code if you have a very large list, say thousands of items long, and you need to know how many string objects are in this list.  _The problem is that this code only works for the one list variable._  What if you had numerous lists that needed to be sorted through and specific items counted?  The code needs to be reusable and adaptable to any list situations.

### Defining a function

I now introduce one of the most useful components of programming -- the function.  A function is a reusable piece of code that takes an input, most commonly referred to as an _argument_ and utilizes that argument inside the function code block.  Generically here is what a function looks like:

```python
def functionName(agrument1, argument2, argument3):
	#do stuff with those arguments
	return something
```
To define a function you first begin with the _def_ statement.  The _def_ statement does just that it defines the function.  The second term defins the name of the function -- in this case functionName.  The function name is followed by open and close parenthesis.  Inside the parenthesis are the arguments that are _passed_ to the function -- that is the correct way to say it by the way.  One _passes an argument to the function_.  The definition line ends with a colon and the entire code block is tabbed once. At the end of a code block (typically) is the _return_ statement.  The _return_ statement returns something as you exit the code block.  Functions can _print_ or _return_ something depending on the needs of the function.  Functions could also do nothing, just execute the block of code. 

To understand more about function let's rebuild the above code block into a function.  Remember, in rebuilding the code block we want to make is resusable and extensible to any list object.

```python
def stringCounter(listObject):
	counter = 0
	for item in listObject:
	    if type(item) == str:
	        counter += 1
	return counter
```
We first defined our function as 'stringCounter' and pass an argument called 'listObject' to the function.  The first variable established in the function is the counter function.  

```python
L = ['bubbles', 1, 1.3, "cats", "farmers", 'Yucatan', 9000, 'forest']

stringCounter(L)
```

```python
print stringCounter(L)

numStrings = stringCounter(L)

print numStrings

print type(numStrings)
```


#### Side note:  Scoping

Assuming you have the above code block written starting with the defining of the 'stringCounter' and nothing else above it, run the following code:

```python 
print counter
```
Unless you have defined 'counter' outside the function 'stringCounter' you should have had this returned to you.

```python
NameError: name 'counter' is not defined
```
This is an important point to understand about Python and programming in general.  In terms of the variable 'counter' it only exists in side the function 'stringCounter' and it does not exist outside of it.  What is returned outside the function is an integer this is assigned inside the function to 'counter', so when the function exits all memory associated with the computation inside the function is dicarded and the result is returned.  This type of logic is referred to as __scoping__.  The variable 'counter' only exits inside the functions __scope__. 

Scoping tends to confuse beginners -- and for good reason.  It is by nature not confusing.  Take for instance the code below.  Can you guess what will print in the two print statements.

```python
anInt = 1

def addOne(anInt):
	anInt += 1
	return anInt 

print anInt

addOne(anInt)

print anInt
```
The first thing that may confuse you about this code is the fact that a variable 'anInt' is defined before the function is defined and then the argument anInt is passed to the function.  The first thing to note that that the variable and the argument have nothing to do with each other.  Arguments are only going to exit inside the function.  You could have named the variable 'Ralph' or even the argument that name.  The way I have thought of it is that the argument is just a placeholder for an object/variable that the function is going to use.

So, what did you get when you ran the code?  You should have printed 1 and then 1 again.  The function does not change the value of anInt.  It simply adds 1 to what every numerical value (int or float) that you give it and return that prints that.  

Scoping can get way more complicated, but that is the gist of it.  What happens in a function (Vegas) stays in a function. 

Another scoping examples:

```python
x = 7

def genX(someVariable):
	x = someVariable
	print x

genX(8)

print x

x = genX(x) + 10

print x
```
From these few lines of code can you determine what "x" is going to print?  At the start there is a function that defined "genX" that is passed the variable "someVariable".  This function will then set x equal to someVariable and print x. The important point is that all this happens in the genX function scope and does not change what is happening outside the function.  "x" is defined before the genX function is defined and called to create a new value of x but the implementation of genX does not change the original value of "x".  This is the most basic rule of scoping.   

Complex examples of scoping abound on the old interweb.  Just Google "scoping rules python" to see some.  But what I have found over the years is to just remember that what happens in a function (Vegas) stays in a function (Vegas).  In other words, variables created in functions remain within the scope of the function and do not enter the top level scope.  You can return the result of a function to a variable but this creates a new variable or overwrites an existing variable. 

#### Non-default and Default Function Arguments

There are two types of arguments that can be passed to functions- non-default and default arguments.   The difference between standard arguments and defalut arguments is that the later have a default input.  Non-default have to always be listed before arguments with default values.  Standard syntax for non-defalut and default arguments are as follows.

```python
def printArgs(arg1, arg2, arg3 = 10):
	print arg1, arg2, arg3

printArgs(1,2)

printArgs(1,2,3)
```

In the first case, arguments are only passed for the first two arguments.  Since 'arg3' has a defalut there is no need to enter a value unless you want the value to change.  

Non-defaults have to always come before default args and the two types of arguments cannot be mixed.  In other words, you cannot use the following syntax below.  

```python
def printArgs(arg1, arg3 = 10, arg2):
	print arg1, arg2, arg3
```
This will result in a syntax error ("SyntaxError") because default arguments are being presented before non-default arguments.  

#### Problem #1 - Counting words in a string:

Given the following string, your job is to parse this string into individual words and using the word as the keys you need to make the number of times each word appears at the value.  This means you have to interate through the string with each word and return the dictionary of words and their appearance value.  There is an obvious problem, there are some words that are going to be adjacent commas and periods that will not match the same word that do not sit next to a comma or period.  Do not worry about this for now.  Just focus on creating the dictionary with values.  

You can start off by writing the code outside of a function, but in the end it needs to wrap into a function.  
```
taleOfTwo = 'It was the best of times, it was the worst of times, it was the age of wisdom, it was the age of foolishness, it was the epoch of belief, it was the epoch of incredulity, it was the season of Light, it was the season of Darkness, it was the spring of hope, it was the winter of despair, we had everything before us, we had nothing before us, we were all going direct to Heaven, we were all going direct the other way – in short, the period was so far like the present period, that some of its noisiest authorities insisted on its being received, for good or for evil, in the superlative degree of comparison only.'
```
##### Problem #2 - Palindromes:

Develop a function or set of functions that takes a string input and determines if the input is a palindrome.  Think about this problem from a pseudocode perspective before moving forward -- in other words, don't just start writing code.  Think about all the problems that a user can introduce that can cause the function to fail.  Think about how you should break up the code into separate functions (this is called decomposition which we will talk more about later) -- because you probably don't want one function to do all the work because it is harder to debug.  Lay out a series of steps that need to be completed before you evaluate the palindrome.  Last is coming up with and algorithm that evaluate the string to determine if it is a palindrome.  


##### Problem #3:

Download the following link and parse the file to 