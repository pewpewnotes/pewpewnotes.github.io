* ### Summary

* A statement is a type of instruction that causes the program to perform some action. Statements are often terminated by a semicolon.

* A function is a collection of statements that execute sequentially. Every C++ program must include a special function named main. When you run your program, execution starts at the top of the main function.

* The rules that govern how elements of the C++ language are constructed is called a syntax. A syntax error occurs when you violate the grammatical rules of the language.

* Comments allow the programmer to leave notes in the code. C++ supports two types of comments. Line comments start with a // and run to the end of the line. Block comments start with a /* and go to the paired */ symbol. Don’t nest comments.

* You can use comments to temporarily disable lines or sections of code. This is called commenting out your code.

* Data is any sequence of symbols that can be interpreted to mean something. A single piece of data, stored somewhere in memory is called a value.

* A variable is a named piece of memory that we can use to store values. A variable’s name is called an identifier. In order to create a variable, we use a statement called a definition statement. When the program is run, each defined variable is instantiated, which means it is assigned a memory address.

* A data type tells the compiler how to interpret a piece of data into a meaningful value. An integer is a number that can be written without a fractional component, such as 4, 27, 0, -2, or -12.

* Copy assignment (via operator=) can be used to assign an already created variable a value.

* Initialization can be used to give a variable a value at the point of creation. C++ supports 3 types of initialization:

* Copy initialization.
* Direct initialization (also called parenthesis initialization).
* Brace initialization (also called uniform initialization or list initialization).
* You should prefer brace initialization over the other initialization forms, and prefer initialization over assignment.

* Although you can define multiple variables in a single statement, it’s better to define and initialize each variable on its own line, in a separate statement.

* std::cout and operator<< allow us to output an expression to the console as text. std::endl outputs a new line character, forcing the console cursor to move to the next line. std::cin and operator>> allow us to get a value from the keyboard.

* A variable that has not been given a value is called an uninitialized variable. Trying to get the value of an uninitialized variable will result in undefined behavior, which can manifest in any number of ways.

* C++ reserves a set of names called keywords. These have special meaning within the language and may not be used as variable names.

* A literal constant is a fixed value inserted directly into the source code. Examples are 5 and “Hello world!”.

* An operation is a mathematical calculation involving zero or more input values, called operands. The specific operation to be performed is denoted by the provided operator. The result of an operation produces an output value.

* Unary operators take one operand. Binary operators take two operands, often called left and right. Ternary operators take three operands.

* An expression is a combination of literals, variables, operators, and function calls that are evaluated to produce a single output value. The calculation of this output value is called evaluation. The value produced is the result of the expression.

* An expression statement is an expression that has been turned into a statement by placing a semicolon at the end of the expression.

* Programming is hard, and your programs will rarely come out perfect (or close to it) the first time. Get your programs working first, then refine them into something great.
