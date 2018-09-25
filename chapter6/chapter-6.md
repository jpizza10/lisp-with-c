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
    
