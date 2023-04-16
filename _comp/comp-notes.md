---
title: Comp Notes
permalink: /comp-notes/
---

## 2021 Log
* 2/21/2021: upgraded laptop to Big Sur. Downloaded Atom editor.
* 2/22/2021: downloaded Command Line Tools for Mac OS v. 12.4 and was able to get "Hello World" working in Atom and cmdline using clang. Appropriate because it has been exactly 43 years and 1 day since K&R pubished this, per [Daring Fireball](https://daringfireball.net/linked/2021/02/23/hello-world) and [CSAIL at MIT](https://twitter.com/MIT_CSAIL/status/1363875135191678984).
* 2/24/2021
	* Started new paper notebook
	* Redrew Thain Chapter 2 diagram [**Figure 2.1 – Typical Toolchain**](https://www3.nd.edu/~dthain/compilerbook/chapter2.pdf): Preprocessor &#8594; Compiler &#8594; Assembler &#8594; Static Linker &#8594; Dynamic Linker.
	* Redrew [**Fig 2.2 – Stages of a Typical Unix Compiler**](https://www3.nd.edu/~dthain/compilerbook/chapter2.pdf): Scanner &#8594; Parser &#8594; *AST* &#8594; Semantic Routines &#8594; Multiple rounds of Optimizers &#8594; Code Generator &#8594; *Assembly.s output* 	* Experimented with clang to output AST per [these  instructions](https://bastian.rieck.me/blog/posts/2015/baby_steps_libclang_ast/)
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

### Chapter 2: A Quick Tour
#### Tools in a typical toolchain
* Preprocessor (e.g., **cpp** in gcc)
* Compiler proper (e.g., **cc1** in gcc)
* Assembler (called [**as** or **gas**](https://en.wikipedia.org/wiki/GNU_Assembler) in gcc)
* Static linker (e.g., [ld](https://ftp.gnu.org/old-gnu/Manuals/ld-2.9.1/html_node/ld_3.html) in gcc)
* Dynamic linker (e.g., [ld.so](http://manpages.ubuntu.com/manpages/cosmic/man8/ld.so.8.html) in gcc)
* See also Fig. 2.1 and drawings in JH notes Comp #1, 2/22/2021.

#### Subcomponents within a Unix Compiler
* Scanner
* Parser (generates AST)
* Semantic Routines
* A series of code optimizers
* Code generator
* See also Fig. 2.2 and drawings in JH notes Comp #1, 2/24/2021.

### Chapter 3: Scanning
#### Section 3.1: Kinds of Tokens
* Identifying [**tokens**](https://stackoverflow.com/a/39909662) in source code can be complicated.
	1. **Keywords** are reserved words in the language such as *while*, *class*, or *true*.
	2. **Identifiers** are programmer-definable names for variables, functions, classes, and other code elements. Some languages like Perl require certain **sentinels** such as the dollar sign ($) to denote all variable_names. 
	3. **Numbers** can be formatted as integers, floating point values, fractions, or in alternate bases such as binary, octal, or hexadecimal. 
	4. **Strings** are literal character sequences that must be clearly distinguished from keywords or identifiers, typically set off by single or double quotes. Strings should also have the ability to handle escaped characters, quotations, new lines, and unprintable characters.
	5. **Comments** are used to clarify the code.
	6. **Whitespace** are also used to make the code more human-readable and my play a role in the structure of the program (e.g., Python).

#### Section 3.2: A simple, formal scanner
* See [Figure 3.1](https://www3.nd.edu/~dthain/compilerbook/chapter3.pdf) on p. 12.


----------------

## 2022 Log
* 6/28 Did some thinking and writing about difference between DevMarketing and DevRel. How DevRel = Evangelism + Advocacy.
* 7/11 Research into WebAuthn
	* The two complementary components of [FIDO2](https://en.wikipedia.org/wiki/FIDO2_Project) are: (1) The  [WebAuthn](https://en.wikipedia.org/wiki/WebAuthn) standard and (2) The [CTAP2 protocol](https://en.wikipedia.org/wiki/Client_to_Authenticator_Protocol) short for Client To Authenticator Protocol 2.
	* Use cases suggested by W3C / FIDO2 [official developer documentation](https://www.w3.org/TR/webauthn-1/#use-cases), Section 1.2
		1. New user registration
		2. Existing/returning user authentication
		3. New device registration
		4. Other use cases: (a) creation/registration of a new credential to support additional factor to increase security of an existing log-in flow, e.g., registering a Yubikey (b) single payment or other transaction from a [relying party](https://www.w3.org/TR/webauthn-1/#relying-party)
	* Researched [relying party applications](https://en.wikipedia.org/wiki/Relying_party), [claim-based identity](https://en.wikipedia.org/wiki/Claims-based_identity), [STS](https://en.wikipedia.org/wiki/Security_token_service) short for Secure Token Service, etc.
		* Wrt to Claim-based identity, it is important to distinguish between a **claim** refers to what an entity *is* or *is not*; claim does not refer to what the roles, responsibilties, priveleges this entity has.  In contrast, the abilities/privileges granted to a given entity is separately determined by the receiving application. Each application may have different mappings between what a "Normal User" *is* and what she can *do*.
* 7/12 Drew diagrams and made powerpoint architecture diagrams of WebAuthn compared to traditional username/password authentication.
* 7/14 More on WebAuthn and how to communicate it
* 7/20 Rebuilt hello world Node app to allow me to examine bitwise operations. Working well and I'm able to experiment with rather large decimal numbers and see what happens when I apply XOR operations on them.
* 7/26 Began reading about how to use registers in vim. [Good article here](https://www.brianstorti.com/vim-registers/)
* 7/27 Recorded simple first macro in vim. Turning on line numbers with :set number invoked by @n
* 7/28 Recorded second macro to add a new section to the top of a file. Invoked by @o (lowercase letter "o"):
	1. start macro recording - q
	2. choose register "o" you want to store this macro in: lowercase "o"
	3. go to top of document - gg
	4. Add 6 lines *above* - "6" then "capital O"
	5. change back to CMD mode - <esc>
	6. move up 2 lines - kk
	7. change to EDIT mode - i
	8. enter 20 dashes "---" etc
	9. change back to CMD mode - <esc>
	10. go back to top of document - gg
	11. change to EDIT mode - i
	12. change back to CMD mode - <esc>
	13. quit out of macro recorder - q
	* final command sequence including initial invocation of macro recording and exiting out of macro recording: qogg6O<esc>kki--------------------<esc>ggi<esc>q
* 7/31 When in Command mode, typing * by itself (asterisk) will automatically search forward for any future instance of the current word. Interesting shortcut. No need to type / to invoke search and you can see what vim is doing b/c it populates a search field for you at the bottom of the screen.
* 8/03 Started reading *You Don't Know Javascript, 2nd Edition*. On [Chapter 1](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md).
* 8/18 Research on SSGs, API CMSs, and Deployment/Hosting Platforms
* 8/20 Learned more about Visual Block mode to add inital characters to a whole bunch of lines. See OneNote for more
* 8/21 Visual Block mode, remember shift-i to insert (*not* just lowercase i) and <esc> produces a short delay before the edits take place on all the lines.

---------------------------------------

## 2023 Log
* 1/29/2023 - set up new Mac Studio
* 1/31 - more on fish shell etc.
* 2/01	- Experiments with Stable Diffusion / DiffusionBee
* 2/02 - podcast discussion. Difference between [GAN and diffusion model](https://octoml.ai/blog/from-gans-to-stable-diffusion-the-history-hype-and-promise-of-generative-ai/)
* 2/04 - Read some earlier papers on diffusion
* 2/05 - [2015 original paper](https://arxiv.org/abs/1503.03585) on diffusion by Sohl-Dickstein, Weiss, et al "Deep Unsupervised Learning using Nonequilibrium Thermodynamics"
* 2/08 - set up website. tested with libsyn and riverside
* 2/09 - Got stable diffusion working on the Mac Studio and documented all the steps.
* 2/10 - sf.org domain assigned to libsyn. researched miniconda / minimamba as alternatives.
* 2/11 - plan: use brew to install mamba, pip (for python only libraries that are not in mamba/conda). Uninstall everything else except for npm 
* 2/12 - Review Goodfellow, Bengio, and Courville on history of autoencoders
* 2/13 - more GBC on autoencoders, refers to GOFAI/symbolic approach as "knowledge base" approach. But I think KB was really an 80s subset of symbolic overall approach.
* 2/14 - Final version of sf.o e1
* 2/15 - SF podcast now syndicated to Apple, Spotify, Overcast, etc.
* 2/17 - 20 more eleventy
* 2/21 - read [Stephen Wolfram](https://writings.stephenwolfram.com/2023/02/what-is-chatgpt-doing-and-why-does-it-work/) and [Murray Shanhan](https://arxiv.org/abs/2212.03551) Feb 2023 articles on LLM
* 2/23 - more articles on history of BERT, transformers, MUM, etc.
	* This 18 minute [YouTube video](https://youtu.be/wi0M2J4uE5I) by Mean Gene Hacks compares 3 LLMs that all have about 175 B parameters: OpenAI's GPT-3, BigScience's BLOOM, and Facebook's OPT-175 
* 2/24 - Today, [FB released LLaMA](https://ai.facebook.com/blog/large-language-model-llama-meta-ai/) (Large Langauge Model Meta AI) in 4 sizes 7 billion parameters, 13 billion parameters, 33B parameters, and 65B parameters. Yann LeCun claims that LLaMa-13B outperforms GPT-3 (even though the latter has 175B). And LLaMA-65B is competitive with the best models like Chinchilla70B and PaLM-540B.
* 2/25 - should read this [visual primer on pixels and css](https://every-layout.dev/rudiments/units/) by Andy
* 2/26 - Options for next eleventy course
	* Stephanie Eckles [Oct 2020](https://11ty.rocks/posts/create-your-first-basic-11ty-website/)
	* Stephanie Eckles [March 2021](https://www.smashingmagazine.com/2021/03/eleventy-static-site-generator/)
* other starter kit / tutorials sourced from [the main Eleventy site](https://www.11ty.dev/docs/tutorials/)
	* Zach Leatherman's January 2018 tutorials: [Level 1](https://www.zachleat.com/web/eleventy-tutorial-level-1/) and [Level 2](https://www.zachleat.com/web/eleventy-tutorial-level-2/)
	* July 2021 [a place for my head](https://shivjm.blog/colophon/how-i-create-an-article-series-in-eleventy/) with references on discord by [Shiv JM](https://shivjm.blog).
	* July 2022 [Detailed guide](https://5balloons.info/guide-tailwindcss-eleventy-static-site/) to building with 11ty and TailwindCSS by Tgugnani 
* 2/27 More courses found
	* **Good eleventy [walkthrough](https://rphunt.github.io/eleventy-walkthrough/template-files.html) with clear organization**, explanation of data files etc
	* good default [directory structure](https://www.webstoemp.com/blog/eleventy-projects-structure/) from webstoemp
* 2/28 set up new computer. Got Stable Diffusion working fast! also set up .vimrc .bash_profile etc.
* 3/01 updated colors for .bash_profile and .vimrc files. IR_Black ty Todd
* 3/10 good list of keyboard shorcuts for [Audacity on Mac](https://tutorialslink.com/shortcut-keys/most-used-keyboard-shortcut-keys-in-audacity-for-mac-os)
* 3/13 Wow I made so much progress this past weekend. Saturday with vim customization and Sunday with HN related projects and getting them working
	* See [3/15 notes](/startups-v-incumbents-2023a/) on startups incumbents, the business of Gen AI.
* 3/27 Found out about privacy-focused web analytics using [Plausible](https://plausible.io/privacy-focused-web-analytics) from Erich Grunewald's [blog](https://www.erichgrunewald.com). Came here from this [HN thread](https://news.ycombinator.com/item?id=35332537)
* 4/05 While researching [Kraska's 2017 paper on B-Trees and Learned Indexes](https://arxiv.org/abs/1712.01208), came across this [2021 review article by Nan Wu and Yuan Xie](https://arxiv.org/abs/2102.07952) "A Survey of Machine Learning for Computer Architecture and Systems". Another interesting paper by Kraska:
	* [2019 by Nathan, Ding, Alizadeh, Kraska](https://arxiv.org/abs/1912.01668) introducing Flood to Learn Multi-Dimensional Indexes
* 4/09 Did some reading about how hard links and soft links and symlinks work in Unix filesystems.
	* [this article](https://toolhub.tech/blog/Difference-between-Symbolic-Link-and-Hard-Link/) unfortunately has a lot of spammy ads but the content is not bad and there is a helpful diagram of relationship between files, data on hard disk, and relationship of hard links and symlinks.
	* The [inode](https://en.wikipedia.org/wiki/Inode) article on wikipedia is pretty good. i-node might have referred to "index-node".
	* [Hard link](https://en.wikipedia.org/wiki/Hard_link) article at wiki.
	* Symbolic links, [symlinks](https://en.wikipedia.org/wiki/Symbolic_link), and soft links are all perfectly synonymous. 
	* Note however, that macOS aliases are slightly different than symlinks. See [this article last updated 2020](https://www.lifewire.com/aliases-symbolic-links-hard-links-mac-2260189)
	* See ChatGPT convo 4/09. Prompt to ChatGPT: 'In UNIX, is there any difference between symbolic links and soft links?'
		* GPT response: 
			* 'In UNIX, "symbolic link" and "soft link" are two different terms used to refer to the same thing, which is a special type of file that acts as a pointer to another file or directory.
			* 'Symbolic links are created using the ln command with the -s option. They are also sometimes referred to as soft links or symlinks. A symbolic link is simply a small file that contains a path to the target file or directory.
			* 'The term "soft" is used to differentiate symbolic links from "hard links," which are another type of link in UNIX. Hard links are a way to create additional names (i.e., links) for a file or directory, but they must be on the same filesystem as the original file or directory.
			* 'So, to answer your question, there is no difference between symbolic links and soft links in UNIX. They are just two different terms used to refer to the same thing.'