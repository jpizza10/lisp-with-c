# Languages - Chapter 5

## What is a programming language?

A programming language reflects a real language in that it is built upon structure and ruls that dictate what is valid oto say.

Utilization of these rules is used to generate our own speech, or code.

Linguist **Noam Chomsky** formalized a number of important observations about languages.
One of these was the observation that natural languages are built up of recursive and repeated substructures. 

For example, as long as the structure is followed i.e. noun doing an action, multiple nouns can be doing multiple actions and the sentence is still valid.

In C, this observation holds true as the body of an if statement contains a list of new statements of which one of the bodies of an if statement could contain an if statement.

These are called **re-write rules** because they tell us how one thing can be re-written as something else.

    > if (x > 5) {return x;}
    > if (x > 5) { if ( x > 10) { return x; } }

Chomsky's observation is important because it means that although there an infinite number of different things that can be said, or written down in a particular language, it is still possible to process and understand all of them with a finite number of re-write rules. These re-wrtie rules are what we call __**grammar**__.

Grammar in computer language must be extremely explicit and well defined for a computer to understand and define a language.

In creating our Lisp derivative a grammar must be created. To read input, a grammar must be define to determine if the input is valid. 

## Parser Combinators

mpc is the author's __Parser Combinator__ library that allows us to build programs that understand and process particular languages. These are known as parsers. Pareser Combinator library allows easy building of parsers, and allows us to only provide the grammar rules (sort of...).

mpc allows us to write normal code that looks just like grammar, whereas in some libraries code is written to specify grammar but indirectly.

## Coding Grammars
To create a langauge, caleld Doge, which has the following grammars:

* An adjective is either "wow", "many", "such", or "so".
* A Noun is either "lisp", "language", "c", "book", or "build"
* A Phrase is an Adjective followed by a Noun
* A Doge is zero or more phrases

To create a parser in mpc the type used is:

    mpc_parser_t*
To define the multiple options that define a type use:

    mpc_or

To put the definitions of adjective and noun using mpc:

    /*Build a parser 'Adjective' to recognize descriptions */
    
    mpc_parser_t* Adjective = mpc_or(4, mpc_sym("wow"), mpc_sym("such"), 
                                        mpc_sym("so"), mpc_sym("many")
                                     );
                                        
    /*Build a parser 'Noun' to recognize descriptions */
    
    mpc_parser_t* Noun = mpc_or(5, mpc_sym("lisp"), mpc_sym("langauge"), 
                                        mpc_sym("C"), mpc_sym("book"), mpc_sym("build")
                                );
    
To define that two or more things are required to define a type:

    mpc_and
    
    /* Parser for a 'Phrase' , combining an adjective and a noun */
    
    mpc_parser_t* Phrase = mpc_and(2, mpc_strfold, Adjective, Noun, free);

mpc_and also takes the arguments mpcf_strfold and free which we will come back to.

To define in the example Doge language, we must specify that zero or more of some paser is required. For this we need the function mpc_many, which requires the special variable to say how the resultes are joined together.

    mpc_parser_t* Doge = mpc_many(mpcg_strfold, Phrase);
    
    /*A Doge is many valid phrases pieced together*/
  
  Our Doge parser accepts inputs of any length. This means the language is __infinite__.
  
If we use more mpc functions the complexity of the langues can grow. THis complexity causes the readability of the grammar rules to become cumbersome and messy. Due to this, whole set of helper functions that build on simple constructs are defined by the language and able to be used for complicated langauges. 
  
## Natural Langauges

mpc lets us write grammars in a more natural form too, the grammar can be specified in one long string.

