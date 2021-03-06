+++
title = "Algos & Programming - Lecture 10"
author = ["eo shiru"]
date = 2018-11-09
lastmod = 2019-04-06T00:17:34+02:00
draft = false
+++

## Introduction {#introduction}

How does the compiler know whether a program is "correct" (in the sense of compilable) or not?
We basically distinguish between **grammar** and **semantics**.

**Grammar** (like we know it from school) consists of  _morphology_ (Formenlehre v Wörtern) and syntax (Sätze). In the realm of programming morphology practically doesn't matter therefore _grammar_ and _syntax_ are mostly used interchangeably.

The **semantics** (_meaning of a sentence_) do not matter to the compiler.


## Syntax {#syntax}

The **syntax** of a language is a _set of rules_ after which _expressions_ are built. This is true for natural languages like English and for formal languages likes C or Python, as well as mathematical logic or description languages etc.

Expressions in the above definition might be phrases, formulas are program/code statements.

Often times the better you understand the semantics the harder it gets to recognize the syntax (for example in my motherlanguage I don't think about the SPO-rule for subject-predicate-object at all).

Every formal language consists of **symbols/tokens**. A symbol is the **smallest** observable unit in a language (kleinste Einheit der Betrachtung innerhalb der Sprache). Symbols can be single tokens, combinations of such or whole words.

_Every finite, non-empty set \\(\sum\\) of symbols is called **alphabet**._

With the elements in \\(\sum\\) we can build **expression**. The "empty expression" is represented as \\(\epsilon\\)  (epsilon).

The set \\(\sum = {0,1,2,3,4,5,6,7,8,9}\\) for example is sufficient to build all natural numbers in the decimal system.

/The set of all strings(combinations) (Zeichenketten) the symbols from \\(\sum\\) can build is called **Kleene star** \\(\sum \*\\) of \\(\sum\\) (Kleenesche Hülle).

For example:
\\[ \sum = \\{a,b\\} \Rightarrow \sum \* = \\{\epsilon, a, b, aa, bb, ab, ba, aaa, aab, aba,baa, ...\\} \\]

The set of all strings without the empty string is represented as \\(sum +\\) Kleene Plus.

_Each subset \\(L \subseteq \sum\*\\) is also a **formal language**_.

In the following context we focus on formal languages and "languages" then refers to such.


## Formal languages and generative/formal grammar {#formal-languages-and-generative-formal-grammar}

How can the syntax of a language be described? Which expressions/strings in a language are valid and which aren't? An enumeration of valid expressions is usually unpractical because the quantity of expressions is often times enormously big or infinite.

A solution to this is to _describe_ how valid expressions can/may be **generated**. These "rules" are called **generative/formal grammar**. From wikipedia: "In formal language theory, a grammar (when the context is not given, often called a formal grammar for clarity) is a set of production rules for strings in a formal language. The rules describe how to form strings from the language's alphabet that are valid according to the language's syntax. A grammar does not describe the meaning of the strings or what can be done with them in whatever context—only their form."

For generative grammar of a language \\(L\\) a second alphabet \\(V\\) of variables is used in addition to the alphabet \\(\sum\\).

-   elements of \\(\sum\\) are called **terminal symbols**
    -   elementary symbols of a language
    -   cannot be replaced/reproduced via production rules
    -   eg: "for", "if"
-   elements of \\(V\\) are called **nonterminal symbols** (in some literature it is N instead of V)
    -   are reproducable/replacable via production rules

When speaking about those elements in an abstract way usually lower case letters (a,b,c..) are used for elements of \\(\sum\\) and uppercase letters for elements of \\(V\\).

A grammar is defined by production rules (or just 'productions') that specify which symbols may replace which other symbols; these rules may be used to generate strings, or to parse them. Each such rule has a head, or left-hand side, which consists of the string that may be replaced, and a body, or right-hand side, which consists of a string that may replace it. Rules are often written in the form head → body; e.g., the rule a → b specifies that a can be replaced by b.

To generate an expression we begin with a **start symbol** \\(S \in V\\).

Then depending on the nature of the rules \\(P\\) we distinguish between different kind of grammars (a regular grammar is a left or a right regular grammar):

-   a left regular grammar  is a formal grammar (V, Σ, P, S), such that all rules in P obey the forms:
    -   A → a - where A is a non-terminal in V and a is a terminal in Σ
    -   A → Ba - where A and B are in V and a is in Σ
    -   A → ε - where A is in N and ε is the empty string.
    -   so only **one nonterminal symbol** on the _left side_ and on the _right side_ **one terminal symbol** that _may be_ **preceeded** by _one nonterminal symbol max_
-   a **right regular grammar** is a formal grammar (V, Σ, P, S) such that all the production rules in P are of one of the following forms:
    -   B → a - where B is a non-terminal in V and a is a terminal in Σ
    -   B → aC - where B and C are non-terminals in V and a is in Σ
    -   B → ε - where B is in V and ε denotes the empty string, i.e. the string of length 0.
    -   so only **one nonterminal symbol** on the _left side_ and on the _right side_ **one terminal symbol** that _may be_ **followed** by _one nonterminal symbol max_

Types of grammars:

-   **regular grammar** (reguläre Grammatik) &rarr; either _all_ rules of P are of left regular grammar nature _or_ right regular grammar nature (not both/mixed)
-   **context-free grammar** (kontextfreie Grammatik) &rarr; a context-free grammar is a grammar in which the left-hand side of each production rule consists of _only a single nonterminal symbol_
-   **context-sensitive grammar** (kontextbehaftet/sensitive Grammatik) &rarr; a context-sensitive grammar is a formal grammar in which the left-hand sides and right-hand sides of any production rules may be surrounded by a context of **the same** terminal and nonterminal symbols `αAβ → αγβ`
-   **unrestricted grammar** (allgemeine Grammatik)

After the american linguist Noam Chomsky those grammars build the so called **Chomsky-Hierarchy** in which they're also called as:

-   **Type-0 grammars** &rarr; _unrestricted grammars_ (allgemeine Grammatiken)
-   **Type-1 grammars** &rarr; _context-sensitive grammars_
-   **Type-2 grammars** &rarr; _context-free grammars_
-   **Type-3 grammars** &rarr; _regular grammars_

Each n-1 grammar can "do everything and more" that a grammar of type n can do (a type 1 grammar can do everything a type 2 grammar can and so on; Grammatiken niedrigeren Typs sind erzeugungsmächtiger als die höherer Typen)


## Syntax Diagrams {#syntax-diagrams}

How may we describe the rules of grammars? For the following we limit us to (maximal) contrext free grammars. To describe grammar rules there exist two main approaches:

-   syntax diagrams
-   (extended) Backus-Naur form

<div style="color:red;">
  <div></div>

I was told that these were asked in last years exam

</div>

Syntax diagrams consist of of:

-   boxes with round corners &rarr; terminal symbols (lowercase, see above)
-   boxes with straight corners &rarr; nonterminal symbols (uppercase, see above)
-   connections via lines and arrows
-   each walkable way (in arrow direction) is valid a expression (Jeder (in Pfeilrichtung) begehbare Weg ist ein valider Ausdruck)

Components:
![](/knowledge-database/images/syntax-diagram-intro.png)

An example of a (simplified) function declaration in C in a syntax diagram:
![](/knowledge-database/images/syntax-diagram-func-decl.png)

Example of a syntax diagram for a while loop in python:
![](/knowledge-database/images/syntax-diagram-python.png)


## Backus-Naur Form {#backus-naur-form}

While syntax diagrams are easy to read, they're quite cumbersome and take a lot of space. A more compact alternative is the Backus-Naur form (BNF).

BNF uses meta symbols:

-   `::=` definition symbol
-   `|` alternative symbol
-   `< >` nonterminal brackets which convert any sequence of letters, digits and spaces into a nonterminal symbol

All symbols which are neither meta symbols nor nonterminalsymbols are terminal symbols.

BNF is directly translatable into context-free grammar, but needs (for example for loops) syntactic helper variables.

That's why there's also the Extended Backus-Naur form (EBNF) which is like BNF plus:

-   `[ ... ]` &rarr; description of **optional parts**
-   `{ ... }` &rarr; description of **repetitions**

There are also some syntactic differences:

-   arbitrary paren placement (Klammerung)
-   definition symbol is `=`
-   terminal symbols are wrapped in `""` or `''`
-   nonterminal symbols arent specially marked
    -   there also might be whitespaces in nonterminal symbol identifiers, the sequence is then separated via commas eg `signed integer = sign, integer`
-   expressions end with semicolons `;`
-   specific repetitions via `4 * (...)`
-   comments via `(* This is a comment*)`

A (E)BNF defintion or a syntax diagram is **complete** (vollständig) if a rule exist on the left side for every nonterminal symbol on the right hand rule side.


## Regular Grammar in Action {#regular-grammar-in-action}

Now we'll introduce **regular expressions** which are a compact notation for regular grammars.

String searching or pattern matching in (certain) files is such a common task that "tools" using regular expression exist to help with it (for example grep, sed, awk, perl, Python, C#.. provide ways to pattern match with regular expressions).

Since the 1980s, different syntaxes for writing regular expressions exist, one being the POSIX standard and another, widely used, being the Perl syntax.

Because there is only a limited amount of symbols/characters/tokens (Zeichen) available regular expressions differentiate between regular("normal") (terminal)symbols and meta characters, with a special meaning. Common but not all meta characters are:

-   `^` matches the starting position within the string
-   `.` dot wildcard matches any single character (newlines sometimes excluded tho)
-   `[ ]` a bracket expression matches a single character that is contained within the brackets eg `[abc]` matches "a", "b", or "c"
    -   `[^ ]` matches a single character that is _not_ contained within the brackets

= `$` matches the ending position of the string or the position just before a string-ending newline (in line-based tools, it matches the ending position of any line)

-   `*` matches the preceding element _zero or more_ times
-   `+` matches the preceding element _one or more_ times
-   `{n,m}` matches the preceding element at least `n` and not more than `m` times (eg `a{1,3}` matches only `a`, `aa` and `aaa`)
-   `\` escapes the previous meta character

There are also character classes which are the most basic regex concept after a literal match. It makes one small sequence of characters match a larget set of characters (eg in ASCII [a-z] for lowercase letters). Some examples of POSIX character classes:

-   `[:alpha:]` for alphabetic characters (A-Z, a-z)
-   `[:digit:]` for digits (0-9)
-   `[:alnum:]` for alphanumeric characters (A-Z,a-z,0-9)
-   `[:blank:]` for space and tab
-   `[:print:]` visible characters and the space character (printable characters)

Example usage of grep which finds all defintions of `time_t` in header files (option -E stands for extended-regexp):

```sh
grep −E "typedef ([_[:alpha:]][_[:alnum:]]*[[:blank:]]+)+time_t;" *.h # (copied from slides doesnt work for me :D)
```


## Compiler {#compiler}

A modern compiler uses multiple formal grammars for different purposes:

-    Lexical Analysis

    Lexical Analysis is the process of converting a sequence of characters (such as in a computer program or web page) into a sequence of tokens (strings with an assigned and thus identified meaning).

    Lexical analysis is the first phase of a compiler. It takes the modified source code from language preprocessors that are written in the form of sentences. The lexical analyzer breaks these syntaxes into a series of tokens, by removing any whitespace (in C, not in python because they belong to the syntax) or comments in the source code.

    If the lexical analyzer finds a token invalid, it generates an error. The lexical analyzer works closely with the syntax analyzer. It reads character streams from the source code, checks for legal tokens, and passes the data to the syntax analyzer when it demands.

    This is often done via a lexical specification that is defined using regular expressions.

-    Syntax Analysis

    Syntax analysis or parsing is the second phase of a compiler. We have seen that a lexical analyzer can identify tokens with the help of regular expressions and pattern rules. But a lexical analyzer cannot check the syntax of a given sentence due to the limitations of the regular expressions. Regular expressions cannot check balancing tokens, such as parenthesis. Therefore, this phase uses _context-free grammar_ (CFG), which is recognized by push-down automata.

    CFG, on the other hand, is a superset of Regular Grammar. This implies that every Regular Grammar is also context-free, but there exists some problems, which are beyond the scope of Regular Grammar. CFG is a helpful tool in describing the syntax of programming languages (take a look at [this](https://www.tutorialspoint.com/compiler%5Fdesign/compiler%5Fdesign%5Fsyntax%5Fanalysis.htm) resource which is pretty good and also has some more explanations for terminal symbols etc).

    A syntax analyzer or parser takes the input from a lexical analyzer in the form of token streams. The parser analyzes the source code (token stream) against the production rules to detect any errors in the code. The output of this phase is a parse tree.

    This way, the parser accomplishes two tasks, i.e., parsing the code, looking for errors and generating a parse tree as the output of the phase.

    Parsers are expected to parse the whole code even if some errors exist in the program.

    **Limitations of syntax analyzers**

    Syntax analyzers receive their inputs, in the form of tokens, from lexical analyzers. Lexical analyzers are responsible for the validity of a token supplied by the syntax analyzer. Syntax analyzers have the following drawbacks:

    -   it cannot determine if a token is valid
    -   it cannot determine if a token is declared before it is being used
    -   it cannot determine if a token is initialized before it is being used
    -   it cannot determine if an operation performed on a token type is valid or not

    These tasks are accomplished by the _semantic analyzer_

-    Semantic Analyzer

    A parser constructs parse trees as seen in the section about the parser / syntax analyzer above.

    The plain parse-tree constructed in that phase is generally of no use for a compiler, as it does not carry any information of how to evaluate the tree. The productions of context-free grammar, which makes the rules of the language, do not accommodate how to interpret them.

    Semantics of a language provide meaning to its constructs, like tokens and syntax structure. Semantics help interpret symbols, their types, and their relations with each other. Semantic analysis judges whether the syntax structure constructed in the source program derives any meaning or not.

    For example:

    ```java
    int a = "value";
    ```

    The code above should not issue an error in lexical and syntax analysis phase, as it is lexically and structurally correct, but it should generate a semantic error as the type of the assignment differs. These rules are set by the grammar of the language and evaluated in semantic analysis. The following tasks should be performed in semantic analysis:

    -   Scope resolution
    -   Type checking
    -   Array-bound checking

    From the lecture slides: "usually context-sensitive language is used to perform semantic analysis"


## Excourse: General Difference between Expressions and Statements {#excourse-general-difference-between-expressions-and-statements}

A statement is like an instruction that the runtime performs. Programs consist of statements. Without statements, there is nothing to do.

An expression is a piece of code that can be 'evaluated', meaning it can be reduced to a value.

The two concepts are not related, or even similar. They may coincide with the same piece of code, but they do very different things.

`x = 1` is not a statement. `'x = 1'` is an _expression_ that evaluates to 1, with the side effect of assigning the value 1 to x.

`x = 1;` is a _statement_ (note the semi-colon at the end) that performs this assignment.

In many languages (Java, C, JavaScript), it's easy to distinguish statements. Statements usually end with a semi-colon. Statements can't be evaluated, they just do something.

Expressions are harder to distinguish: The following statement consists of 9 expressions: `f[x] = 2*x+1;`

1.  `f` variable
2.  `x` variable
3.  `f[x]` binary postfix operation
4.  `2` literal
5.  `2*x` binary operation
6.  `1` literal
7.  `2*x+1` binary operation
8.  `f[x] = 2*x+1` assignment operation

In some languages there is no distinction between expressions and staments. In Lisp for example all code and data are written as expressions. When an expression is evaluated, it produces a value.

---

Sources: <https://www.tutorialspoint.com>
