# Chapter 6 - Parsing

## Polish Notation

**Polish Notation** is notation of arithmetic where the operator comes before the operands.

For example:

    1 + 2 + 6 is + 1 2 6

Or:

    6 + (2 * 9) is + 6 ( * 2 9)

Or: 

    (10 * 2) / (4 + 2) is / (* 2 10) (+ 4 2)
    
This polish notation or prefx notation will be defined in mpc to create our own lisp. However, the grammar of this notation must first be created. 

Let's first start simple and define it in a textual manner using words and no lines of code.

For a start, the operator always comes first in an expression followed by either numbers or other expressions in parantheses. 

This means we can say a _**program**_ is an operator followed by one or more expressions.**

Where an _**expression**_ is either a number or in parantheses, an operator followed by one or more expressions.

> ***Program*** : the start of input, an ***Operator***, one or more ***Expression***, and the end of _input_.

> ***Expression*** : either a ***Number*** or '(', ***Operator***, one or more ***Expression***, and an ')'.

> ***Operator***: '+', '-', '\*\', or '/'.

> ***Number***: an optional - , and one or more characters between 0 and 9
    
## Regular Expressions

Looking at how to implement the textual description of the polish notation there a few things that have not been covered to this point:

*   Start of Input
*   End of Input
*   Optional Characters
*   Range of Characters

To implement the challenges thate have been identified Regular Expressions will be utilized. 

**Regular Expressions** are a way of writing grammars for small sections of the text such as words or numbers. Grammars written using regular expressions are unable to consist of multipl rules, but they do give precise and oncise control over what is matched and what isn't.

#### Basic Rules for Writing Regular Expressions

Regular Expression | Description
-------------------|------------
. | Any character is required.
a | The character 'a' is required.
\[\abcdef\]\ | Any character in the set abcdef is required.
\[\a-f\]\ | Any character in the range a to f is required.
a? | The character 'a' is optional.
a* | Zero or more of the character 'a' are required.
a+ | One or more of the charater 'a' are required.
^  | The start of input is required.
$  | The end of input is required.

In the mpc parser combinator library, the regular expressions are placed in between forward slashes.

i.e. /-?\[\0-9\]\+/

#### Installing mpc
