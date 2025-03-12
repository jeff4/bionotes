---
title: Astro
permalink: /astro/
sitemap: false
---

# 2024 Log on Astro and AstroPaper

### 6/19/2024
* See dialog in ChatGPT with suggested Astro code.

### 1/12/2025 
* Edits to original content and table created 6/20/204
* See this Claude Sonnet 3.5 dialogue for updated table adding Scheme and Haskell
* Created dev.to account and found this April, 2024 [article](https://dev.to/snikidev/astrojs-as-an-alternative-to-nextjs-pushing-the-limits-30ga) by Nikita Kakuev on how the Astro approach (if not necessarily the Astro framework) is the future. "The future is simple, vanilla JS because simplicity always wins."

#### datastructures
* Table comparing the names used in various languages for common data structures

|             | **Array**    | **Map**          | **Set**       |
|-------------|--------------|------------------|---------------|
| **JavaScript** | array        | map              | set           |
| **Python**     | list         | dict             | set           |
| **Java**       | Array / ArrayList | HashMap          | HashSet       |
| **Computer Science**         | Dynamic Array | Hash Table / Associative Array / Dictionary | Hash-Set      |

#### explanation of differences between JS and Python for arrays, maps, and sets
Here are the definitions for the specified items along with their equivalent data structures or objects in Python, including differences:

1. **Array**
	*  **JavaScript Definition:** An `Array` is an ordered collection of values (elements) that are indexed by integers. Each element in an array has a specific position, starting from index 0. Arrays can store elements of any type, including other arrays, objects, or primitive values.
		*  **Example:**
		     ```javascript
		     let fruits = ["apple", "banana", "cherry"];
		     console.log(fruits[1]); // Output: banana
		     ```
	* **Python Equivalent:** `list`
		* **Definition:** A `list` in Python is an ordered collection of elements that can be of any type. Lists are indexed by integers, starting from index 0, similar to JavaScript arrays.
		* **Example:**
		       ```python
		       fruits = ["apple", "banana", "cherry"]
		       print(fruits[1]) # Output: banana
		       ```
	* **Differences:** Python lists can also hold elements of any type, including other lists and objects, just like JavaScript arrays. Both data structures are dynamic in size and allow for element modifications.

2. **Map**
	*  **JavaScript Definition:** A `Map` is a collection of key-value pairs where both keys and values can be of any type. Unlike plain objects, which use strings as keys, maps can use objects, functions, and other data types as keys. Maps maintain the order of their elements based on the order of insertion.
		* **Example:**
			```javascript
			let map = new Map();
			map.set('name', 'Alice');
			map.set('age', 30);
			console.log(map.get('name')); // Output: Alice
			```
	* **Python Equivalent:** `dict`
		* **Definition:** A `dict` (dictionary) in Python is a collection of key-value pairs where keys can be of any immutable type (e.g., strings, numbers, tuples), and values can be of any type. Dictionaries maintain insertion order since Python 3.7.
		* **Example:**
		```python
		info = {'name': 'Alice', 'age': 30}
		print(info['name']) # Output: Alice
		```
	* **Differences:** Python dictionaries only allow immutable types as keys, while JavaScript maps allow any type of keys. Both structures maintain insertion order and allow for dynamic addition and modification of elements.

3. **Set**
	* **JavaScript Definition:** A `Set` is a collection of unique values. Unlike arrays, sets do not allow duplicate elements. Sets can store values of any type and maintain the order of insertion.
		* **Example:**
		```javascript
		let set = new Set();
		set.add(1);
		set.add(2);
		set.add(2); // Duplicate value, won't be added
		console.log(set.size); // Output: 2
		```
	* **Python Equivalent:** `set`
		* **Definition:** A `set` in Python is an unordered collection of unique elements. Sets do not allow duplicate values and can store elements of any immutable type.
		* **Example:**
		```python
		s = set()
		s.add(1)
		s.add(2)
		s.add(2) # Duplicate value, won't be added
		print(len(s)) # Output: 2
		```
	* **Differences:** Both JavaScript sets and Python sets store unique values and do not allow duplicates. JavaScript sets maintain insertion order, while Python sets are unordered collections. Both support basic set operations like union, intersection, and difference.


***

# AstroPaper 2025 Log
## 1/12/2025
* Began trying to install v4.0 version of AstroPaper. Install instructions from AstroPaper 3 [blog post](https://astro-paper.pages.dev/posts/astro-paper-v3/)
* Cmd line instructions are on [main AstroPaper github page](https://github.com/satnaing/astro-paper?tab=readme-ov-file) in the [*Running Locally* section](https://github.com/satnaing/astro-paper?tab=readme-ov-file#-running-locally)j
* Before I could run the astro install command, I had to upgrade node via homebrew, then upgrade npm. 
	* Also, since i ran `brew upgrade`, my **Alacritty** terminal was also updated so i had to migrate that. See OneNote for detailed notes
* Hmm, per [Issue #435](https://github.com/satnaing/astro-paper/issues/435), as of Jan 12, 2025, AstroPaper is still pinned to Astro version 4.16.3. And we are requesting that install can be updated to use Astro 5.1. So maybe I'll just hold off on the Astro/AstroPaper migration for now until Astro 5 is supported by AstroPaper/SatNaing.

## 1/16/2025
* Still waiting for Sat Naing to update AstroPaper to fully support Astro v5.

## 1/21/2025
* Still no update on [Issue #435](https://github.com/satnaing/astro-paper/issues/435)

***

## 2/12/2025
* Notes on JS program (with maybe python and haskell implementations) to auto-format new blog posts.

***

# 3/11/2025
* OK, Sat Naing finally pushed updates for AstroPaper 5, which includes support for Astro v5 and Tailwind v4 out of the box.
* **Sat's** [**main blog post on AstroPaper 5**](https://astro-paper.pages.dev/posts/astro-paper-v5/).
* See also these general AstroPaper blog posts from the past that have all been updated for AP5 as of March 8, 2025:
	1. [How to configure blog posts](https://astro-paper.pages.dev/posts/adding-new-posts-in-astropaper-theme/) 
	1. [How to configure sitewide variables and visual theme](https://astro-paper.pages.dev/posts/how-to-configure-astropaper-theme/)

## Machine checklist
* champ-1524 has everything up to and including updated .bash_profile
1. delete and recreate `/a1/` directory
1. next, create new github repo
1. next, pull from new github repo to minipro23
* minipro23 has everything up to and excluding `pnpm create astro@latest --template satnaing/astro-paper`. And in fact, we won't use that because we will populate by downloading from github

## General notes:
* Have to install new package manager [pnpm](https://github.com/pnpm/pnpm). Can read this [blog post](https://pnpm.io/blog/2020/05/27/flat-node-modules-is-not-the-only-way) for more on pnpm.
* Instructions from main [AstroPaper GitHub page](https://github.com/satnaing/astro-paper?tab=readme-ov-file#-running-locally)

#### pnpm command
`pnpm create astro@latest --template satnaing/astro-paper`

#### npm command
`npm create astro@latest -- --template satnaing/astro-paper`

## grep command within vim to update from cd4 shortcutrs to cd1 shortcuts (and more importantly, switch from Dropbox to local directory)
* `:24,36s~jeffh\/Dropbox\/proj-4\/a4-paper-intel~jeffh/demo_files/a1-arm/~gc`

***

### I. Preliminary Steps
1. Update/upgrade homebrew to make sure we are on the latest
1. Use homebrew to install pnpm with this command `brew install pnpm`
	* per `pnpm --version`, we are running version `10.6.2`
1. Create new directory locally in `~/demo_files/`, **not** in Dropbox. Let's call it `a1.-arm` (Will eventually delete a3 and a4).


### II. Install Astro
1. Run **pnpm create astro@latest --template satnaing/astro-paper** 
	* Make sure when it asks you where to create home directory, using `/.` to load it all into current directory.
	* Enable TypeScript (y)
	* Allow installer to install dependencies
1. `pnpm run dev` won't work yet. You need to either:
	* install astro using `pnpm add astro` OR
	* invoke first run directly using `npx astro dev`. This command will say that we need to install `astro@5.4.3, OK to proceed (y/n)`. 
	* Note I chose first option and it's working now
1. Change `.bash_profile` so that we have a new shortcut to execute. instead of `np` as an alias for `npm run dev`, etc., let's use **pp** as an alias for `pnpm run dev` whih starts the local server on port ...
1. Create a new repo at GitHub
1. Connect repo with Netlify so that this can run as vanilla as `https://jeffhwang-a1.netlify.app/`



***

## 3/12/2025
* OK, minor updates to sw and docs in AstroPaper, latest version is [**5.0.1**](https://github.com/satnaing/astro-paper/releases/tag/v5.0.1). Previous link goes to [5.0.1 release page](https://github.com/satnaing/astro-paper/releases/tag/v5.0.1).
