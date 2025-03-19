---
title: Sed Notes
permalink: /sed/
---

## 7/09/2023
* Began reading links about **sed** (for stream processing) and **awk** (for delimited columns by Aho, Weinberger, and Kernighan).
* (Reviewed these [two](https://www.softwaretestinghelp.com/unix-filter-awk-sed-commands/#:~:text=Unix%20provides%20sed%20and%20awk,well%20with%20delimited%20field%20processing.) [links](https://www.makeuseof.com/tag/sed-awk-learn/) again on 8/22. Best to use other sed reources b/c these are very basic.)
 
## 7/11 
* More links on sed from Hacker News:
	* Grymoire's [Intro and Tutorial for Sed by Bruce Barnett](https://www.grymoire.com/Unix/sed.html) and associated [2015 HN thread](https://news.ycombinator.com/item?id=8851124) with a [comment about Grymoire's similar awk tutorial](https://news.ycombinator.com/item?id=8853658). Plus Grymoire's [grep tutorial](https://www.grymoire.com/Unix/Grep.html)
	* [Differences between grep, sed, awk from Linode](https://www.linode.com/docs/guides/differences-between-grep-sed-awk/#the-differences-between-grep-sed-and-awk) and [2023 HN thread](https://news.ycombinator.com/item?id=34280281)
	* [Gnu Sed manual and tutorial](https://www.gnu.org/software/sed/manual/sed.html)
	* Casual [quick notes on sed](https://github.com/adrianlarion/useful-sed) with associated [2021 HN thread](https://news.ycombinator.com/item?id=29196221). Note that there may be errors in some of these sed scripts.

## 7/12 
* More sed links: 
	* Good sed exercises at [50 sed examples](https://linuxhint.com/50_sed_command_examples/). Began going through more seriously on 8/23.
	* <del>This might be a better [set of 10 sed examples](https://www.makeuseof.com/sed-examples/)</del>. *Completed this on 8/23.*

## 7/13
* Reflections. GNU sed (invoked by gsed) works better than core utils sed that comes prepackaged with macOS. Important to use single quotes (') rather than double quotes("). And ability to chain regexps with a semi-colon (;) sequentially is pretty useful to keep patterns distinct. Although probably hard to maintain..
* Best video so far on [sed by Luke Smith](https://youtu.be/QaGhpqRll_k)

## 8/07
* More sed resources (see also Notes app):
	* From 2008 or so but updated since then. [Sed-one-liners](https://catonmat.net/worlds-best-introduction-to-sed), associated [text files with all one-liners](https://catonmat.net/wp-content/uploads/2008/09/sed1line.txt) and associated [HN comment](https://news.ycombinator.com/item?id=2431264). It's the first chapter of a $20 e-book [Sed One-Liners Explained](https://catonmat.net/sed-book). Note that catonmat = [Peter Krumins](https://catonmat.net/about), co-founder of Browserling.com. And these one-liners were originally compiled by [Eric Pement](https://www.pement.org/sed/)
	* From the same 2011 thread on [Sedtris: Tetris in sed](https://news.ycombinator.com/item?id=2430171) where the above catonmat one-liner article appeared, also found this [2008 other side of the moon Progamming Patterns in sed](https://tech.bluesmoon.info/2008/09/programming-patterns-in-sed.html)
* Completed Luke Smith video from 7/12.
* Began experimenting with catonmat's [first chapter](https://catonmat.net/worlds-best-introduction-to-sed)

## 8/08
* Hm, perhaps look at the sed resources at [Eric Pement's site](https://www.pement.org/sed/)
* On second thought, i think grymoire's original [Bruce Barnett's Sed intro and tutorial](https://www.grymoire.com/Unix/Sed.html) is the better way to go.

## 8/09
* Finished to the end of the flag section in Grymoire site, aka the section titled ['Write to a file with /w filename'](https://www.grymoire.com/Unix/Sed.html#toc-uh-10)
* Finished up to end of the ['Multiple commands witn an -command' section](https://www.grymoire.com/Unix/Sed.html#uh-13). Next section is 'Filenames on the command line'.

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

## 8/17
* Tried duos of 'history', 'British', and 'local' in 4-test.md input file and used gsed command to remove them one at a time. Now need to have a generic regex that can remove n duplicated words.

## 8/18 sed
* After experimentation, I realized that using the **-r** flag to activate Extended Regular Expressions (ERE)  is critical to getting regex working well with gsed. 
* With that flag turned on, can use parentheses to create numbered capturing groups. For awhile, I could use gsed without the -r flag turned on; I was able to capture patterns in groups with parentheses just by making sure I properly escaped those parens with a backslash like so \\(. However, I got inconsistent results. 
* In the end, the best bet was to just turn on **-r** like this:
		`gsed -nr 's#\b(\w+)\b \b\1\b#\1  ~~~ \1#gp' source.txt >out.txt`
* The above example uses **-n** to suppress automatic printing. Other notes:
	* The **gp** options at the end ensure respectively: (1) that all instances per line are executed on (globally), NOT just the first instance; and (2) p means print each line where a line matches indicated pattern and is worked upon.
	* I'm using hash-marks (#) instead of the usual forward slash (/) as delimiters. 
	* I'm using **\\b** as word-boundaries. 
	* The '~~~' symbol shows how to visually see where i've inserted something into the doubled space.

## 8/19
* Next step, try doing case insensitive substitutions using ['s/the/the the/I' from this section](https://www.grymoire.com/Unix/Sed.html#uh-10a)
* When using shuf to shuffle contents of /zhongwen, make sure to use the -o option to indicate output file, e.g., 
		`shuf source.txt -o output.txt`

## 8/22 
* [Short blog post](https://utcc.utoronto.ca/~cks/space/blog/unix/UnixTechnologyAndIdea) about Unix as a technology and as an idea. [HN thread](https://news.ycombinator.com/item?id=37205536)
* Purchased Peter Krumins' (catonmat) e-book [*Sed One-Liners Explained*](https://catonmat.net/sed-book). See Box.

## 8/23
* Next two examples from [this 10 examples article](https://www.makeuseof.com/sed-examples/) that I referenced on 7/13.
	1. Interesting and quick way to doublespace a single-spaced file. i.e., add a blank line after each line. 
		`gsed 'G' 1-indigenous-test.md >out.txt`
	1. To add two blank lines in between each line, add another expression with a semi-colon.
		`gsed 'G;G' 1-indigenous-test.md >out.txt`
* Next several examples from [this 50 examples article](https://linuxhint.com/50_sed_command_examples/#s9) starting with Example #9. Referenced on 7/12.
	1. In addition to defining ranges (i.e., only execute this for lines 5-20'), one can set a pattern to look for before executing the action. For example, the one-liner below will only replace lowercase 'the' with uppercase "THE' when the line contains "These" with a capital T.
		`gsed -nr '/These/ s/the/THE/gp' 2-indigenous-test.md >out.txt`
	1. Also, the pattern for 'These' can accept regex syntax. So if we want to execute this substitution on lines for both 'These' and 'these', we can search for (T|t)
		`gsed -nr '/(T|t)hese/ s/the/THE/gp' 2-indigenous-test.md >out.txt`
	1. Unfortunately, the initial pattern does not allow flags so something like `/These/i` would not work. *BUT* the i flag when added to the g (global) and p (print) flags will pattern match for case insensitive the/The. And it will be case-insensitive for 't', 'h', and 'e'.
		`gsed -nr '/(T|t)hese/ s/the/THE/gpi' 2-indigenous-test.md >out.txt`
	1. Conversely, if you want to apply something to all the lines that **don't** have a 'These' in it, you can just add a **!** flag like so /These/!:
		`gsed -nr '/These/! s/the/THE/gpi' 2-indigenous-test.md >out.txt`

## 8/26 Peter Krumins' [Sed One-Liners](https://catonmat.net/sed-book)
* **2.6** Insert a blank line below every line that matches a */pattern/*. 
	* PK's example:
		`gsed -r '/pattern/G'`
	* Jeff's example from hist-ss NYer article:
		`gsed -r '/Constable/G' gopnik-2023-dalle.md >out.txt`
	* Note that the explanation for the **G** flag comes from **Example 2.1**.
* **2.9** Duplicate all lines
	* PK's example:
		`gsed -r 'p'`
	* Jeff's example from hist-ss NYer article:
		`gsed -r 'p' gopnik-2023-dalle.md >out.txt`
* **3.1** Number each line of a file
	* PK's example:
		`gsed = filename | sed 'N;s_\n_\t_'` where _ is used as delimiter instead of usual /.
	* Jeff's example from hist-ss NYer article:
		`gsed = gopnik-2023-dalle.md | gsed 'N;s_\n_\t_' >out.txt`
	* *Note: This example calls sed twice with a pipe. Instance 1 loads the file using the **=** operator. And instance two searches for new lines and replaces them with tab characters.* 
* **3.4** Count number of lines in file *aka* simulate 'wc -l'
	* PK's example:
		`gsed -n '$='`
	* Jeff's example from hist-ss NYer article:
		`gsed -n '$=' gopnik-2023-dalle.md >out.txt`

## 8/29 PK book
* Up to 4.11 on p. 20.
* Note. the **-E -r --regexp-extended** flags are all equivalent and turn on extended regular expressions.
* p. 1-3. There are four spaces: **(1)** Input Stream,**(2)** Output Stream, **(3)** Pattern Space, and **(4)** Hold Buffer.
	* Jeff's example from hist-ss NYer article:
		`gsed -n '$p' gopnik-2023-dalle.md >out.txt`
		* This uses the fact that **$** means both the end of a line and the *last line* of a file. In this case, sed will output just the final line of file.
		* However, '^p' does not seem to print the first line.
* p. 4-5. Instead of specifying a single page (or a range of lines in the form *10,25p*), you can specify a pattern. So for example, let's just operate on the lines where there are three hashmarks at the beginning.
	* This works well against a copy of my zhongwen.md file.
		`gsed -n '/###/p' 8-zhongwen-test.md >out.txt`
	* The only problem is that in addition to grabbing the H3 level "Lessons 1-40" lines, it also captures the H4 line `#### 6/25 - 99 Ranch and Liang Mama with J`. Despite multiple experiments, I can't seem to exclude that line. Something about spaces, \s, and \w, are still not working.
	* Next, we can not only print out a list of Lesson headings, we can apply a regex like so:
		`gsed -n '/###/ s/Lesson/Chapter/p' 8-zhongwen-test.md >out.txt`
	* The above sed line works and replaces each instance of Lesson with Chapter. Also, since it is only matching lines with 'Lesson', the *99 Ranch* line is suppressed from printing in the output file.
* p. 5. One can also specify a range between two patterns. I don't have a replacement working yet but I can at least print specifically the passsage between the two regexs like so:
		`gsed -n '/Seine/,/New York City/p' gopnik-2023-dalle.md >out.txt`
	* This captures all lines beginning with the one that has *Seine* and ending with the one that has *New York City*.

## 8/30 PK book
* **2.2** Double-space a file which already has blank lines in it. 
	* PK's example:
		`gsed '/^$/d;G'`
	* JH's version executed in h-ss directory:
		`gsed '/^$/d;G' gopnik-2023-dalle.md >out.txt`
	* Comments: From the semi-colon, we see there are actually two expressions. First, search for a pattern,(*aka* there is no s/find/replace/ needed). In this case, the */pattern/* being searched for is just a blank line indicated by *^$*. Second, use the **G** command to add a blank line to every line so the whole file is double-spaced.

* **2.4** Undo double spacing
	* PK's example:
		`gsed 'n;d'`
	* JH's version executed in h-ss directory:
		`gsed 'n;d' gopnik-2023-dalle.md >out.txt`

* **2.5** Insert a blank line above every line that matches */pattern/*
	* PK's example:
		`gsed '/pattern/{x;p;x}'`
	* JH's version executed in h-ss directory:
		`gsed '/pattern/{x;p;x}' gopnik-2023-dalle.md >out.txt`
	* This works but I explore it more below.

## 9/01 PK Book
* **2.5** Search for /pattern/ and only print lines that contain that pattern
	* JH's v1
		`gsed -n '/pattern/p' e1-old-DELETE.md >out.txt`
	* JH's v2
		`gsed -n '/ultimately/p' e1-old-DELETE.md >out.txt`
	* Comments: this is a simplifed version of PK's earlier example `gsed '/pattern/{x;p;x}'`
	* need to understand use of curly braces and the swap coming from the x command better.

* **2.5** New modified version that suppresses all printing and *only* prints out the matched pattern
	* JH's v2
		`gsed -n '/Capital/{x;p;x;p}' e1-old-DELETE.md >out.txt`
	* Comments: Let's think about what's happening here. PK's original 2.5 feeds in a line into the pattern space and stops when it encounters the \\n newline character. Then, the **x** command exchanges the contents of the *pattern space* into the *hold space*. This means that the pattern space is now empty. Next, the **p** comand outputs whatever is in the pattern space which is nothing aka empty. This creates a new line. Then, the **x** command swaps what was in the hold space *back* into the pattern space. The final **p** command means, print whatever is in the pattern space, which was the line we had stored.
		* Note that it only activates this sequence of commands for lines that match the pattern specified at the beginning.
		* and of course, turning on the **-n** flag suppresses all line output. So the only lines printed are those where the **p** command is fired.

* **2.6** Insert blank line below every line that matches */pattern/*
	* PK's example which works as advertised. 
		`gsed '/regex/G`
		* Comments: Remember **capital-G** appends a new line \\n to the pattern space and then appends over whatever is in the hold buffer to the pattern space. 
		* Since the hold buffer is always empty, this has the effect of adding a newline (aka blank line) at the end of the pattern buffer. 
		* So everytime this regex is matched, at the end of the loop it will print the entire line that contained the regex as well as an additional blank \\n at the end of it.
	* JH's v1. 
		`gsed '/Four/G' e1-old-DELETE.md >out.txt`
		* Comments: (1) Prints all lines because **-n** flag is not turned on. 
		* (2) For those lines that contain the pattern *Four*, append a \\n newline as well as the (empty) contents of the hold buffer. 
		* Resut: Reprints entire input file but has added a blank line below the relevant matching lines in the Fourier section.
	* JH's v2. 
 		`gsed -n '/Four/{G;p}' e1-old-DELETE.md >out.txt`
		* Required some experimentation but got the **-n** suppression and **p** working. i.e., out.txt only contains a few lines b/c all other lines are not captured by the regex pattern.
	* Note, a good explanation of the g versus G commands when moving data from hold buffer to pattern space at Grymoire's site in [this section](https://www.grymoire.com/Unix/Sed.html#uh-57).

## 9/03 PK Book
### Example 2.8 - Join all lines in the input file
* PK's example:
		`gsed ':a; $s_\n_ _g; N; ba'` 
* JH's example:
	`gsed ':a; $s_\n_ _g; N; ba' gopnik-2023-dalle.md >out.txt` 
	* Note: uses **underscore _** instead of the usual **forward-slash /** delimiter.
	* Tested and works
	* label an expression **:a** and can refer to it with the *branch* notation **ba**. 
* Comments: I don't fully understand syntax and control flow here. Key point is that the `$s_  _   _g` statement only executes *once*, when it encounters the final line of the file as indicated by the **$** symbol.
* Suggest playing with other examples of branches before coming back to this.

### Example 4.12 - Align lines right on a 79-column width (p.20)

* PK's original example:
	`gsed -e :a -e 's_^.\{1,78\}$_ &_' -e ta` 
* JH's v1 example:
	`gsed -e :a -e 's_^.\{1,78\}$_ &_' -e ta gopnik-2023-dalle.md >out.txt` 
	* As usual, using **underscore _** as delimiter rather than the usual grep **forward slash /**
	* Tested and works. Need to try again with a text files where everything has less than 75 chars per line.
	* OK, new version using all input files having less than 75 characters in it already looks cleaner. Works even better than v1.
* JH's v2 example:
	`gsed -e :a -e 's_^.\{1,78\}$_ &_' -e ta gopnik-test.md >out.txt` 
	* v1 logic is exactly the same as v2. Only difference is the content in the input file
	* If you want to learn more about the **t branch** command, look at **A.19** in the Apppendix on the t command. Also, the entry for *t command* in the Index lists all the one-liners that use t:
		1. Example 4.12, p.20
		1. Example 4.24, p.28
		1. Example 4.25, p.29
		1. Example 6.4, p.56
* JH's v3 example:
	`gsed -e :a -e 's_^.\{1,85\}$_ &_' -e ta gopnik-test.md >out.txt` 
	* v3 is the same as v2 except now the columns are 85 chars wide, not 79 chars.

## 9/04 Understanding the execution cycle to better use b, t, and T commands
### Reading the GNU sed manual
* When sed documentation refers to 'the cycle', they are referring to [the execution cycle](https://www.gnu.org/software/sed/manual/sed.html#Execution-Cycle). i.e., (1) reading character by character from the input stream: (2) stopping the stream when it encounters a \\n newline character; (3) placing everything that was in the input stream up to--but **not including**-- the \\n in the pattern space; (4) Then executing commands upon the content in the pattern space; (5) When the last command is finished executing for this cycle, the contents of the pattern space are automatically printed out to the output stream **unless the -n suppression flag is turned on**; and (6) finally, a new \\n character is added. Thus, the cycle for this one line is complete and sed moves onto the next line in the input file.
	* Note, in step (4) above, each command can have a distinct address associated iwith it; addresses are a kind of condition code, and a command is only executed if the condition is verified before the command is to be executed.
	* Unless special commands (like **D**) are used, the pattern space is automatically deleted in between each execution cycle. 
	* In contrast, the hold buffer will keep its data between cycles unless otherwise directed.

### Revisiting PK example 2.8
* How does this sed program join all the lines in a file into one long line? Let's decompose each statement.
		`gsed ':a; $s_\n_ _g; N; ba' gopnik-test.md >out.txt` 
* Again, I'm using **underscores _** instead of the usual **forward slash /** to delimit the substitution command. Aka *s_ _ _g* instead of *s/ / /g*.
* Next, I'm going to edit the label and use `TOP` instead of `a` to avoid confusiong `:a` with the [sed commands](https://www.gnu.org/software/sed/manual/sed.html#Common-Commands) `a` and `a\\` for appending text after a line. 
		`gsed ':TOP; $s_\n_ _g; N; bTOP' gopnik-test.md >out.txt` 
* The entire list of commands consists of 4 expressions:
	1. `:TOP`
	1. `$s_\n_ _g`
	1. `N`
	1. `bTOP`
* Followed by the input file and the output location out.txt.
* Let's assume that input file just has four lines:
	Line 1
	Line 2
	Line 3
	Line 4
* When executing this program for Line 1, sed ignores expressions 1 and 2; 1 because it's just a label and 2 because the substitution is restricted to the last line. (**^** indicates that the *address** should only operate on the last line of the file).
* The [N command](https://www.gnu.org/software/sed/manual/sed.html#Other-Commands): 'Add a newline to the pattern space, then append the next line of input to the pattern space. If there is no more input then sed exits without processing any more commands.' 
	* Go to [GNU sed Other Commands](https://www.gnu.org/software/sed/manual/sed.html#Other-Commands) and scroll down to the N section for more options. Also, refer to the index and [this section of the GNU docs](https://www.gnu.org/software/sed/manual/sed.html#index-N_002c-and-branching) for more info on the `N` command. 
	* Within just one execution cycle, after sed ignores e1 and e2 accumulates `Line 1` into the pattern space, strips out the \\n character at the end of Line 1, THEN
	* The N command adds a newline character to the end of the pattern space and appends the contents of the next line until it hits the file's newline character at which point it stops.
	* Then sed strips out Line 2's newline character and moves from e3 to finally reach e4 for the first time. 
	* At this point, the e4 branch moves the program back to the top. Note that we still have not left the first execution cycle left even though we've already processed two lines!
	* As usual, we ignore e1 and e2 and hit e3 for our next usage of the `N` command. Now `N` adds back in a newline character (that's how the N function works) and then reads in the next line of input which is Line 3. Rinse and repeat.
	* In other words, within a single execution cycle, sed will accumulate every single line into the pattern space.
	* After all four lines are stored inside the pattern space, the `N` commands executes again and adds a final trailing \\n at the very end.
	* Then, e4 is hit and the branch command moves us back to e1. 
	* However, since there are no more lines in the input stream, e2 is finally triggered for the very first time.
	* In a single shot, the substitution expression replaces every single newline in the pattern space (if the input file is 100k lines long, then 100k \\n characters are eliminated in one shot).
* At the end of all that, the pattern space just has one long line, consisting of `Line 1 Line 2 Line 3 Line 4`. When the sed program exits, it automatically prints the contents of the pattern space into the output stream.

### Some sample scripts from the GNU sed docs
* [Useful one-liners, exotic examples, emulating standard utilities, etc.](https://www.gnu.org/software/sed/manual/sed.html#Examples)

## 9/05
### 6 Examples for Sed Branching Operation
* Created test file 11-input.txt per instructions at [this article](https://www.thegeekstuff.com/2009/12/unix-sed-tutorial-6-examples-for-sed-branching-operation/)
* JH example
	`gsed '/Administration/ {s_Administration_Supervision_; :loop; n; b loop;}' 11-input.txt >out.txt`
	* Tested and works.

## 9/06
* Began reading O'Reilly book on sed and awk by Dale Dougherty and Arnold Robbins (2nd edition, 1997). Refer to this as *OR* from now on.
* Important point about b, t, and T commands. If they are immediately followed by a label, then they GOTO that label. If they are *not* immediately followed by a label, they jump to the end of the script for this execution cycle. See p.127 of O'Reilly [sed & awk, 2nd Edition](https://www.oreilly.com/library/view/sed-awk/1565922255/) from 1997. (Advanced Flow Control Commands section of Chapter 6: Advanced sed Commands.)
* Played with using `-f filename` for more complex sed scripts. Next step is to reorganize input and output files into a single clean directory.
* Also on advice of OR book, experimented with [ed text editor](https://en.wikipedia.org/wiki/Ed_(text_editor))
* Next steps 
	1. Move all input files into consolidated new `sed` directory
	1. Begin building *.sh files inside that directory
	1. Test these *.sh files to collect input and output text files
	1. continue reading OR Chapter 4, esp. starting from p.58
	1. working sed script `s1` is located inside `2b BioNotes/_history_socialsciences/scripts/`
	1. See Warp for `gsed -f *scriptfile*` command.

## 9/07
* Reorganized filesystems. This command now works `sed -n -f ./scripts/s1 e1-test-input.md >out.txt` and invoke cds = `../sed/` directory and  cdss = `../sed/scripts/` subdirectory which will store sed scripts like s1. Remember to `chmod 777`!

### Addressing Globally Defined (OR p.59)
* A sed command can specify 0, 1, or 2 addresses. An address can be a regular expression, a line number, or a line number addressing symbol (e.g., `$` means last line in the input stream).
	1. If no address is specified, then the command is univerally applied to every line, sequentially. 
	1. If there is only *one* address, then the command is only applied to any line matching that address.
	1. If two comma-separated addresses are specified, then the command is performed on the first line matching the address and then all succeeding lines up to and *including* the line matching the second address. **aka this is a Range, formed by two address separated by 1 comma.**
	1. If an address is followed by an **exclamation mark `!`**, then the command is applied to all lines that do *not* match that address.

## 9/08
* Some discoveries implementing the `-f` script version of PK Example 4.12.
	* First, `-e` might not work to delineate different expressions. Just use the semicolon.
	* I guess each substitution statement `s/foo/bar/p` does **not** need to be wrapped in single quotes `'`. That will also cause an error.
	* See `/sed/scripts/s2`. This command works when executed in the `/sed` directory: `sed -f ./scripts/s2 gopnik-test.md >out.txt`   

## 9/09
* More observations
* Again, if using curly braces inside the script, **do not** use single quotes to encapsulate teh sed script the way you would on the command line. Single quotes not needed.
Also, whitespace is mostly ignored. So you can format all the expressions in a single line separated by semicolons (;).  Or have each expression parsed out onto each of its own lines:w

## 3/27/2024
* To grep for files of the form '68-temp.md', '69-competitors', just type `ls | grep 6.-`. B/c `.` refers to a single character of any value, followed by the literal `-`.

## 7/10/2024
* Used this command `gsed -nr 's|^[0-9]+\.|1.|gp' 93-ideas.md >out.md` to to find every instance of an initial number at the beginning of a line, and replace it with a `1.`. Reason: Original conversion to ordered list in Byword did not insert "1." everywhere, but had actual "1., 2., 3., ..., 134.". 

## 7/15/2024
* Wasn't *quite* able to get this regx working, but it was still an interesting exercise in vim. Below text from from ChatGPT:
	* It looks like the issue might be related to how the escape sequences are interpreted in Vim. In Vim, you need to escape the backslashes properly. Let's adjust your command accordingly:
	
	```vim
	:%s|\(\d\.\)|~\1|gc
	```
	
	* In Vim, the escape sequence for capturing groups should be `\(\)`, and to match a digit, you can use `\d`. Try this corrected command:
	
	```vim
	:%s|\(\d\.\)|~\1|gc
	```
	
	* If you want to include a space before the digit, ensure you have a space in the pattern:
	
	```vim
	:%s| \(\d\.\)| ~\1|gc
	```
	
	* Let's break it down again:
	- `:%s| \(\d\.\)| ~\1|gc` - Search and replace command in Vim.
	- ` ` (space) - Matches a literal space.
	- `\(\d\.\)` - Captures a digit followed by a period.
	- ` ~\1` - Replaces with a space, a tilde, and the captured group.
	
	* Ensure you have no additional or missing spaces in the pattern. If it still doesn't work, consider double-checking the actual text and ensuring the spaces and digits are matched correctly. 
	
	**Use initial \v to invoke _very magic_mode in vim**
	* If the issue persists, here’s an alternative approach using `\v` (very magic) which simplifies the escaping:
	
	```vim
	:%s/\v(\d\.)/~\1/gc
	```
	
	* Using `\v` at the beginning of the pattern makes Vim treat most characters as literal, reducing the need for excessive escaping.

***

## 3/19/2025
* Consider using `fd`, this [replacement for find](https://github.com/sharkdp/fd) which is 'fast, user-friendly alternative to Unix find'. [HN thread](https://news.ycombinator.com/item?id=43410692). From their github readme:
	* Intuitive syntax: `fd PATTERN` instead of `find -iname '*PATTERN*'`.
	* Regular expression (default) and glob-based patterns.
	* Very fast due to parallelized directory traversal.
	* Uses colors to highlight different file types (same as `ls`).
	* Supports parallel command execution
	* Smart case: the search is case-insensitive by default. It switches to case-sensitive if the pattern contains an uppercase character.
	* Ignores hidden directories and files, by default.
	* Ignores patterns from your `.gitignore`, by default.
	* The command name is 50% shorter* than find :-).
