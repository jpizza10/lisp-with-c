# Chapter 7 - Evaluation

## Trees

Up to this point in the book the capability to create a grammar and accept user input has been created. However, there is no current evaluation of the input in regards to the grammar. For instance, the program is able to consider whether input is valid or invalid but is unable to perform the function defined by the grammar.

Chapter 7 will define the code that will allow the evaluation of the input.

> ***Abstract Sytanx Tree*** : represents the structure of the program based on the input entered by the user. 

In the case of the Polish Notation grammar defined, the tree can looked at compartmentally as the following:

* At the leaves of three, is the data to be processed (i.e. operators, numbers)
* At the branches are the rules used to produce this part of the tree. The information on how to traverse and evaluate the data. In essence, the branch to take is determined by the rules generated.

To put this in context of our previous work that has been completed, let's tread deeper into the traversal process and its internal definition.

Inside of `mpc.h`, exists `mpc_ast_t`
