---
title: Comp Notes
permalink: /comp_notes/
---

## Log
* 2/21/2021: upgraded laptop to Big Sur. Downloaded Atom editor.
* 2/22/2021: downloaded Command Line Tools for Mac OS v. 12.4 and was able to get "Hello World" working in Atom and cmdline using clang. Appropriate because it has been exactly 43 years and 1 day since K&R pubished this, per [Daring Fireball](https://daringfireball.net/linked/2021/02/23/hello-world) and [CSAIL at MIT](https://twitter.com/MIT_CSAIL/status/1363875135191678984).
* 2/24/2021
	* Started new paper notebook
	* Redrew Thain Chapter 2 diagram [**Figure 2.1 – Typical Toolchain**](https://www3.nd.edu/~dthain/compilerbook/chapter2.pdf): Preprocessor &#8594; Compiler &#8594; Assembler &#8594; Static Linker &#8594; Dynamic Linker.
	* Redrew [**Fig 2.2 – Stages of a Typical Unix Compiler**](https://www3.nd.edu/~dthain/compilerbook/chapter2.pdf): Scanner &#8594; Parser &#8594; *AST* &#8594; Semantic Routines &#8594; Multiple rounds of Optimizers &#8594; Code Generator &#8594; *Assembly.s output* 
	* Experimented with clang to output AST per [these  instructions](https://bastian.rieck.me/blog/posts/2015/baby_steps_libclang_ast/)
	* **cpp** is a confusingly overloaded term. 
		* First, it may refer to the first part of the gcc tool chain which is the *cpp* **C P**re**P**rocessor. 
		* Secondly,  the .cpp in *foo.cpp* is the file extension for C++ source files. E.g., "hello.cpp" compiles to a C++ executable that runs the "hello.o" object code.
	* Per Figure 2.1 (see JH notes Comp #1, 2/22/2021), the gcc compiler is also called cc1 per this [Stack Overflow article](https://stackoverflow.com/questions/63561353/is-gcc-a-compiler-or-is-it-a-collection-of-tools-for-the-compilation-process).
* 2/25/2021 - Grammar G1, p. 8
	1. **Addition:** expression &#8592; expr + expr 
	1. **Multiplication:** expression &#8592; expr * expr
	1. **Assignment:** expression &#8592; expr = expr
	1. **Call a function:** expression &#8592; id ( expr )
	1. **Parentheses:** expression &#8592; (expr)
	1. **An identifier is an atomic expression:** expression &#8592; id
	1. **An integer is an atomic expression:** expression &#8592; int
* 2/26/2021 – moved exercise files to ~/df/jeff_c_lang_exercises
* 2/27/2021 – Started Purple Dragon Book. read about Java etc.
* 2/28/2021 – copied test_scanner.c out into jeff_c_lang_exercises. Started Section 3.3 on Regular Expressions.
* 3/01: Created page for the [Purple Dragon book](/aho-lam-2e/). 
* 3/03: Drew various illustrated versions of Figure 1.6 (Aho p. 5).
* 3/04: Further reading of Lexical and Syntax Analysis in Aho.
* 3/05: Drew further more refined versions of Figure 1.6 (Aho p. 5).
* 3/06: Started [K&R](/kr-88) book, successfully completed several [Edit-Compile-Run](https://wiki.c2.com/?EditCompileLinkRun) iterations for temperature conversion programs through end of p. 14.
* 3/07 - 3/10: Worked through most of Chapter 1 of K&R.
* 3/11: Started [K.N. King book](/knk-2008/); successfully compiled and ran first program from KNK p. 23.
* 3/13: Wrote additional KNK programs.
* 3/14: More KNK programs.
* 3/15: Redrew Phases of Compiler, Figure 1.6 (Aho p. 5)
* 3/16: More progress in Aho and Thain books
* 3/17: More progress in Aho book.
* 3/18: More Aho book.
* 3/19: More Aho book.
* 3/21: Redrew compiler diagram.
* 3/22 - 3/23: Thain p. 14 notes in JH notebook.
* 3/24: Reviewed Thain regular expressions again in notebook. Moved forward with Thain Section 3.4 on Finite Automata and Deterministic Finite Automata.
* 3/25: More on FA and DFA.
* 3/26: The New Turing Omnibus by A.K. Dewdney, Chapters 2, 10, etc. on regular expressions, finite automata, etc.
* 3/27: ...
* 3/28: ...
* 3/29: ...
* 3/30: ...
* 3/31: ...
* 4/01: ...
* 4/02: Created page for Ellen D. Wu, [*The Color of Success*](/ewu-2014)
* 4/03: ...
* 4/12 - 5/03: Black Reconstruction
* 5/10: Began The Black Jacobins
* 5/11: Dewdney
	* Chapter 7: Four computers of the Chomsky Hierarchy
	* Chapter 2: Finite Automata
	* Chapter 14: Regular Languages
	* Chapter 26: Linear Bounded Automata
	* Chapter 31: Turing Machines

## Chapter 2: A Quick Tour
### Tools in a typical toolchain
* Preprocessor (e.g., **cpp** in gcc)
* Compiler proper (e.g., **cc1** in gcc)
* Assembler (called [**as** or **gas**](https://en.wikipedia.org/wiki/GNU_Assembler) in gcc)
* Static linker (e.g., [ld](https://ftp.gnu.org/old-gnu/Manuals/ld-2.9.1/html_node/ld_3.html) in gcc)
* Dynamic linker (e.g., [ld.so](http://manpages.ubuntu.com/manpages/cosmic/man8/ld.so.8.html) in gcc)
* See also Fig. 2.1 and drawings in JH notes Comp #1, 2/22/2021.

### Subcomponents within a Unix Compiler
* Scanner
* Parser (generates AST)
* Semantic Routines
* A series of code optimizers
* Code generator
* See also Fig. 2.2 and drawings in JH notes Comp #1, 2/24/2021.

## Chapter 3: Scanning
### Section 3.1: Kinds of Tokens
* Identifying [**tokens**](https://stackoverflow.com/a/39909662) in source code can be complicated.
	1. **Keywords** are reserved words in the language such as *while*, *class*, or *true*.
	2. **Identifiers** are programmer-definable names for variables, functions, classes, and other code elements. Some languages like Perl require certain **sentinels** such as the dollar sign ($) to denote all variable_names. 
	3. **Numbers** can be formatted as integers, floating point values, fractions, or in alternate bases such as binary, octal, or hexadecimal. 
	4. **Strings** are literal character sequences that must be clearly distinguished from keywords or identifiers, typically set off by single or double quotes. Strings should also have the ability to handle escaped characters, quotations, new lines, and unprintable characters.
	5. **Comments** are used to clarify the code.
	6. **Whitespace** are also used to make the code more human-readable and my play a role in the structure of the program (e.g., Python).

### Section 3.2: A simple, formal scanner
* See [Figure 3.1](https://www3.nd.edu/~dthain/compilerbook/chapter3.pdf) on p. 12.

