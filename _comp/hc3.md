---
title: HC3 - Notes on Haskell Mooc
permalink: /hc3/
sitemap: false
---


***

# Haskell Notes, page 3
* [Haskell Mooc Course](https://haskell.mooc.fi/)


## 12/09/2024
## 3.4 Lambdas
* The last "spanner" we need in our functional programming toolbox is the **lambda (&#955;)**.
* Lambda expressions are *anonymous functions*.
* Lambdas let us rewrite a function like:

```haskell
let big x = x>7 in filter big [1,10,100]
```

* into this:

```haskell
filter (\x -> x>7) [1,10,100]
```

***

* In other words, we don't need to name or define the helper function (e.g., **`let big x = ...`**) 

* Note that in Haskell, the **backslash character (\\)** represents the **lambda (&#955;)**.
* The Haskell expression *`\x -> x + 1`* is trying to mimic the mathematical notation **&#955;x . x+1**
* Note! You never *need* to use a lambda expression. You always have the option of defining a function normally using **let** or **where**.
* JavaScript equivalent is the **arrow function** `x => x+1`.
* Python equivalent is `lambda x: x+1`.
* For more on arrow functions within JS, see David Flanagan, Chapter 8, section 8.1.3 Arrow Functions. P. 344 of 1245.
	* See also prelim on p. 339. ES6 introduced arrow functions to JS.
* JH: It seems to me that only a small part of JS 'arrow functions' is the syntatic sugar of writing a concise function quickly and anonymously (no name to function in function declaration). The bigger aspect is ability to compose functions, pass functions as arguments / input parameters into other functions to make JS accept a functional programming paradigm. Note the *bind()* aspect of JS programming.
* Mooc says 'lambda expressions are quite powerful constructs which have a deep theory of their own, known as [lambda calculus](https://en.wikipedia.org/wiki/Lambda_calculus).'
	* Some even consider purely functional programming languages such as Haskell to simply be typed extensions of lambda calculus with extra syntax.

***

## 12/11/2024
## 3.5 Sidenote: The . and $ operators
* The two most common operators in Haskell codebases are **`.`** and **`$`**.

### 3.5.1 The . operator -- Function Composition

```haskell
(.) :: (b -> c) -> (a -> b) -> a -> c
```

* And this is what it does:

```haskell
(f.g) x -- output: f (g x)
```

* Examples:

```haskell
double x = 2*x
quadruple = double . double -- computes 2*(2*x) == 4*x
f = quaduple . (+1)         -- computes 4*( x+1 )
g = (+1) . quadruple        -- computes 4*x + 1
third = head . tail . tail  -- fetches the third element of a list
```

***

## 12/13/2024
#### 3.5.1.2 Reimplementing doTwice() with `.`
* Note that one can use the **`doTwice`** both as an *applied only to a fucnction*, or as *applied to a function* + *applied as a value*. 

```haskell
doTwice :: (a -> a) -> a -> a
doTwice f = f . f
```

***

```haskell
let ttail = doTwice tail
in ttail [ 1, 2, 3, 4 ] -- output [3,4]

(doTwice tail) [1,2,3,4] -- output: [3,4]
doTwice tail [1,2,3,4] -- output: [3,4]  
```

***
* Often function composition is not used when defining a new function; but instead to avoid defining a helper function.
* Consider the difference between these 2 expressions:

```haskell
let notEmpty x = not (null x)
in filter notEmpty [[1,2,3],[],[4]]
--output: [[1,2,3],[4]] 

filter ( not . null ) [[1,2,3],[],[4]]
--output: [[1,2,3],[4]] 
```

***
## 12/18/2024
### 3.5.2 The $ operator more details
* Consider it's type: 

```haskell
ghci> :t ($)
($) :: (a -> b) -> a -> b
```

* It takes as an input/argument something of type **`(a->b)`** and returns a value of type **b**.
* In other words, **$** is a function application operator.
* The expression **`f $ x`** is the same as **`f x`**.
* This seems pretty useless, but it means that the **$** operator can be used to eliminate parentheses!
* These 2 expressions are the same:

```haskell
head (reverse "abcd") -- Expression 1
head $ reverse "abcd" -- Expression 2
```

* A more impressive example:

```haskell
-- v1: Lots of parentheses 
reverse (map head (map reverse (["Haskell", "pro"] ++ ["dodo", "lyric"])))

-- v2: Rewritten with '.'
(reverse . map head . map reverse) (["Haskell","pro"] ++ ["dodo","lyric"])

-- v3: Rewritten with '.' and '$'
reverse . map head . map reverse $ ["Haskell","pro"] ++ ["dodo","lyric"]
```

***

* Sometimes the operators **`.`** and **`$`** are useful as fnctions in their own right.
* For example, a list of functions can be applied to an argument using a map and a section of `$`:


```haskell
--Expression 1
map ($"string") [reverse, take 2, drop 2]

--Expression 2
[reverse $ "string", take 2 $ "string", drop 2 $ "string"]

--Expression 3
[reverse "string", take 2 "string", drop 2 "string"]
  
```
* See this [ChatGPT](https://chatgpt.com/share/67639e82-b2fc-8013-81b8-5b6e3ec8c32d) to understand how/why the above three expressions are identical.
* If this seems complicated, don't worry. You don't need to use `.` or `$` in your own code until you are comfortable with these infix operators.
* For more on reading other people's Haskell that uses `.` and `$`, check out this [article](https://typeclasses.com/featured/dollar)

***

## 3.6 Example: Rewriting whatFollows()
* Now let's rewrite **`whatFollows`** example using these tools. The original version:

```haskell
substringsOfLength :: Int -> String -> [String]
substringsOfLength n string = map shorten (tails string)
  where shorten s = take n s

whatFollows :: Char -> Int -> String -> [String]
whatFollows c k string = map tail (filter match (substringsOfLength (k+1) string))
  where match sub = take 1 sub == [c]
```

* To get started, let's get rid of the helper function **`substringsOfLength`** and move all the code to `whatFollows`.

***
## 1/08/2025
* Next, paste in output from rewritten version with f1, f2, ...
* and then reimplement in Haskell

## 1/13/2025
* Furthermore, Haskell Types are going to look a lot like Classes in Java/C++ or other OO-languages. But **don't be fooled** they are not classes. Probably Types are most similar to Interfaces.

## 1/22/2025
* Let's re-examine the original implementation of helper function `substringsOfLength()` and original version of `whatFollows()` from 12/05/2024. There was a JS implementation from that date as well as [this ChatGPT](https://chatgpt.com/share/67514f9e-61d8-8013-bc70-75137ff20ab3) explanation.

## 1/23/2025
* starting from section 3.6, note that the Mooc has a copy of the original whatFollows(). see `3whatFollows.hs`.
* With some help from Claude, got verion 0 working. remember to use single quotes (***`'`**) for individual characters and double quotes (**`"`**) for strings. 
	* e.g., the proper way to call the function in GHCi is `whatFollows 'u' 4 "superman"`. Which outputs `perm`.
* Now going through v0 line by line.
* After some more Claude dialogue, learned more about how the `string` and `n` work together in the subStringsOfLength function. 
	* **`shorten`** is a generic function and it doesn't necessarily key off of `s`. Instead of `s`, one can place any parameter there, it doesn't need to be a string. It's a higher order function (I think).

## 1/25/2025
* Rewriting v0 with function names:

```haskell
import Data.List
f2_substringsOfLength :: Int -> String -> [String]
f2_substringsOfLength n string = map f3_shorten (tails string)
  where f3_shorten s = take n s

f1_whatFollows :: Char -> Int -> String -> [String]
f1_whatFollows c k string = map tail (filter f4_match (f2_substringsOfLength (k+1) string))
  where f4_match sub = take 1 sub == [c]
```
***
* After a dialogue with Claude, decided there are:
#### Five ways to declare a function in Haskell

1. **Top-Level Declaration**
```haskell
functionName :: Type1 -> Type2 -> OutputType
functionName arg1 arg2 = expression
```

2. **Where Clause**
```haskell
mainFunction args = expression
  where helperFunction args = helperExpression
```

3. **Let Binding**
```haskell
mainFunction = let localFunction args = expression
               in localFunction args
```

4. **Case Expression**
```haskell
function args = case expression of
    pattern1 -> result1
    pattern2 -> result2
```

5. **Lambda/Anonymous Function**
```haskell
\arg1 arg2 -> expression
-- Example usage:
map (\x -> x + 1) [1,2,3]
```
***
* Remember, Method 2 with the **where** clause means that function is *only* available within that the larger function it is embedded in. I got into trouble trying to use `f3_shorten` separately in GHCi because it doesn't mean anything outside of `f2_subStringsOfLength`.


## 2/05
