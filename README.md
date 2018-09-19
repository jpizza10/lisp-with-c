# Build Your Own Lisp (Using C)

## Chapter 3

#### Programs
* A program of C consist only of function definitions and structure definitions.
    * A C source file will contain functions and types. These functions can call other functions 
    or themselves.
    * Functions can call external libraries using "include" files and this external function calling allows for complexity in C.
    * A C program will always start with the execution of the **main** function. i.e. 
    int main(void).
    
    
#### Variables
* Variables are data that are named. i.e. int tokens, char* first_name
* Functions in C manipulate variables.
* Every variable has an explicit type
  * The types are declared by the programmer or built into the language.
* To declare a variable:
    * int count;  /*Declaring the name of the variable (count) and its type (integer)
    * int count=10; /*If wanting to initialize the variable when declaring the variable*/

##### Variable Types
  
Type | Type Description | Example
-----|------------------|--------
void | Empty Type (Returns no Value) | 
char | Single Character/Byte | char last_initial = "P";
int  | Integer | int age = 62;
long | Integer that can hold larger values | long age_of_universe = 13798000000;
float| Decimal Number | Float mm_of_inch_worm = 2.23mm;
double | Decimal Number with more precision | double speed_of_sloth = 0.0107289;

#### Function Declarations

A function is a computation that manipulates variables, and may change the overall state of a program.

In basic terms, a function recieves a variable as input and returns a variable as output afeter a computation is completed.

To **declare a function**:

* Write the type of variable the function returns
* The name of the function
* In parenthesis a list of variables it takes as input (if more than one seperate by commas).
* Body of the function are placed inside { }
  * Lists all of the statements the function executes, terminated by semicolons
* Return statement provides the return value from the function and exits the function when return statement is hi. Program returns to last place in main function.

_Example of a function declaration_

int subtract_two_numbers(int x, int y) {
 if (x > y)
 {
  return x-y;
 }
 else 
 {
 return y-x;
 }
 
 Variables can also be initialized with the output of functions as well. 
 
 int subtracted = subtract_two_numbers(13, 10);

