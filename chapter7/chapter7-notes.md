# Chapter 7 - Evaluation

## Trees

Up to this point in the book the capability to create a grammar and accept user input has been created. However, there is no current evaluation of the input in regards to the grammar. For instance, the program is able to consider whether input is valid or invalid but is unable to perform the function defined by the grammar.

Chapter 7 will define the code that will allow the evaluation of the input.

> ***Abstract Sytanx Tree*** : represents the structure of the program based on the input entered by the user. 

In the case of the Polish Notation grammar defined, the tree can looked at compartmentally as the following:

* At the leaves of three, is the data to be processed (i.e. operators, numbers)
* At the branches are the rules used to produce this part of the tree. The information on how to traverse and evaluate the data. In essence, the branch to take is determined by the rules generated.

To put this in context of our previous work that has been completed, let's tread deeper into the traversal process and its internal definition.

Inside of `mpc.h`, exists `mpc_ast_t` which is the following **struct** definition:

    typedef struct mpc_ast_t {
    char* tag;
    char* contents;
    mpc_state_t state;
    int children_num;
    struct mpc_ast_t** children;
    } mpc_ast_t;

The struct is defined by multiple fields:

1. `tag` 
  * type: `char*`
  * This is the information that preceded the contents of the node. It identified the rules used to parse the item. For example,        `expr|number|regex`
  * The tag field is important as it allows us to see the rules used to create a node.
2. `contents`
  * type: `char*`
  * Contain the actual contents of the node, the actual data, i.e. `5`, `'*'`, `'%'`
  * Empty for branches as there is no date, branches are a traversal object
3. `state`
   * type: `mpc_state_t`
   * The current state of the parser when it located the node, such as the line and colum number. 
   * Out of scope for our current program
4. `children_num`
   * type: `int`
   * Tells how many children for a node
5. `children`
   * type: `struct mpc_ast_t**` an array to store the children of the node
   * A double pointer type, to be explained in greater detail. From research, seem to add abstraction in C and allow for pointers to be     used to grow variables in complexity.

To access fields of an array square brackets are utilized and the indexing starts at 0 i.e. `children[0]` accessed the first child of the node.

To access fields for mpc_ast_t* since it is a pointer to a stuct, instead of using a `.` to access other struct fields we must use an arrow `->` there is no fundamental reason as to why but it is the case.

Example code snippet (retyped for understanding purposes)

    /* Load AST from output */
    mpc_ast_t* a = r.output;
    printf("Tag: %s\n", a->tag);
    printf("Contents: %s\n", a->contents);
    printf("Number of children: %i\n", a->children_num);
    
    /* Get First Child */
    mpc_ast_t* c0 = a -> children[0];
    printf("First Child Tag: %s\n", c0 -> tag);
    printf("First Child Contents: %s\n", c0 -> contents);
    printf("First Child Number of Children : %i\n", c0 -> children_num);
    
    
    
   
  
  
