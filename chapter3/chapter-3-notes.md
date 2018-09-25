# Build Your Own Lisp (Using C)

## Chapter 3

#### Programs
* A program written in C consists only of function definitions and structure definitions.
    * A C source file will contain functions and types. 
    * Functions are able to call other functions or can potentially call itself "recursion".
    * Functions can call external libraries using "include" files. This adds complexity to C.
    * A C program will always start with the execution of the **main** function written as `int main(void)`
    
    
#### Variables
* Variables are data that is named. i.e. `int tokens`, `char* first_name`
* Functions in C manipulate variables
* Every variable has an explicit type
  * The types are declared by the programmer or built into the language (i.e. built-in types).
* To declare a variable:
    * `int count;  /*Declaring the name of the variable (count) and its type (integer)`
    * `int count=10; /*If wanting to initialize the variable when declaring the variable, if the variable is not initialized it will         have a garbage value as it will point to an arbitrary value at a garbage memory address*/`

##### Variable Types
  
Type | Type Description | Example
-----|------------------|--------
void | Empty Type (Returns no value) | 
char | Single Character/Byte | `char last_initial = "P"`;
int  | Integer | int age = 62;
long | Integer that can hold larger values | `long age_of_universe = 13798000000`;
float| Decimal Number | `float mm_of_inch_worm = 2.23`;
double | Decimal Number with more precision | `double speed_of_sloth = 0.0107289`;

#### Function Declarations

A function is a computation that manipulates variables, and may change the overall state of a program.

In basic terms, a function recieves a variable as input and returns a variable as output after a computation is completed.

To **declare a function**:

1. Write the type of variable the function returns i.e. int, double, char*
2. The name of the function the programmer creates
3. In parenthesis a list of variables (parameters) it takes as input (if more than one, seperate by commas)
4. Body of the function is placed inside { }
  * Lists all of the statements the function executes, terminated by semicolons ;
5. Return statement provides the return value from the function and exits the function when return statement is  hit. Program returns to last place in main function.

_Example of a function declaration_

    int subtract_two_numbers(int x, int y) {
        if (x > y)
         {return x-y;}
         else {return y-x;}
     }
 
 Variables can also be initialized with the output of functions as well. 
 
 int subtracted = subtract_two_numbers(13, 10);

#### Structure Declarations

Structures are used to define new types that are not explicitly defined in the standard C language. Structures are seveal core variables mentioned in the above table together to define a new type.

To represent, complex data types that have multiple properties **structs** (structures) are used.

For example to create the properties of Downage in football we can define the following:

    typedef struct {
        int down;
        int distance;
    } downage
    
The type defined above is no different then the built-in types. To access individual fields, use a dot `.` followed by the name of the field

    /*Define a third down and 15 yards*/
    downage d;
    d.down=3;
    d.distance=15;
    
#### Pointers

A pointer is the same as a normal type that has an asterisk suffixed to the name. 

To declare a pointer to an int i.e. `int*`.

Pointers are used in C for strings or lists mostly.

Pointers ***point*** to the memory address of the variable and access the original variable ,where if not using a pointer there may user error since the manipulation is happening to a copy of the variable. Users may think they are falsey manipulating the actual variable and not the copy.

#### Strings

In C, strings are represented by `char*`. Inside, strings are stored as a list of characters in C, where the final character is the _null terminator_ `\0`. 

#### Conditionals

Conditional statements only perform code after the statement, if the statement's conditions are satisfied.

Examples of conditionals:
   * `if` `else`
   * `&&` (and)
   * `||` (or)
   
#### Loops

Loops allow code to be repeated until some condition is met causing the loop to be exited.

*While Loop*

Repeatedly executes a block of code until some condition becomes false.

    int i =5;
    while (i > 0) {
    puts("Loop Iteration");
    i = i - 1;
    }

*Do While Loop*

Will first execute the code and then check the condition to determine whether to execute more iterations of the code.

    i=3;
    do {
         puts("First iteration");
       }
    while (i<0);
    
 *For Loop*
 
 Requires three expressions seperated by semicolons (;):
 
 * The ***initalizer***, performed before the loop starts, initializes the variable
 * The ***condition***, checked during every iteration of the loop to check if the condition is true or false
 * The ***counter***, performed at the end of each loop can increment or decrement variable intialized in loop

 
 #### Bonus Marks
 
 * What built-in types are there other than the ones listed?
 
   * Long Double, an even more precise float
   * Long Long, very large int
   * Ints can also be unsigned or signed, signed integers can be positive or negative, unsigned are all positive values

* What other conditional operators are there other than the &gt; and &lt; ?
   * == (equal), != (not equal), && (and), || (or), >= (gt or equal to), <= (lt or equal to).

* What other mathematical operats are there other than add or subtact?
   * Multiplication (*)
   * Division (/)
   * Modulo (%)
   
* THe += operator will increment whatever variable it operates on by whatever value is pecified. 

* The do loop works by doing what is specified until a condition is met then exits. A do loop differs than a while loop because a do loop will execute an initial iteration first before checking the condition whereas a while loop will not execute until the condition is satisfied.

* The switch statement allows for the program to follow different cases on a path defined by the code executed when the case is met within the switchs statement.

* Break allows for the program to exit out of a function call and return to main.

* Continue allows the program to follow the path it was following after the code has run.

* typedef tells the compiler that a new type is being created for a struct. The type def lets the compiler know what th allows for a type to be defined by setting the variables that define the complex type inside.

