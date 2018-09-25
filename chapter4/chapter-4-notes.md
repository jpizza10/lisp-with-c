# Build Your Own Lisp With C

## Chapter 4: An Interactive Prompt

### Read, Evaluate, Print (REPL)

An interactive prompt is a program that prompts the user for some input, the program will then use that input to reply to the user via some message appearing in the prompt.

##### REPL: Read Evaluate Print Loop
A common way to interact with a programming language.

Before creating a REPL, the first interactive program will start with a short interactive program that waits for some input from the user.

__**Definitions and Explanations**__

In C, the function __fgets__ is used to read input up until a new line (/n).

As this input is entered, it must be stored in a memory location. The input in this case will be stored in an constantly sized input buffer.

**Buffer** : temproary storage of data before the data is computed on via function. 

Once the input is stored it can be printed back to the user using __printf__ function.

In the code example, the buffer is defined as a static char. Variables defined as **static** in c are defined ousite of functions and are only visible within the file they are defined in, as is the case in the interactive prompt. THe use case for the global static variables is that they do not pollute the name space as they are not exported to other files.

However, a **static** variable defined within a function can be accessed across different invocations of the same code block. IF they are defined initialize, they are initialized only once. In this case, the static varaibles are usually initialzied to 0 by default. The variable is able to retain it's value between function calls.

**puts**
  Writes a string to stdout buffer up to but not including the null character (/0). A new line character is apppnded to the    output.

**fputs** 
  Stores the user input stream into the buffer. Appends a newline character to the buffer stream whereas puts does not.

**fgets**
  Accesses the user's input stream which has been stored in a buffer.
  
**stdin**
  Input that has been entered through the keyboard interface.

**stdout**
  Output that will appear on the users screen.
  
 #### Edit the input
 
 On Linux, using the arrow keys to move through the text to edit any values do not work. The arrow keys register as weight symbols such as ^[[D or ^[[C.]]
 
 To achieve this ability in the existing program, the library **editline** will be used which provide two fnctions **readline** and **add_history**.
 
 readline is used to read input from some prompt, but allows edits to that prompt. readline does not utilize a newline character so it must be manually added in the code. The function also stores the input by allocating new memory each time. It is freed by using the free( ) function.
 
 add_history lets the user record the history of the input so it can be retreived via the use of the up and down arrows.
 
 Had to install the libraries for editline also had to link to the library using the following line in the compiler call:
 
    cc -std=c99 -Wall prompt.c **-ledit** -o prompt
 
 #### The C Preprocessor
 
 C has a mechanism called the preprocessor that runs before the compiler is run. These specific preprocessor lines of coded are identified by an octothorpe or hash, #.
 
 Typically, these are sign in header file includes to allow the preprocessor to link the correct headrs and files before compiling the code.
 
 In this case, we have used the preprocessor to detect which operating system is being utilized by the user. Based on the OS seperate code will be run.
 
 To declare what code the compiler should emit it is wrapped in #ifdef, #else, and #end preprocessor statements. Essential an if statement but occur at preprocessor level. All contents from #ifdef to the first #else are used if the condition is true and all the contents from the #else to the final #endif are used if false.
 
 #### Bonus Marks
 
 * What does the "\n" mean in those strings?
  * \n is the escape character in c used to create a newline.
 * What other patterns can be used with printf?
  * %i or %d - signed decimal integer
  * %u - unsgned decimal integer
  * %o - unsigned octal
  * %x - unsigned hexadecmial integer
  * %X - unsigned hexadecimal integer (uppercase)
  * %f - decimal floating point, lowercase
  * %F - decimal floating point, uppercase
  * %e - scientifica notation, lowercase
  * %E - scientific notation, uppercase
  * %g - use the shortest representation: %e or %f
  * %G - use the shoretest representation : %E or %F
  * %a - heaxadecmial floating point, lowercase
  * %A - hexadecimal floating point, uppercase
  * %c - character
  * %s - string of characters
  * %n - nothing is printed
  * %% - a percent sign
  
* What happens when you pass printf a variable that does not match the pattern?
  * The program will not compile, giving an error that it expected a different type.
  
* What does the preprocessor command #ifndef do?
  * The #ifndef command executes the code after it if the token provided after #ifndef is defined or not, if it is not defined it will complete the code between it and the #else statement.
  
* What does the preprocessor command #define do?
  * #define will define any value before the code is compiled so that it may be registered in the compilation process and used in the program. Will allow the token to be defined in the preprocessor or allow a macro to be defined as well.
 
 Macro example
 
     #define MAX(a, b) ((a) > (b) ? (a) : (b))
     
     

* If _ WIN32 is defined on Windows, what is defined on Linux or MAc?
    * Linux and Mac utilize FreeBSD
 