Here is how to recreate the Doge language using this method

    mpc_parser_t* Adjective = mpc_new("adjective");
    mpc_parser_t* Noun = mpc_new("noun");
    mpc_parser_t* Phrase = mpc_new("phrase);
    mpc_parser_t* Doge = mpc_new("doge);
    
    mpca_lang(MPCA_LANG_DEFAULT,
      "                                           \
       adjective : \"wow\" | \"such\"             \
                  | \"so\" | \"many\";            \
       noun      : \"lisp\" | \"langauge\" |      \
                  | \"book\" | \"build\" | \"c\"; \
       phrase    : <adjective> <noun>;            \
       doge      : <phrase>*;                     \
       ",
       Adjective, Noun, Phrase, Doge);
       
      /* Do Some parsing here...*/
      
      mpc_cleanup(4, Adjective, Noun, Phrase, Doge);
      

THe first argument mpca_lang are the options flages. For this we just use the defaults. THis is the grammar specifiaction and consists of a number of re-write rules.Each rule has a the name of the rule on the left, a colon :, and on the right the definition terminated with a semicolon ;.

Symbol | Rule
-------|-------
"ab"   | The string ab is required
'a'    | The character a is required
'a' 'b'| First 'a' is required then 'b' is required
'a' ( or symbol from C) 'b' | Either 'a' or 'b' is required
'a'*   | Zero or more 'a' required.
'a'+   | One or more 'a' required.
<abba>  | The rule abba is required.
    
## Bonus Marks

1. Write some more examples of strings the Doge langaugage contains.
    * Such language wow lisp many building, many language such lisp wow C
    
2. Why are there back slashes \ in front of the quote marks " in the grammar?
    * It is the escape quote character notification to let the compiler know that the character should be a " and not to interfere with     the string quote for the grammar definitions.
    
3. Why are there back slashes \ at the end of the line in the grammar?
    * This back slash has same function as mentioned in question 2 but this provides the closing quote for the identified grammar rule      with the string definitions.
    
4. Describe textually a grammar for decimal numbers such as 0.01 or 52.221?

       mpc_parser_t* Hundreds = mpc_new("hundreds");
       mpc_parser_t* Tens = mpc_new("tens");
       mpc_parser_t* Ones = mpc_new("ones");
       mpc_parser_t* DecimalPoint = mpc_new("decimalPoint");
       mpc_parser_t* Tenths = mpc_new("tenths");
       mpc_parser_t* Hundredths= mpc_new("hundredths");
       mpc_parser_t* Thousandths = mpc_new("thousandths");
   
       mpca_lang(MPCA_LANG_DEFAULT,
        "                                           \
        hundreds : \"1\" | \"2\" | \"3\" | \"4\" | \"5\" \
                   | \"6\" | \"7\" | \"8\" | \"9\" | \"10\"; \ 
        tens : \"1\" | \"2\" | \"3\" | \"4\" | \"5\" \
                   | \"6\" | \"7\" | \"8\" | \"9\" | \"10\" ; \
        ones : \"1\" | \"2\" | \"3\" | \"4\" | \"5\" \
                   | \"6\" | \"7\" | \"8\" | \"9\" | \"10\" ; \
        decimalPoint : \".\" ;
        tenths : \"1\" | \"2\" | \"3\" | \"4\" | \"5\" \
                   | \"6\" | \"7\" | \"8\" | \"9\" | \"10\" ; \
        hundredths : \"1\" | \"2\" | \"3\" | \"4\" | \"5\" \
                   | \"6\" | \"7\" | \"8\" | \"9\" | \"10\" ; \
        thousandths : \"1\" | \"2\" | \"3\" | \"4\" | \"5\"  \
                   | \"6\" | \"7\" | \"8\" | \"9\" | \"10\" ; \
        ",
        Hundreds, Tens, Ones, DecimalPoint, Tenths, Hundredths, Thousandths);
        
        /*Parsing...*/
        
        mpc_cleanup(7, Hundreds, Tens, Ones, DecimalPoint, Tenths, Hundredths, Thousandths);
        
5. Describe textually a grammar for web URLs such as http://www.buildyourownlisp.com

    Textually - > http://www. + domainName + domainExtension (ie .com, .org, .edu, .net...)
    
       <http extension> <domainName> <domainExtension>

6. Describe textually a grammar for simple English sentences such as **the cat sat on the mat**.

    Textually - > Article (the | a) + noun + verb + adverb + article+ noun
         <Article> <noun> <verb> <adverb> <article> <noun>
    
7. Describe more fomally the above grammars. Use |, /* or any symbols as needed. 
    Completed Above.

8. If you are familiar with JSON, textually describe a grammar for it.
    I am not familiar with JSON but am going to give it a shot.
  
    <attributeName> : <attributeValue>
    
