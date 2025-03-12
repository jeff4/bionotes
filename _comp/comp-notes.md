---
title: Comp Notes
permalink: /comp-notes/
sitemap: false
---

## 2021 Comp Notes
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
* 4/02: Created page for Ellen D. Wu, [*The Color of Success*](/ewu-2014)
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
	* See [3/15 notes](/startups-v-incumbents-2023/) on startups incumbents, the business of Gen AI.
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
* 4/19 ["Offline Is Just Online With Extreme Latency"](https://blog.jim-nielsen.com/2023/offline-is-online-with-extreme-latency/) and [HN thread](https://news.ycombinator.com/item?id=35626015)
* 4/28 Microsoft is rewriting some parts of Windows core in Rust. [HN thread](https://news.ycombinator.com/item?id=35735444)
* 4/29 [Old 2014 post](https://buildyourownlisp.com/contents) on learning C by creating a compiler and designing a custom LISP. Recent [HN thread](https://news.ycombinator.com/item?id=35726033) with [rebuttal and critique](https://gist.github.com/no-defun-allowed/7e3e238c959e27d4919bb4272487d7ad)
* 5/04 [Seven ur-languages of programming](https://madhadron.com/programming/seven_ur_languages.html) from 2021. [HN thread](https://news.ycombinator.com/item?id=35813496)
* 5/07 Sample [dotfiles from Rachel Kroll](https://rachelbythebay.com/w/2023/05/05/dot/)
* 5/18 Reminiscing about building out [Google's infrastructure by scaling up](https://motherduck.com/blog/the-simple-joys-of-scaling-up/) and [HN thread](https://news.ycombinator.com/item?id=35988984)
* 7/05 From February, 2023, ['A human just defeated an AI in Go. Here’s why that matters'](https://news.ycombinator.com/item?id=36590242), and [HN thread](https://news.ycombinator.com/item?id=36590242)
* 7/06 Meta/FB/Instagram launched Threads today and here's an [HN article](https://news.ycombinator.com/item?id=36612835) about how the backend is built in Python 3.10

## 7/14 - 7/16 awk resources
* Watched [intro video to awk by Gary Explains](https://youtu.be/jJ02kEETw70) (20 minutes long)
* Ben Porter's [history and tutorial video for awk](https://youtu.be/E5aQxIdjT0M) (1 hour long) 
* Bruce Barnett aka Grymoire also has an [Intro and Tutorial for Awk](https://grymoire.com/Unix/Awk.html).

## 8/10
* Been experimenting with alternative terminal emulators recently. First [Warp](www.warp.dev), then today [Alacritty](https://github.com/alacritty/alacritty). At some point, will refactor color themes available on [GitHub](https://github.com/alacritty/alacritty-theme)

## 8/10 Regex notes
* z\* matches zero to any z's found. z+ matches 1 to any z's found. z? optionally matches z's found.
* Good [regex tutorial](https://www.regular-expressions.info/optional.html). Question mark is called a *quantifier*. This tutorial mostly focuses NFA aka "regex-directed" engines.
* The 12 reserved charactes in regex like *?.()[]* are called special characters or **metacharacters**.
	* Note that single quote and double quote are *not* metacharacters. You can treat them as literals.
* The section on how [regex engines work internally](https://www.regular-expressions.info/engine.html) is essential! The end of this section has a simple but clear example of how left-most matching and sequencing works when matching.
* This website also has a good [summary of GNU regexp](https://www.regular-expressions.info/gnu.html) for tools like GNU sed. But the site also has [extensive documentation about regexp support/flavors for many other languages, frameworks, and tools](https://www.regular-expressions.info/reference.html).
* Most flavors of sed use traditional NFA per the [3rd edition of Mastering Regular Expressions (2006)](https://www.oreilly.com/library/view/mastering-regular-expressions/0596528124/ch04.html). In other words, sed regex is non-deterministic. See [this excellent semi-academic blog post](https://www.abstractsyntaxseed.com/blog/regex-engine/nfa-vs-dfa). The end of [Chapter 4 of MRE](https://www.oreilly.com/library/view/mastering-regular-expressions/0596528124/ch04.html) has good examples to help determine if a particular regex engine is NFA, Traditional NFA, POSIX NFA, DFA, or a hybrid between NFA/DFA. 
	* NFA = Non-deterministic Finite Automata aka "regex directed"
	* DFA = Deterministic Finite Automata aka "text directed". Always greedy.
* Character classes = Character sets are synonyms. Defined by square brackets around the set [].
* ^ = negation for the remainder of a character class.
* Most of the usual [metacharacters act as a normal literal character when inside square brackets](https://www.regular-expressions.info/charclass.html) as part of a class! i.e. "In most regex flavors, the only special characters or metacharacters inside a character class are the closing bracket ], the backslash \, the caret ^, and the hyphen -. The usual metacharacters are normal characters inside a character class, and do not need to be escaped by a backslash. To search for a star or plus, use [+*]. Your regex will work fine if you escape the regular metacharacters inside a character class, but doing so significantly reduces readability."
	* Special note which I think applies to gsed: "The closing bracket ], the caret ^ and the hyphen - can be included by escaping them with a backslash, or by placing them in a position where they do not take on their special meaning. The POSIX and GNU flavors are an exception. They treat backslashes in character classes as literal characters. So with these flavors, you can’t escape anything in character classes."
* Common shorthands to avoid typing the same character class over and over again:
	* **\d** = [0-9], i.e., all digits
	* **\w** = [A-Za-z0-9_], i.e. all 'word' characters
	* Note "It always matches the ASCII characters [A-Za-z0-9_]. Notice the inclusion of the underscore and digits. In most flavors that support Unicode, \w includes many characters from other scripts. There is a lot of inconsistency about which characters are actually included. Letters and digits from alphabetic scripts and ideographs are generally included. Connector punctuation other than the underscore and numeric symbols that aren’t digits may or may not be included." from [this section](https://www.regular-expressions.info/shorthand.html)
	* **\s** = whitespace characters. BUT "\s stands for “whitespace character”. Again, which characters this actually includes, depends on the regex flavor. In all flavors discussed in this tutorial, it includes [ \t\r\n\f]. That is: \s matches a space, a tab, a carriage return, a line feed, or a form feed. Most flavors also include the vertical tab, with Perl (prior to version 5.18) and PCRE (prior to version 8.34) being notable exceptions. In flavors that support Unicode, \s normally includes all characters from the Unicode “separator” category. Java and PCRE are exceptions once again. But JavaScript does match all Unicode whitespace with \s." A lot of inconsistency!
	* you can negate any of the shortcuts above by use uppercase versions of the shortcuts. e.g., **\D** = anything *other than digits*; **\S** = anything *other than whitespace characters*.

## 8/11 Regex notes
* **\b** = very useful word border. Used in history file and detected The, These, There, Their, etc. See OneNote also from 8/11 under gsed notes.
* From [The Dot section](https://www.regular-expressions.info/dot.html), scroll to the bottom two sections. \N never matches line breaks. But more importantly, use the dot sparingly. Probably better to use a negated characer class instead of the form \[^ these chars are negated\].
* ^ and $ at the beginning and end of lines (obviously like in vim), are called [*String Anchors*](https://www.regular-expressions.info/anchors.html).
* [Parentheses are used for grouping](https://www.regular-expressions.info/brackets.html) while [**pipes \|**](https://www.regular-expressions.info/alternation.html) are used to demarcate different enumerated options like a multiple choice or case/switch block.
	* Note that POSIX like GNU usually chooses the longest option, etc., prefers *catapult* instead of *cat* in the expression **(cat \| catapult )**. So you need to be explicit to make sure the longest or left-most option is not used. 
* Optional items are marked by the **? question mark** as described in [this section](https://www.regular-expressions.info/optional.html) which also explains the concept of greediness.
* Star \(*) and Plus \(+) allow 0-infinite matches and and Plus allow 1-infinite matches. You can also specify how much reptition exactly with curly braces{}. See more at [this article](https://www.regular-expressions.info/repeat.html)

## 8/12 Starship prompt notes
* Successfully installed Nerd Font and Starship. Basic check show that both are working.
* However, not seeing how to modify the color schemes for input versus output yet.
* Next steps. Try seeing results with zsh. And try on ARM.

## 8/19 sed
* When using shuf to shuffle contents of /zhongwen, make sure to use the -o option to indicate output file, e.g., 
		`shuf source.txt -o output.txt`

## 8/22 
* [Short blog post](https://utcc.utoronto.ca/~cks/space/blog/unix/UnixTechnologyAndIdea) about Unix as a technology and as an idea. [HN thread](https://news.ycombinator.com/item?id=37205536)
* Purchased Peter Krumins' (catonmat) e-book [*Sed One-Liners Explained*](https://catonmat.net/sed-book). See Box.

## 8/24
* [HN thread on icons](https://news.ycombinator.com/item?id=37245530) referencing a Medium article.

## 9/09 - Back to Eleventy. First deploy with Netlify 
* Got started with Netlify [using these instructions](https://docs.netlify.com/get-started/)
* Node, npm, Netlify CLI are all installed and up to date. Now to choose an Eleventy Starter Kit.

### Eleventy Starter Kits 
* Top candidate starter projects from [this page](https://www.11ty.dev/docs/starter/):
	* [Twelvety by Greg Ives](https://github.com/gregives/twelvety) has nice photos and has responsive picture shortcodes with AVIF and WebP support. Last updated June 2021, 140 commits, 291 stars. This and 11tyOne by Phil Hawksworth are the leaders so far. [Demo site](https://twelvety.netlify.app).
	* [EleventyOne by Phil Hawksworth](https://github.com/philhawksworth/eleventyone) looks small, fast, and tested. Only challenge is that it was created Jan 2021 and hasn't had much updates since then? 462 stars, 112 forks. [Demo site](https://eleventyone.netlify.app). 
	* [Eleventy Starter Ghost](https://github.com/TryGhost/eleventy-starter-ghost) is quite good, has 330 stars, 162 forks, last commit was in 2022.
	* [Eleventy-Starter-Boilerplate](https://github.com/ixartz/Eleventy-Starter-Boilerplate/) by [CreativeDesignsGuru](https://creativedesignsguru.com). Has 256 stars, 53 forks, last commit was in 2021. They offer $29 premium themes as well. Detailed instructions on running locally and deploying via Netlify. [Demo site here](https://creativedesignsguru.com/demo/Eleventy-Starter-Boilerplate/eleventy-starter-boilerplate-presentation/)
	* [Neat Starter by Surjith S M](https://github.com/surjithctly/neat-starter) and [demo site](https://neat-starter.netlify.app/blog/). Barebones and created in 2020, but has 289 stars. 
* Other options:
	* [Smix by Jane Doe](https://smix.netlify.app), aka by [Ru Singh](https://rusingh.com). [github repo](https://github.com/MaybeThisIsRu/smix-eleventy-starter) has 110 stars. I like the rather stark black background and simple text.
	* [Eleventy Plus Vite by Matthias Sott](https://github.com/matthiasott/eleventy-plus-vite) and [demo site](https://eleventyplusvite.netlify.app) has 151 stars. 
	* [Pack11ty](https://pack11ty.dev) has 184 stars
	* [11TA by Shane Robinson](https://github.com/11ta/11ta-template). [Demo site with forest](https://11ta.netlify.app) indicates that Shane was inspired by [EleventyOne](https://github.com/philhawksworth/eleventyone) and [jet by Marc Amos](https://github.com/marcamos/jet). 11TA has 111 stars.
	* [Twenty Ninety](https://www.seancdavis.com/twenty-ninety) by Sean Davis

### Configure DNS
* Go to Hover and add CNAME per [this Netlify doc](https://docs.netlify.com/domains-https/custom-domains/configure-external-dns/#configure-a-subdomain). with Hostname = `www` and TargetName = `jeffhwang.netlify.app`.
* OK after a bunch of SSH and email privacy work, got git working locally on cmdline and able to push/pull to GitHub.
* Note: content of header and other items are stored in `twelvety/src/_includes/`
* Success! jeffhwang.me now points to jeffhwang.netlify.app

## 9/10
### Next steps for Twelvety
* draw diagram explaining tree structure of Twelvety
* test uploading photos as assets

### Tree structure of Twelvety
Below tree was generated by typing the **tree** command from the parent **proj-1** directory: `tree -d ./twelvety`

		twelvety
		├── src
		│   ├── _assets
		│   │   ├── images
		│   │   └── styles
		│   ├── _data
		│   ├── _includes
		│   └── _layouts
		└── utils
		    ├── shortcodes
		    └── transforms

### Comments on tree structure
* Tooling is inside the `utils` subdirectory. No need to make any changes here
* Note that `.twelvety.js`, `.eleventy.js`, `package.json` are files located at the root
* I presume that I add source images to `/src/_assets/images`. And if I want to use different CSS, I add those to `/src/_assets/styles`

### _includes subdirectory 
* `src/_includes/header.html` -- edit this to change header, e.g., changed from Twelvety --> Jeff Hwang, changed GitHub link from Greg's to mine.
* `src/_includes/content.md` -- edit this to change the main content on the home page.

### _layouts subdirectory
* `src/_layouts/default.html`. Currently, there is only one layout here, `default.html`. For different page types, like posts, etc. probably need to create new *.html files to be stored in `src/_layouts/`

### _data subdirectory
* `src/_data/meta.json` contains critical sitewide info for fields including Site Name, Title Field, Description field for snippets that show up in SEO etc.
	* `"site": "Twelvety"` -- this is the sitewide name.
	* `"title": "Eleventy Starter"` -- this is the name of the specific page we are on.
	* `"site": "Twelvety"` -- this is the description; is this sitewide, or can i configure this page by page?

### A lot of wrestling with SSH today
* realized that I had mistyped `Identityfile` and spelled it `Identifyfile`.
* shows the importance of copying and pasting when possible. typos are dangerous and hard to find. the `ssh-add` utility error message was not superhelpful. The way i debugged it in the end was that i moved around the lines of the `~/.ssh/config` file.
* Next steps
	* Browse the [Readme](https://github.com/jeff4/twelvety/blob/master/README.md) for more info on how the directory and systems work. Note: a lot of this details functioning under the hood in the utils directory.
	* Watch 11ty video series crash course from scratch youtube

## 9/11
### Other Eleventy starters to try
* I like [Yetty](https://github.com/ygoex/yetty) in all ways *except* the cross-out line that is used to denote which page you are currently on. See [demo site](https://jamstackthemes.dev/demo/theme/11ty-yetty/)
* [Fernfolio](https://github.com/TylerMRoderick/fernfolio-11ty-template) is very minimalist but might do the job. [Demo site](https://fernfolio.netlify.app)
* [TwentyTwentyOne](https://github.com/smolcodes/twentytwenyonetheme) has a typo in the github project name / URL. Only 5 stars in GH. [Demo site](https://jamstackthemes.dev/demo/theme/twentytwentyone/). still looks pretty good and embeds Math syntax js libraries.

## 9/12
* Got GH working consistently. Critical to use `git remote set-url origin git@github.com/USERNAME_AT_GITHUB:_repo-name_` to enforce authentication over SSH rather than HTTPS/user-password.

### Tree structure of Fernfolio
Below tree was generated by typing the **tree** command from the parent **proj-1** directory: `tree -d ./fernfolio-11ty/`

		fernfolio-11ty
		└── src
		    ├── _11ty
		    │   ├── filters
		    │   ├── libraries
		    │   ├── shortcodes
		    │   └── utils
		    ├── _data
		    ├── _includes
		    │   ├── macros
		    │   └── partials
		    ├── _layouts
		    ├── admin
		    │   └── preview-templates
		    ├── assets
		    │   ├── img
		    │   ├── js
		    │   └── scss
		    │       ├── components
		    │       ├── global
		    │       ├── layouts
		    │       └── third-party
		    ├── pages
		    ├── posts
		    ├── projects
		    └── tags

### Other comments
* Footer content is stored in `/src/_includes/partials/footer.njk`
* Separately, to edit the content in the homepage, go to `/src/_data/home.json`
* Hints on how to modify sitewide header / navigation bar.
    * Note that `/src/_includes/partials/site-header.njk` has references to
    * Look also at `/src/admin/preview-templates/index.js` has a section called `Register CSS` and another called `Register preview templates`.
	* Another hint. `grep -r "[Bb]log" >out.txt" returns potential culprit `./src/admin/config.yml`.
* Successfully accessed Decap CMS (formerly called Netlify CMS). Needed to give a password to the user (see 1p). Access by going to `[project-name].netlify.app/admin`.

## 9/13/2023
### Yetty Tree Structure
Below tree was generated by typing the **tree** command from the parent **proj-1** directory: `tree -d ./yetty/`

		yetty
		├── src
		│   ├── _data
		│   ├── _includes
		│   │   └── layouts
		│   │       └── partials
		│   │           └── components
		│   │               ├── navigation
		│   │               ├── post-card
		│   │               ├── svg-icon
		│   │               └── tags-list
		│   ├── about
		│   ├── assets
		│   │   ├── images
		│   │   │   └── favicon
		│   │   ├── scripts
		│   │   │   └── vendors
		│   │   └── styles
		│   │       └── scss
		│   │           └── partials
		│   │               ├── 01-Abstract
		│   │               ├── 02-Generic
		│   │               ├── 03-Components
		│   │               ├── 04-Layout
		│   │               ├── 05-Templates
		│   │               ├── 06-Pages
		│   │               ├── 07-Utilities
		│   │               └── 08-MQ
		│   ├── feed
		│   └── posts
		└── utils
		    ├── collections
		    ├── filters
		    ├── shortcodes
		    └── transforms

### Comments
* To edit home content, go to `/src/_data/home.json`
* To edit About page, go to `/src/about/index.md`
* Not sure what key/order does inside `/about/index.md`
* To change sitewide info, go to `/src/_data/metadata.json`. Here, you can change critical things like sitewide title, URL, description, repo, contact info for the author, etc.
	* Esp. when it comes to author key-value pairs, these populate into the footer via the nunjucks code inside `/src/_includes/layouts/partials/footer.njk`
* The `/src/_includes/layouts/partials` directory is critical. It contains these files:
	* `head.njk` which is the templated version of *Head* for all the HTML on the site
	* `footer.njk` which is the templated version of the sitewide footer. Populated by things like author metadata from `/src/_data/metadata.json`. 
	* `header.njk` is pretty short and simple. Decided to comment out the "get the code" button using `{# #}`. See info on Nunjucks comments [here](https://mozilla.github.io/nunjucks/templating.html#comments).
* Going to copy `/partials/footer.njk` into `original-footer.txt` so I can do major changes to it.
* used [info in this article](https://www.linode.com/docs/guides/how-to-undo-git-commit/#how-to-undo-a-git-commit). Remember, you can do a soft reset which maintains original change plus reset; or you can do a hard reset that brings you back entirely.
* [git amend to change commit message](https://leonardomontini.dev/git-undo-amend-reset/) look at option #2.
	* See also this [answer from phind.com](https://www.phind.com/search?cache=wkpr6ck5mh8bqzmr1uerj1ww)

### Tried Astro-v
* Got it successfully downloaded. need to set it up on Netlify.

## 9/14/2023 Astro-v
### Tree structure just directories
* Command `tree -rd ./astro-v`

		astro-v
		├── src
		│   ├── pages
		│   ├── layouts
		│   └── components
		└── public

### Tree structure including both files and directories
* Command `tree -r ./astro-v`

		astro-v
		├── tsconfig.json
		├── tailwind.config.cjs
		├── src
		│   ├── pages
		│   │   ├── index.astro
		│   │   └── content.js
		│   ├── layouts
		│   │   ├── BaseLayout.astro
		│   │   └── AccordionLayout.astro
		│   ├── env.d.ts
		│   └── components
		│       ├── Header.astro
		│       ├── Footer.astro
		│       ├── Container.astro
		│       └── Card.astro
		├── public
		│   ├── screenshot.jpeg
		│   ├── profile.jpg
		│   ├── favicon.svg
		│   ├── content_code.png
		│   └── accordion_code.png
		├── package.json
		├── package-lock.json
		├── original-README.md
		├── astro.config.mjs
		├── README.md
		└── LICENSE.md

* Comments. not able to build/deploy Astro-vitae successfully on Netlify. Also, seems like my yetty instance is borked and no longer builds/deploys. Decided to eliminate both Astro-v and yetty.
* Reactivated my old Discord account and joined both the 11ty and Astro Discord communities. Seems like the Astro Discord is much more active. Resources:
	* Continue working through [Astro beginner tutorial](https://docs.astro.build/en/tutorial/0-introduction/1/)
	* Watch this [2022 Astro Crash Course video on YouTube](https://www.youtube.com/watch?v=cbYr75_R15M). Note the associated [github repo](https://github.com/littlesticks/astro-101) by littlesticks aka Jordan U.
	* Consider watching this [2022 Discord youtube guide](https://www.youtube.com/watch?v=nPmdafMo1b8)

* Currently, only two sites left. 
	* jeffhwang.net.ap points to a Twelvety site. DNS records have not resolved yet so the primary domain listed is still whalesharkconsultig.
	* jeffhwang-test.net.ap points to Fernfolio.  let's rename this to jeffhwang-t1.net.ap
	* Both jh-t2 and jh-t3 are confirmed deleted now.

### Tutorial for Astro
* [Astro beginner tutorial](https://docs.astro.build/en/tutorial/0-introduction/1/) 
* First, make sure node is up to date with the brew update > doctor > upgrade sequence.
* Next, go to desired parent directory (`proj-4`) and type `npm create astro@latest` which should launch a commandline install wizard. Options chosen:
	* Name new directory `a2-astro`
	* How would you like to start your new project? Rather than 'full source', or 'blog template', i chose `empty` to create from scratch.
	* Install dependencies? `yes`
	* Do you plan to write Typescript? `no`
	* Initialize a new git repo? `yes`


### Tree structure of a2
* Command to `-r` recursively search while `-I` ignoring the `node_modules subdirectory (which is *enormous*). Execute this command from the parent `/proj-4` directory: `tree -r -I node_modules a2-astro/`

#### tree structure of files + directories
		a2-astro
		├── tsconfig.json
		├── src
		│   ├── pages
		│   │   └── index.astro
		│   └── env.d.ts
		├── public
		│   └── favicon.svg
		├── package.json
		├── package-lock.json
		├── astro.config.mjs
		└── README.md


#### tree structure of directories only
* Execute this command from the parent `/proj-4` directory: `tree -rd -I node_modules a2-astro/`

		a2-astro/
		├── src
		│   └── pages
		└── public

## More steps
* First time I created a git-aware local directory and then pushed it to github. Not optimal, but I used the web UI to create a new repo at github.com.
* Next, I used my terminal to navigate to the local a2-astro directory. I followed [these instructions](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github#adding-a-local-repository-to-github-using-git):
	* `git remote add origin git@github.com:jeff4/a2-astro.git`
	* Then I verified that fetch/pull has the correct URLs (aka authenticated by SSH rather than HTTPS) with the command `git remote -v`
* Then, I used the usual sequence of `git add .`; `git commit -m "this is first comment etc"`; `git push origin`
* However, I got the error that 'fatal: The current branch master has no upstream branch. To push the current branch and set the remote as upstream, use `git push --set-upstream origin master`"
* this worked! However, now I have two branches: `main` and `master`. So I had to set `master` as the default branch and delete the old empty `main` branch. Note that `main` branch was created when I used the web ui to create the GH.com repo originally.  
* OK, deployed successfully to Netlify, and site is live!


## 9/16/2023 
* More on Astro tutorial
* From [Unit 2.1](https://docs.astro.build/en/tutorial/2-pages/1/), seems like for every new `[page].astro` file you add to `/src/pages/`, Astro creates a new page with a default route.
* Finished up to [Unit 2.2](https://docs.astro.build/en/tutorial/2-pages/3/). Now to define and use variables for dynamic content.
* [Unit 2.4](https://docs.astro.build/en/tutorial/2-pages/4/) introduces styles for the first time. Note that this is an [HTML tag](https://www.w3schools.com/tags/tag_style.asp). When entering this into the HEAD section of an HTML document, we can define a stylesheet that applies a style to the entire HTML page--without having to put in custom styles all over the BODY section.
* Finished all of Unit 2. On to [Unit 3--Components](https://docs.astro.build/en/tutorial/3-components/1/).
* A little confused in 3.2, create a social media footer. why is this `https://www.${platform}.com...` not working???. Ah ha! the problem is that i was using single quote `'` rather than the backtick `` ` ``! Now it works when i type

		<a href={`https://www.${platform}.com/${username}`}>{platform}</a>

## 9/17/2023
* Did some maintenance on mm-m2p. Changed from Dp-M to regular Dp. Also updated vbp and vrc and PlugInstall so that *.astro files have proper syntax highlighting. Also used one-liners in Terminal to filter by file sizes in [this article](https://apple.stackexchange.com/questions/118167/how-do-i-quickly-find-large-files-and-folders-on-my-mac)
* OK, did more work on componentizing Navigation, Header, Footer, and creating a hamburger menu for mobile viewport sizes. Completed Unit 3. 
* On to [Unit 4 - Layouts](https://docs.astro.build/en/tutorial/4-layouts/)
* completed Unit 4.1. Now onto creating my first blog post in 4.2.

## 9/18/2023
* have updated blog-post-1 but *not* blogposts 2 and 3 so far
* Successfully used `.gitignore` refactor in a2-astro root folder. Seems like there is some problem when i try to use the global `.gitignore` in my user home.
* Now have a stable notesection within Astro that only shows up locally.

## 9/19/2023
* Mostly finished the tutorial last night except for dynamic islands.


## 9/20/2023
### Additional Astro themes to try
* [Astro CUBE](https://github.com/williamhzo/astro-cube) 45 stars but i like it's minimalism. I think almost no JS.
* [Astro-Paper](https://github.com/satnaing/astro-paper) 1100 Stars!
* [Accessible Astro Starter](https://github.com/markteekman/accessible-astro-starter) 407 stars.
* [Astro Cactus](https://github.com/chrismwilliams/astro-theme-cactus) 359 stars.
* [Astrofy Template](https://github.com/manuelernestog/astrofy) 373 stars.
* [Blogster: Sleek](https://github.com/flexdinesh/blogster). In addition to sleek, has these subthemes: newspaper, bubblegum, and minimal. 340 stars. As of late August 2023, looks like Blogster has gone into [maintenance mode](https://github.com/flexdinesh/blogster#maintenance-status)--because Astro's new [content collections](https://docs.astro.build/en/guides/content-collections/) seems to deprecate some of the capabilities of Blogster.

### more themes from Friday 9/22/2023
* myfritz's [Astro Landing Page](https://github.com/mhyfritz/astro-landing-page/tree/main). 323 stars, 105 forks, might be best. Uses Astro and Tailwind and minimal JS. Only potential issue is astronaut grpahic. [Demo site](https://statichunt.com/demo/astro-landing-page)
* [Portfolio site](https://github.com/veranikabarel/astro-portfolio) is ok except that it probably requires more projects than I currently have. [Demo site](https://statichunt.com/demo/astro-portfolio)
* [Astro Boilerplate](https://github.com/ixartz/Astro-boilerplate) is a popular theme by [ixartz](https://github.com/ixartz). 509 stars, 206 forks. But probably too much for my needs. [Demo site](https://statichunt.com/themes/astro-boilerplate)

### Best candidates
* Astro CUBE, Astro-Paper, myfritz's Astro Landing Page.



## 9/22/2023 Friday
* Rebuild Astro tutorial from scratch in `/a3` subdirectory
* First, type `npm create astro@latest` above the new directory you want to create. I typed that in /p4 and the installer asks you the name of the directory which ended up being `/p4/a3/`
* Next edit `.gitignore` and add `*.swp *.swo` so that git does not track temporary vim files
* Type `vbp` to edit .bash_profile to add new aliases to most common astro directories

### list of commands to set up new github repo
* Used web app at github.com to create a new repo called `a3`
* Local commandline used these 3 commands in succession
	1. `git remote add origin git@github.com:jeff4/a3.git` This uses SSH to specify what "origin" refers to...in this case, the repo that lives at github.
	1. `git push --set-upstream origin master` This names the main branch master.
	1. `git push origin`  If you try to execute this command before the `git push --set-upstream origin master` command, git has a helpful error which tells you to execute --set-upstream first before git push origin.

## 9/23/2023 Saturday
* succeeded in transferring domains to Netlify and provisioning ssl certs for domain names.
* Continuing with Astro tutorial
* Next, going to start using variables per [Unit 3.2](https://docs.astro.build/en/tutorial/2-pages/3/)
* Completed first JS variables in both code fence area and main template area. Skipped styling pages individually in Unit 2.4. Jumped directly to site-wide styling in [Unit 2.5](https://docs.astro.build/en/tutorial/2-pages/5/)

## 9/24/2023 Sunday
* experimented with css
* In [Unit 4.2](https://docs.astro.build/en/tutorial/4-layouts/2/), consider continuing refactor of `MarkdownPostLayout.astro`
* Completed [Unit 5.1](https://docs.astro.build/en/tutorial/5-astro-api/1/) and first usage of `await Astro.glob()`. 

### Notes on CSS
* items to style are called selectors.
* remember cascade hierarchy. Most local / recent `<style>` wins
* Scroll down to the middle of [this article](https://mailchimp.com/resources/padding-vs-margin/) to see what it means when padding and margins have 1, 2, 3, or 4 values.  See this example from `../styles/global.css`:

		.footer a { 
			display: inline-block;
			padding: 10px 18px 0px 0px;
		}/

* Completed the entire tutorial. Next step is following [these instructions](https://docs.astro.build/en/guides/content-collections/#migrating-from-file-based-routing) to migrate from *file-based routing* to *content collections*.
* Hm. myfritz's Astro Landing page with the moving starfield and animated astronaut is cool but perhaps the file structure is too complex. Astro CUBE doesn't even have a components directory!
* I think [AstroPaper](https://astro-paper.pages.dev/about/) is the winner

## 9/25/2023 Monday
* Decided to go with AstroPaper. After verifying that I'm running an `npm --version` higher than 7.0, i used `npm create astro@latest -- --template satnaing/astropaper` (double double dash required per [Running Locally instructions](https://github.com/satnaing/astro-paper#-running-locally)
* In this case, I created the desired `a4` directory first, navigated to there, and within the astro installer, chose `./` as root directory. In previous installs, I went to `proj-n`, ran `npm create astro` command there, and then inside installer, I defined the root directory = `./a4/`.
* Edited `.gitignore` file to ignore vim temp files.
* Next, tried to edit the social media links in the footer. Went to inspect `/src/components/Socials.astro`. And I see it's importing from `@config` which is a TypeScript file located at: `/src/config.ts`. You can toggle the list of socials by setting values to false for each desired social.
* Followed steps from 9/22 to make sure local and remote branches synch via git. Actually, here are updated instructions. It's four steps:    
	1. `git remote add origin git@github.com:jeff4/a3.git` This uses SSH to specify what "origin" refers to...in this case, the repo that lives at github.
	1. Now, you have to go through usual sequence of: (a) `git add .`; (b) `git commit -m "this is my first commit"`. *Then* you have staged changes on local that allows steps 3 and 4.
	1. `git push --set-upstream origin master` This names the main branch master.
	1. `git push origin`  If you try to execute this command before the `git push --set-upstream origin master` command, git has a helpful error which tells you to execute --set-upstream first before git push origin.
* In the future, I will rewrite the instructions to default naming the origin branch **main** rather than 'master'. 

### Config of AstroPaper
* Things I modified in `/src/config.ts`:
	1. Turned 'Facebook.active' from true to false.
	1. Modified SITE properties, except have not yet changed from `website` property from `https://astro-paper.pages.dev/` to presumed `jeffhwang.me`.
	1. e.g., changed author to jeff; changed desc from " minimal, responsive and SEO-friendly Astro blog theme."
	1. under `const SITE: Site = {...`, the `title:` property formerly had value "AstroPaper". I've changed it to "Jeff Hwang" and that has changed the site wide title as well as the icon in the upper left.
* Next step is to remove Posts and Tags from the header. Succeded in doing this by just commenting out lines 61-70 in `/src/components/Header.astro`. Note that the original version is still in the `/components` directory, just renamed to `original-Header.astro.txt`.
* Now to fix social addresses by changing them in `/src/config.ts`. Deleted most references, which were just copies of the github address
* Executed from a4 root directory: `grep -r --exclude-dir=node_modules "Mingalaba"` to find where to delete Mingalaba on the homepage. It's located in the /src/pages/index.astro.

## 9/27/2023
### grep -r while excluding named subdirectories
* To exclude directories like `node_modules` from grep, see [this answer](https://stackoverflow.com/questions/6565471/how-can-i-exclude-directories-from-grep-r]). Example: `grep -r --exclude-dir=node_modules "rss.xml"` looks for the string `rss.xml` recursively from this directory including subdirectories but ignores the `node_moduels` subdirectory. To exclude a file, use the `--exclude=filename`` flag.

### More AstroPaper config
* A version of Astropaper is live at jeffhwang-a4.netlify.app and www.jeffhwang.me successfully points to there.
* Can't figure out why when I add 'Stepfunction' as a header item, the mobile version of the hamburger menu messes up horizontal alignment of light/darkmode control. Before adding Stepfunction, both search icon and light/dark icons were center aligned. Now, only search icon is; light/dark icon is left aligned :(
* Tested and `https://jeffhwang.me/rss.xml` allows people to subscribe to my blogposts. Going to comment out the `export async function get() {...` call from `/src/pages/rss.xml.ts` to see if I can kill this feed until I can get my blog posts up and running. For additional notes, see [Unit 5.4](https://docs.astro.build/en/tutorial/5-astro-api/4/) in the Astro tutorial to understand how to set up the rss feed.
* For some reason, Sat placed all blog posts within `/src/content/blog/`
	* note that `/src/pages/posts/` exists, but it has *.astro files. All *.md content files are in `/src/contet/blog`
* I don't quite understand within vim why this command worked. `:%s_ .*$__gc` Wanted to right-trim() every line. And I had processed the file such that every line terminated with a space ` ` and a carriage return. But it did seem to work and other variants like `:%s_ .*$_$_gc` and `:%s_ .*$_\$_gc` did not. They seemed to want to put in a literal `$` at the end of each file during replacement whether the `$` was escaped by a backslash or not. Note that i used underscores `_` instead of the usual `/` as grep delimiters for better readability
* Changed the subhead aka description on the Blog page from 'All the articles I've posted' to 'Writings on AI, tech, art, and history' in `/src/layouts/Posts.astro` > `<Main pageTitle="Posts" pageDesc="Writings on AI, tech, art, and history">`
* Note. Originally, the literal term 'Blog' was not used within AstroPaper. Sat preferred to use the term "Posts" everywhere. I've not changed the structure of his usage and posts is used as both static and dynamic routs. Here are the two places I've manually changed 'Posts' to 'Blog':
	1. In `/src/layouts/Posts.astro`, I changed  `<Main pageTitle="Posts" pageDesc="Writings on AI, tech, art, and history">` to `<Main pageTitle="Blog" pageDesc="Writings on AI, tech, art, and history">`
	1. In `/src/components/Header.astro`, I changed the displayed text (but *not* the `href="/posts"`) from Posts to Blog.
* Per Sat's [Readme instructions](https://github.com/satnaing/astro-paper/blob/main/src/content/blog/how-to-configure-astropaper-theme.md#configuring-site), you can change the number of posts per page by changing that value in `src/config.ts` > `postsPerPage`. Changed value from default `3` to current value of `5`.


## 9/28/2023
* The orange link color used throughout is hex #ff6b01 RGB 255, 107, 1
* I added hyperlink visibility by editing `/src/pages/index.astro`. Went to `<style>` section below and added to CSS attributes to the #hero selector. 
* links. [CSS Text Decoration Property and values](https://www.geeksforgeeks.org/css-text-decoration-style-property/)
* Hm. can't figure out why the Blight post from `2015-04-23-what-will-peace-bring.md` breaks the build at Netlify. Tried a few times around 9:45 AM. Will remove for now.

## 9/29/2023
* Created [page on fine-tuning and RAG](/ft-and-rag)
* General intro to [gen ai](https://www.youtube.com/watch?v=hfIUstzHs9A), recorded March, 2023. By Kate Soule at IBM.
	* LLMs are a subset of Foundation Model. 
	* Foundation models are trained a huge corpus (terabytes worth) of unstructured data through unsupervised training.


## 10/02/2023
* Worked on refactoring python code for colab notebook
* began incorporating head of school questions in on Tues 10/3

## 10/04/2023
* Z at the end of a timestamp = [Zulu time](http://www.ines-panker.com/2020/10/26/all-date-formats.html#:~:text=In%20code%2C%20we%20usually%20denote,for%20Z%20is%20“Zulu”.). 
	* 'UTC is a global time standard. It defined how time will be measured and coordinated between everybody. But UTC is also used as a successor of GMT (=Greenwich Mean Time) to describe the time at the 0° meridian.
	* 'In code, we usually denote it with +00:00 or with a Z. The letter Z is used for historical reasons because Z was the name of the timezone using this time. This time is also sometimes called the Zulu time since NATO’s phonetic alphabet for Z is “Zulu”.
	* 'The daylight saving time (=DST) does not affect UTC. DST simply modifies the ±[hh]:[mm]-part of the date-time: Europe’s CTE (=Central European Time) is usually described as UTC+1, but during the summer, when DST kicks in, it simply becomes UTC+2.'
* Zulu time aka UTC does *not* change with daylight savings. So you have to modify during the summer, it's PDT (Pacific Daylight savings Time) which is UTC-7 hours. And in the winter time, we use PST (Pacific Standard Time) which is UTC-8 hours. See [Wiki article on Pacific time zone](https://en.wikipedia.org/wiki/Pacific_Time_Zone) 

## 10/05
* Continued episode editing
* Idea from AK. LLM version of Moz's SEO [Whiteeboard Fridays](https://moz.com/blog/category/whiteboard-friday)
* Created new blog entries on main jeffhwang.me site for each Stepfunction episodes. Updated tags and added "Featured Articles" section back to homepage.

## 10/06
* to search for the pattern of a filename in the current directory, use the `-f` flag for `ls` per [this documentation](https://www.ibm.com/docs/de/power6?topic=commands-ls-command) which suppresses the `-l` and other flags. So this is a good way of going `ls -f | grep uffizi`. Note that no wildcard `*` is needed when using this construct.


## 10/06 - research on how to recreate a llama 7b - rlhf with chat using pure opensource
1. ask phind.com what are the basics needed to start training on hugging face and google colab
1. note that this is the [HF model](https://huggingface.co/TheBloke/Llama-2-7B-Chat-GGML) we need to try to get working. It's llama-7b with rhlf chat 
1. Found this good [Hugging Face course](https://huggingface.co/learn/nlp-course/chapter2/3?fw=pt) while researching HF AutoModels. Looks like it's useful to use it from soup to nuts. also allows usage of Google CoLab to follow along. Also created a link to [PEFT](https://huggingface.co/blog/peft) in the main [fine-tuning](/ft-and-rag) page. Also found [this documentation](https://huggingface.co/docs/trl/sft_trainer) on SFT aka Supervised Fine-Tuning Trainer class at HF. Less necessary,for now but to better understand when the code calls SFTTrainer.

## 10/07
* Set up new MBA 15-inch. migration assistant worked very well. list of post migration assistant adjustments:
	* Backblaze
	* BetterSnapTool
	* TouchID
* updated Warp on mini
* created new `/proj-7-arm64` directory
* followed usual [Astro tutorial](https://docs.astro.build/en/tutorial/1-setup/2/) instructions to place new arm64 subdirectory in `/proj-7-arm64`.
	* It installed astro v3.2.3
* Successfully registered mini with github via SSH instructions in OneNote
* Next, used these [phind.com cached instructions](https://www.phind.com/search?cache=ll73iamy3oh118rbh145icql) to pull down repo from remote github to my local mini-pro2 repo
* Lol, can't quite figure out rebase vs. fastforward and not quite working. might be a bit of a migration project down the line when i fully transition from intel to arm64!
* Transfer relevant notes over to [git page](/git-notes/)

## 10/09 Monday
* Subscribed to GPT4 and Claude from Anthropic
* Interesting [tweet](https://twitter.com/fchollet/status/1709242747293511939) and [substack post](https://fchollet.substack.com/p/how-i-think-about-llm-prompt-engineering) by F Chollet about prompt engineering and what's really happening
* Good [tweet thread](https://twitter.com/kareem_carr/status/1710661717770879099) by Kareem Carr about errors in SBF bayesian statistical thinking. 
* [Recent talk](https://jvns.ca/blog/2023/10/06/new-talk--making-hard-things-easy/) by author of unix zine [Julia Evans](https://jvns.ca/about/). [HN thread](https://news.ycombinator.com/item?id=37791002)

## 10/13
* Interesting take on the [History and evolution of computers](http://whatarecomputersfor.net). Check out 7 chapters including: [Introduction](http://whatarecomputersfor.net), [A Machine for Math](http://whatarecomputersfor.net/a-machine-for-math/), [Versatile Information Machines](http://whatarecomputersfor.net/versatile-information-machines/), [Machines for Millions](http://whatarecomputersfor.net/machines-for-millions/), The World's Knowledge, Almost Everyone, and Computers Show Us Our World.
* Good Mozilla Dev Network article on ['How web browsers work'](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work)

## 10/17
* 2019 article on [how to more deeply understand a piece of mathematics](https://cognitivemedium.com/srs-mathematics) from this [Hacker News thread](https://news.ycombinator.com/item?id=37920191)
* Trying to understand GPU features and pricing better. Some good links:
	* Tim Dettmers Jan 2023 article ['Which GPU(s) to Get for Deep Learning: My Experience and Advice for Using GPUs in Deep Learning](https://timdettmers.com/2023/01/30/which-gpu-for-deep-learning/) 
	* Full stack deep learning pricing charts for [Cloud GPUs](https://fullstackdeeplearning.com/cloud-gpus/) and associated [May 2023 Hacker News thread](https://fullstackdeeplearning.com/cloud-gpus/)

## 10/22
* Back to editing a3. Modified `/src/layouts/BaseLayout.astro` and added `<meta name="robots" content="noindex, nofollow" />` per these [Google instructions](https://developers.google.com/search/docs/crawling-indexing/block-indexing). Should cascade to all pages created on the site.
* To kill my RSS feed, I went to `/src/pages/rss.xml.js` and commented out the `export async function GET(context)` function.

## 10/23
* Simon Willison gave a talk and has a structured blog post about [embeddings](https://simonwillison.net/2023/Oct/23/embeddings/)

## 10/29
* Made some nice progress yesterday Saturday 10/28 at library on reading GBF Chapter 10 on RNNs, and skimming the two 2014 papers by Cho...Bengio on 'Paired Encoder-RNN plus Decoder-RNN'.
* More progress digging into both Chapters 6 and 10 of the GBC Deep Learning book

## 10/30
* More progress reviewing and getting deper on Chapter 6 with some skimming of chapters 7 (Regularization) and Chapter 8 (Normalization)

## 11/01
* More progress
* Reread Chap 9 history of CNNs and impact on deep learning at end of chapter
* Review of Chapter 5 concepts on capacity, over and underfitting, etc.
* more editing of SF ep 16

## 11/02
* Notes on [Hyung Won Chung's Open AI video](https://www.youtube.com/watch?v=dbo3kNKPaUA) at Seoul National University from October 5, 2023.
	* Title "LLMs (in 2023)"
	* Emergent Abilities of LLMs by Jason Wei, Yi Tay, et al (2023)
	* Perspective of 'yet'

## 11/06
* Discussion with Justin about Openness Quotient, history tradition/transformation; lumpers vs splitters, etc.
* Why is AI scary?
	* B/c we don't know the future; exponential change is hard for humans, and it might even be discontinuous
	* Focus on what is enduring. Fundamental laws. Shapiro and Varian 'Information Rules'. In addition, the math is not going to change; just the usage, recombination, application of these math concepts.
	* Are people intimidated by the 'black box' of alien technology that happens to be deep learning? What does it take to approach the box, to open it up? Luckily, this alien tech is at least carbon based so we can understand it. 
* SEL = Social Emotional Learning
* Justin -- optimism aka make decisions to benefit the world
* Topic: how much math do you really need to know?
* Modern learning
	* Upper layer -- learn Python instead of C or Scheme? e.g., learning Shakespeare
	* level below two choices: traditional CS50 is like learning Latin and Middle English.
		* In contrast, the Jeff version of math/CS is like teaching story, plot, theme, character, setting etc. by asking them about Harry Potter, Arcane anime, or whatever they like.
* Another topic: how disruptive or sustaining a new developement? Perhaps like fixed versus variable costs. Depending on time scale, most fixed costs are variable, and most variable costs are fixed.

## 11/06 - 11/12
* More progress on Chapter 5
* hand drew equation versions of point estimation from p.119, section 5.4.1.
* Got to Maximum Likelihood Estimation section
* Clean up of GBC, Chapter 5. Began delving into Chap6 Deep FeedForward Networks

## 11/13 - 11/19
* ['In the bad old days we had Punchcards. How did people deal with that?'](https://blog.computationalcomplexity.org/2023/11/in-bad-old-days-we-had-punchcards-how.html) and [HN thread](https://news.ycombinator.com/item?id=38151299)
* Wisdom from Computing's Past. [Article](https://lewiscampbell.tech/blog/231112.html) and [HN thread](https://news.ycombinator.com/item?id=38236607)
* Completed GGC Chapter 5

## More progress
* 11/19 Began Chapter 6 on Feedforward Networks
* 11/22 Began referring to AML book Learning from Data to cross reference it with Chapters 5, 6, 7 of GBC

## 11/27
* Decided to install [Alacritty Terminal emulator](https://alacritty.org) on my Mac mini M2 Pro. Did it by using DMG.
	* Step 0: First, update brew: (1) update; (2) doctor; (3) upgrade.
	* Step 1: Used homebrew to install prerequisite nerdfont using [these instructions](https://www.geekbits.io/how-to-install-nerd-fonts-on-mac/) and this command `brew tap homebrew/cask-fonts`.
	* Step 2: Looks like no NerdFonts are installed. Per [this YouTube video](https://www.youtube.com/watch?v=Mu4frtvHPOY) by Josh Medeski, I'd like to try *SFMono Nerd Font*. To install this, I used the [github instructions](https://github.com/epk/SF-Mono-Nerd-Font) by GitHub user epk who manages this font.
		* first: `brew tap epk/epk`
		* Typed the instructions for versions of Homebrew greater than 2.6.0: `brew install --cask font-sf-mono-nerd-font`
		* The *SFMono Nerd Font* is at least partially installed because when I use [this FAQ Question](https://starship.rs/faq/#why-don-t-i-see-a-glyph-symbol-in-my-prompt), the snake emoji appears when i type `echo -e "\xf0\x9f\x90\x8d"`. However, the powerline emoji does *not* appear when I type `echo -e "\xee\x82\xa0"`. Behavior seems to be the same on my 2018 5K iMac.
	* Step 3: Continuing with my the YouTube video by Josh Medeski. Two options to install Alacritty itself. (1) Download DMG from alacritty.org. (2) Or in terminal type in `brew install --cask alacritty`. 
		* I used Option 2 cmdline and got success! However, since it wasn't a properly signed app, macOS refused to open it. So then I tried Option 1 DMG install
		* Turns out this is solved by [these instructions](https://support.apple.com/guide/mac-help/apple-cant-check-app-for-malicious-software-mchleab3a043/mac). If you navigate to /Applications, you can right-click and choose open from the right-click menu and Alacritty will open. After that point, Alacritty will be saved as an exception to the Apple security rules and open properly.
	* Step 4: Copy over earlier alacrity config files to `~/.config/alacritty/` directory. Filename is `alacritty.yml`.
		* Decided to change colorscheme to `Solarized-Dark` in .yml file.
		* Success!
		* Copied *.yml file to Apple Notes.
	* Optional steps: Trying additional fonts. Decided to try the Monoid Nerd Font. Steps to apply:
		* type this in cmdline: `brew install --cask font-monoid-nerd-font` per instructions earlier [GeekBit instructions](https://www.geekbits.io/how-to-install-nerd-fonts-on-mac/). 
		* Edited `alacritty.yml` file in `~/.config/alacritty/`. Under 'Font Configuration', uncomment `family: Monoid Nerd Font`. Success!
		* Fonts successfully installed: SFMono Nerd Font, Mononoki NF, RobotoMono NF, SpaceMono NF, VictorMono NF, JetBrains Mono NF, SauceCodePro NF, Monoid Nerd Font, HeavyData NF,
		* Fonts that didn't work for some reason: Hack, UbuntuMono NF, TerminessTTF NF, CodeNewRoman NF, 
	* Current favorite on miniM2pro: **JetBrainsMono Nerd Font**
	* Current favorite on iMac-2018 Intel: **ShureTechMono Nerd Font**
	* installed also on MacBook Air 2014

## 12/02 - 12/18
* Rebuilt a7 on Apple Silicon / ARM64. still having some trouble with js for mobile hamburger interactivity. maybe the naming of Hamburger as a component?
* Almost finished! as of 11:55 pm Monday night, 12:30 am midnight early morning Tuesday Dec 5th, have blog fully up and running.
* final step is to turn on light mode / dark mode
* renamed Blog to Notes
* verified it works from miniPro, and that connection to GH is working etc.

## 12/19 - 12/26
* Built new section for utopian/Scientific
* Mostly done with Chap 6 FF. Need to start with Chap 7 on Regularization
* refactored Eng s: us section
* built out NIS section and added links
* Began experimenting with having by-reference calls within a \*.md file to the frontmatter in that same Markdown document. More reading in [this Astro documentation](https://docs.astro.build/en/core-concepts/layouts/)
* More on Pas Chapter 4 -- almost completed

## 12/27-12/31
* [HN thread](https://news.ycombinator.com/item?id=38781484) on Dwarkesh Patel's Substack article ['Will Scaling Work?'](https://www.dwarkeshpatel.com/p/will-scaling-work). For more notes, see a7/ht section. 

***
## 2024 Comp Notes

## 1/01/2024
* Per advice of this [Verge article](https://www.theverge.com/23591533/mac-remap-keyboard-how-to), installed [Karabiner Elements](https://github.com/pqrs-org/Karabiner-Elements). Not via homebrew, just through .dmg installer from [official website](https://karabiner-elements.pqrs.org).
	* Per [documentation](https://karabiner-elements.pqrs.org/docs/getting-started/installation/), need to go to System Preferences > Login Items and allow in background. Displays as 'Fumihiko Takayama' in Login Items.
	* Allow system software which provides virtual devices for Karabiner-Elements
	* Grant System Preferences > Privacy and Security > Input Monitoring to Karabiner-Elements

## 1/03
* On minipro, transitioned Alacritty from alacritty.yml file to alacritty.toml file by running the `alacritty migrate` command. After that, Alacritty kept throwing warnings on start. To elimate the problem, i commented out and/or deleted the schemes and window opacity fields b/c they were used in \*.yml but not in \*.toml. Legacy versions are still saved in ~/.config/alacritty.  See also:
	* [Issue #7000](https://github.com/alacritty/alacritty/pull/7000)
	* This text `Versions before 0.13.0 used a YAML configuration file. Old YAML config files can be converted to TOML by running alacritty migrate. However, automatic migration drops all comments.` from [this page](https://wiki.archlinux.org/title/Alacritty#:~:text=Old%20YAML%20config%20files%20can,found%20at%20the%20project%27s%20homepage.)

## Daily
* 1/04 - renamed a4-paper to ar-paper-intel
* 1/05 - v1 of AI-timeline
* 1/06 - added clean, fast version of intro and chap 1 Pas
* 1/08 - macros in vim
* 1/09 - cleaned up all italics and JH Breaks for Intro, Chap 1, Chap 2, and Chap 3. Deleted jeffhwang-a3.netlify.app from public web. Intel Mac + Astro in /a3.
* 1/11 - completed GBC chap 7 regularization; moved onto chap 8 on optimization
* 1/13, 1/20 - more on GBC chap 8 optimization

## 1/07 Using Markdown-like syntax to create simple graphs
* [Pikchr](https://pikchr.org/home/doc/trunk/homepage.md) by the people behind SQLite. Created in 2020, to update 1980s PIC format.
	* [Differences from PIC](https://pikchr.org/home/doc/trunk/doc/differences.md)
	* [Jan, 2024 HN thread](https://news.ycombinator.com/item?id=38885094) and [Sept, 2023 HN thread](https://news.ycombinator.com/item?id=36847133)
* [Mermaid](https://mermaid.js.org/intro/) is a JavaScript based diagramming and charting tool built by [Mermaid Chart](https://www.mermaidchart.com/pricing) for-profit company
* [HN comment](https://news.ycombinator.com/item?id=24603608) comparing [Graphviz](https://graphviz.org/about/) which started in 2004 on Mac.

## 1/17 Getting llm working with seymour
* Ignored setting up Jupyter Notebook from [this LangChain section](https://python.langchain.com/docs/get_started/quickstart#setup) which pointed to this [Jupyter install guide](https://jupyter.org/install)
* Looking at OneNote notes from 4/02/2023 on setting up conda environments
	1. See what mamba environments are available by typing `mamba info --envs`
	1. See what packages are installed in a given environment: `mamba list` while in the desired env.
	1. verified that all conda/mamba environments are properly updated by typing `mamba update --all`
		1. I had to do this for all of my environments: `base`, `jupyter`, and `pytorch`.
	1. decided to rename the existing environment `jupyter` into `langc`
		1. used [this command](https://docs.conda.io/projects/conda/en/latest/commands/rename.html) to rename
		1. typed: `conda rename --name jupyter langc`
		1. Note: Have to use `conda` because `mamba` does not suppport the *rename1. sub-command
	1. How to inspect or change the version of python being used in an environment
		1. Just navigate to whichever environment you are in and type `python --version`. Currently on Python 3.10.13 on all 3 envs. See also [this script](https://stackoverflow.com/questions/43168264/which-python-version-is-installed-in-another-conda-env#comment127442114_52408794) to view the python version for all envs at once. Note that this is the macOS version b/c the original answer only works with linux + latest version of xargs.
			* `conda env list | grep -v "^$\|#" |awk '{print $1;}'|xargs -I{} -n 1 sh -c 'printf "Env: {}\t"; conda list -n {} |grep "^python\s";'`
* Successfully changed python version *only* for the `langc` mamba environment. Steps:
	1. Navigate to desired env--in this case `langc` by typing: `mamba activate langc`.
	1. **Important**: If you started with mamba to install python, you have to continue. Switching from conda to mamba midstream will cause errors. Simply type: `mamba install python=3.11` where desired version is **3.11**
* Next, installed langchain with this command: `mamba install -n langc -c conda-forge langchain`.
	* **-n** indicates which env i'm installing into. In this case, it's the conda env i created called `langc`
	* **-c** indicates which channel to pull from. In this case, I'm pulling from `conda-forge`.
	* the name of the package is simply `langchain`.
	* Note that this also installs langsmith

### pip usage to install langchain-openai

* [Using these instrctions](https://python.langchain.com/docs/get_started/quickstart#llm-chain), i got going with building on OpenAI api. Make sure you are in the `langc` env when you do the following
	1. Import the LangChain x OpenAI integration package: `pip install langchain-openai`
	1. Create a `.env` file and store it in root aka `\demo_files\proto-dev\.env`. Add a single line into it with the key-value pair: `openai_api_key='...'`. Entered this command:
		* `(langc) [18:06:55 /demo_files/protodev-llm/sndbx_lngchn]:python3 lng-simple.py`
	1. and got this error
		* ```/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/langchain/chat_models/__init__.py:31: LangChainDeprecationWarning: Importing chat models from langchain is deprecated. Importing from langchain will no longer be supported as of langchain==0.2.0. Please import from langchain-community instead:```
		* ``` `from langchain_community.chat_models import ChatOpenAI`.```
		* ```To install langchain-community run `pip install -U langchain-community`.warnings.warn(```
		* ```Traceback (most recent call last): File "/Users/jeffh/demo_files/protodev-llm/sndbx_lngchn/lng-simple.py", line 14, in <module> from dotenv import load_dotenv, find_dotenv```
		* ```ModuleNotFoundError: No module named 'dotenv'```

## 1/18 continuation. Additional python modules installed via Mamba
* need to install `dotenv` python package. typed `mamba install -n langc -c conda-forge python-dotenv`
	* this module helps find `.env` files for key-value pairs
* need to install `panel` python package. typed `mamba install -n langc -c conda-forge panel`
* Another error occurred b/c the keyvalue pair in `.env` needs to be all-caps. so it looks like this:
	* OPENAI_API_KEY='sk-...'
## Next packages: Streamlit, Chroma vector db, 
* For streamlit related scripts located in `/protodev-llm/agnt_mednec_proto/`, need to install `streamlit` python package. typed `mamba install -n langc -c conda-forge streamlit`
* For Chroma DB related scripts located in `/protodev-llm/agnt_mednec_proto/`, need to install `chromadb` python package. typed `mamba install -n langc -c conda-forge chromadb`
* After this, got this error:
```
python3 *retrieve-v2.py
/Users/jeffh/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/langchain/vectorstores/__init__.py:35: LangChainDeprecationWarning: Importing vector stores from langchain is deprecated. Importing from langchain will no longer be supported as of langchain==0.2.0. Please import from langchain-community instead:

`from langchain_community.vectorstores import Chroma`.

To install langchain-community run `pip install -U langchain-community`.
  warnings.warn(
/Users/jeffh/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/langchain/chat_models/__init__.py:31: LangChainDeprecationWarning: Importing chat models from langchain is deprecated. Importing from langchain will no longer be supported as of langchain==0.2.0. Please import from langchain-community instead:

`from langchain_community.chat_models import ChatOpenAI`.

To install langchain-community run `pip install -U langchain-community`.
  warnings.warn(
/Users/jeffh/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/langchain_core/_api/deprecation.py:117: LangChainDeprecationWarning: The class `langchain_community.embeddings.openai.OpenAIEmbeddings` was deprecated in langchain-community 0.1.0 and will be removed in 0.2.0. An updated version of the class exists in the langchain-openai package and should be used instead. To use it run `pip install -U langchain-openai` and import as `from langchain_openai import OpenAIEmbeddings`.
  warn_deprecated(
/Users/jeffh/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/langchain_core/_api/deprecation.py:117: LangChainDeprecationWarning: The class `langchain_community.chat_models.openai.ChatOpenAI` was deprecated in langchain-community 0.0.10 and will be removed in 0.2.0. An updated version of the class exists in the langchain-openai package and should be used instead. To use it run `pip install -U langchain-openai` and import as `from langchain_openai import ChatOpenAI`.
  warn_deprecated(
2024-01-18 19:29:36.963
  Warning: to view this Streamlit app on a browser, run it with the following
  command:

    streamlit run proto-retrieve-v2.py [ARGUMENTS]
2024-01-18 19:29:36.963 Session state does not function when running a script without `streamlit run`
Traceback (most recent call last):
  File "/Users/jeffh/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/streamlit/runtime/state/session_state.py", line 398, in __getitem__
    return self._getitem(widget_id, key)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/Users/jeffh/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/streamlit/runtime/state/session_state.py", line 443, in _getitem
    raise KeyError
KeyError

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/jeffh/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/streamlit/runtime/state/session_state_proxy.py", line 119, in __getattr__
    return self[key]
           ~~~~^^^^^
  File "/Users/jeffh/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/streamlit/runtime/state/session_state_proxy.py", line 90, in __getitem__
    return get_session_state()[key]
           ~~~~~~~~~~~~~~~~~~~^^^^^
  File "/Users/jeffh/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/streamlit/runtime/state/safe_session_state.py", line 91, in __getitem__
    return self._state[key]
           ~~~~~~~~~~~^^^^^
  File "/Users/jeffh/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/streamlit/runtime/state/session_state.py", line 400, in __getitem__
    raise KeyError(_missing_key_error_message(key))
KeyError: 'st.session_state has no key "show_results". Did you forget to initialize it? More info: https://docs.streamlit.io/library/advanced-features/session-state#initialization'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/jeffh/demo_files/protodev-llm/agnt_mednec_proto/proto-retrieve-v2.py", line 90, in <module>
    if st.session_state.show_results:
       ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/Users/jeffh/demo_files/mambaforge/envs/langc/lib/python3.11/site-packages/streamlit/runtime/state/session_state_proxy.py", line 121, in __getattr__
    raise AttributeError(_missing_attr_error_message(key))
AttributeError: st.session_state has no attribute "show_results". Did you forget to initialize it? More info: https://docs.streamlit.io/library/advanced-features/session-state#initialization

```

### only items installed via pip
* langchain-openai
	* had to install this via pip b/c it's not avilable at conda-channel. So when i typed `mamba install -n langc -c conda-forge langchain-openai`

## Daily
* 1/21 - planned next GBC chapters
* 1/24 - Work on mindscale/labs  

## 1/24 More notes
* [HN thread](https://news.ycombinator.com/item?id=39119835) about fast, Rust-based editor Zed going [open-source](https://zed.dev/blog/zed-is-now-open-source). Currently [macOS only](https://zed.dev/faq), on road-map to [support Linux](https://news.ycombinator.com/item?id=39120029) by 2025. 

## 2/15
* New generation of data apps using [Framework](https://observablehq.com/framework/) from [Observable](https://observablehq.com). [Blog post](https://news.ycombinator.com/item?id=39383386) and [HN thread](https://observablehq.com/blog/observable-2-0)
* Began reading O'Reilly's [Unix Power Tools](https://www.amazon.com/Power-Tools-Third-Shelley-Powers/dp/0596003307). Feel like `ls | grep "search string"` works well. and doesn't even need any wildcards! to filter blog by date, etc.

## 2/16
* New generation of data apps using [Framework](https://observablehq.com/framework/) from [Observable](https://observablehq.com). [Blog post](https://news.ycombinator.com/item?id=39383386) and [HN thread](https://observablehq.com/blog/observable-2-0)

## 2/20
* InfoQ article on [Cloud-Computing in the Post-Serverless Era](https://www.infoq.com/articles/cloud-computing-post-serverless-trends/)
* IEEE 2016 article on [The Surprising Story of the First Microprocessors](https://spectrum.ieee.org/the-surprising-story-of-the-first-microprocessors). Hint: It actually didn't start with the [Intel 4004](https://en.wikipedia.org/wiki/Intel_4004) in 1971.
* [HN post](https://news.ycombinator.com/item?id=39147528) to a Medium article about 'Is Cloud the New Mainframe?'.
* [HN thread](https://news.ycombinator.com/item?id=39197619) about Ben Thompson's Stratechery post on [Intel's Humbling](https://stratechery.com/2024/intels-humbling/)

## 2/24
* New course at Purdue University on [Semiconductor Fabrication 101](https://www.purdue.edu/newsroom/releases/2022/Q2/purdue-launches-nations-first-comprehensive-semiconductor-degrees-program.html) and [HN thread](https://news.ycombinator.com/item?id=39325659)
* Brief history and tour of [C Compilers](https://www.deusinmachina.net/p/compiling-history-a-brief-tour-of) and earlier [history of C programming language](https://www.deusinmachina.net/p/compiling-history-a-brief-tour-of)

## 3/18
* [HN thread](https://news.ycombinator.com/item?id=39720388) about CMU's [CS251 course](https://www.cs251.com) on Great Ideas in Theoretical Computer Science.
* Hugo Barra's long and detailed review and thoughts on AVP from the perspective of a previous head of FB/Meta's Oculus and VR projects. [Article](https://hugo.blog/2024/03/11/vision-pro/) and [HN thread](https://news.ycombinator.com/item?id=39711725).
* Is the Internet Dying? [Ed Zitron's thoughts](https://www.wheresyoured.at/are-we-watching-the-internet-die/), [Cory Dransfeldt's blog](https://coryd.dev/posts/2024/the-internet-isnt-dying-its-changing/), and [HN thread](https://news.ycombinator.com/item?id=39684795)

## 7/08/2024
* Useful [commandline keyboard shortcuts](https://jvns.ca/blog/2024/07/08/readline/) from Julia Evans. [HN Thread](https://news.ycombinator.com/item?id=40907581). The *bash terminal* is using `readline` which offers these standard shortcuts:
1. `Ctrl+a` to go to the beginning of the line. 
1. `Ctrl+e` to go to the end of the line. 
1. `Ctrl+w` to delete the previous word
1. `Ctrl+u` to delete the entire line.

## 7/25/2024
* Reflections on last month of JS learning.
* Started in earnest around 6/21/2024.
* Since then, significant progress through SVP and Flanagan. Am currently in a bit of a slog through client-side JS because I am adding new info about HTML (e.g., going deeper on HTML `<div>` ), and going deeper on CSS.
* On 7/24, purchased paper copy of Jennifer Robbins' [Learning Web Design, 5th ed](https://www.oreilly.com/library/view/learning-web-design/9781491960196/) from 2018.
* Watched next steps for a frontend dev in 2024-2025. This [March, 2024](https://www.youtube.com/watch?v=EzTxYQmU8OE) video by ByteGrad has what seems like reasonable advice. Also from BytGrad, two series to look at regarding CSS Grid vs Flexbox:
	* [7-minute flexbox tutorial](https://www.youtube.com/watch?v=y_taUkBEouU) from 2022.
	* [9 Layout Example on Flexbox](https://www.youtube.com/watch?v=xN1BkNItTRk&t=82s) from 2023. 40-minute Crash Course by ByteGrad.
	* Not from ByteGrad is this tutorial From Feb, 2023 -- [CSS Grid vs. Flexbox](https://www.simplilearn.com/tutorials/css-tutorial/css-grid-vs-flexbox#:~:text=CSS%20Grid%20provides%20two%2Ddimensional,axis%2C%20either%20horizontally%20or%20vertically.)

## 9/06/2024
* [The Good, The Bad, The Ugly of LSPs](https://www.michaelpj.com/blog/2024/09/03/lsp-good-bad-ugly.html) by Michael Peyton Jones, who works on the Haskell LSP. [HN thread](https://news.ycombinator.com/item?id=41440275) 

## 10/09/2024
* During Dinner with Melih in Brooklyn (Buffalo Wild Wings nr the Barclay's Center) earlier this week (Monday 7 Oct), I was reminded of this [presentation by Maggie Appleton](https://maggieappleton.com/home-cooked-software) about Home-Cooked Software and Barefoot Programmers.
    * First saw this on [HN news](https://news.ycombinator.com/item?id=40633029) back in June, 2024 but i guess I never linked it. 
    * Saving here to make it easier to find local first software content.

## 11/2024
* [HN thread](https://news.ycombinator.com/item?id=41717543) about [What is P vs. NP about](https://vasekrozhon.wordpress.com/2024/08/18/what-p-vs-np-is-actually-about/)
* [2024 HN thread](https://news.ycombinator.com/item?id=41684082) about this 2022 post about how [too much efficiency makes things worse](https://sohl-dickstein.github.io/2022/11/06/strong-Goodhart.html) 

## 11/27/2024
* Refound this old resource that uses GPT-3 to summarize arXiv papers. Hasn't been updated since March 2023, looks like. [arXiv-summary](https://www.arxiv-summary.com/archive/)

## 12/30/2024
* [Beginner article on SQLite](https://avi.im/blag/2024/sqlite-facts/) with history, overview, and significance. [HN thread](https://news.ycombinator.com/item?id=42549807) and [PDF of SQLite: Past, Present, Future](https://www.vldb.org/pvldb/vol15/p3535-gaffney.pdf) by Gaffney, D. Richard Hipp (aka *DRH* co-creator), et al. from 2022.

## 1/10/2025
* Three part blog mini-series on AI Tooling for Software Engineers in 2024: Reality Check at Gergely Orosz's *The Pragmatic Engineer* blog:
	* [Part 1](https://newsletter.pragmaticengineer.com/p/ai-tooling-2024)
	* [Part 2](https://newsletter.pragmaticengineer.com/p/ai-tooling-part-2)
	* [Part 3](https://newsletter.pragmaticengineer.com/p/ai-tooling-part-3)
* Interesting conversation with the first developer for Apple's v2 of [Rosetta](https://en.wikipedia.org/wiki/Rosetta_(software)) that was released in 2020 to help transition from Intel to Apple Silicon. Dev is [cwzwarich](https://news.ycombinator.com/item?id=42484409), who wrote most of the first version of Rosetta 2. 
	* **Thread on reading SICP** starting [here](https://news.ycombinator.com/item?id=42488464) from the [HN article](https://news.ycombinator.com/item?id=42483895) about Cameron Zwarich leaving Apple to go work at the [Lean FRO](https://lean-fro.org/about/). 
    
## 2/13/2025
* Going to write a small JS program to auto-format new blogposts. See `/astro` page for more.

## 3/12/2025
* Remember
