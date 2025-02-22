---
title: TypeScript 2
permalink: /ts2/
sitemap: false
---

# Learning TypeScript, page 2
* Josh Goldberg
* O'Reilly Media, 2022
* TypeScript Notes. LTS = Learning TypeScript by Josh Goldberg
* [LTS aka TS1 aka TypeScript 1](/ts1)
* [LTS aka TS2 aka TypeScript 2](/ts2)


## 8/02/2024
### Conceptual overview of various chapters to follow.
* Chapters in *Learning TypeScript* organized into 3 main sections with one extra section:
	* **Part I: Concepts**
	* **Part II: Features**
	* **Part III: Usage**
	* **Part IV: Extra Credit**
* **Part II: Features**
	1. Chapter 5: Functions
	1. Chapter 6: Arrays
	1. Chapter 7: Interfaces
	1. Chapter 8: Classes
	1. Chapter 9: Type Modifiers
	1. Chapter 10: Generics
* **Part III: Usage**
	1. Chapter 11: Declaration Files
	1. Chapter 12: Using IDE Features
	1. Chapter 13: Configuration Options
* **Part IV: Extra Credit**
	1. Chapter 14: Syntax Extensions
	1. Chapter 15: Type Operations

***
# Chapter 6: Arrays p. 104
* TypeScript supports the JS best practice of only using one datatype of the values within an array.

```typescript
const warriors = ["Artemisia", "Boudica"];

warriors.push("Zenobia"); // OK bc new input item is a string

// Error b/c input value is type 'boolean'
warriors.push(true);
```

* One can think of TS inference of an array's type from its initial embers as similar to how TS understands variable types from their initial values.

## 6.1 Array Types p. 105
* Variable meant to store arrays do *not* ned to have an initial value.
* The variables can start off as `undefined` and then receive an array value later.

```typescript
let arrayOfNumbers: number[];
arrayOfNumbers = [4, 8, 15, 16, 23, 42];
```
## 8/19/2024
### 6.1.1 Array and Function Types p. 105
* Array types are an example of a syntax container where function types may need parentheses to distinguis what's in the function type or not.
* Parentheses may be used to indicate which part of an annotation is the function return or the surrounding array type.
* The **createStrings** type here--it is a *function* type--is *not* the same as **stringCreators** which is an array type (Ex on p. 105-106):

```typescript

let createStrings: () => string[];

let stringCreators: ( ()=> string )[];
```

### 6.1.2 Union-Type Arrays p. 106
* One can use a union type to indicate that each element in an array can be one of multiple select types.
* When using array types with unions, *parentheses* may need to be used to indicate which part of an annotation is the **contents of the array** or the **surrounding union type**.
* Using parentheses in array 

```typescript
// This means that type is 
// either a *number* or an *array of strings*
let stringOrArrayOfNumbers: string | number[];

// This means that type is an array of elements
// that are *each* either a number or a string
let stringOrArrayOfNumbers: (string | number)[];
```

### 6.1.3 Evolving Any Arrays p. 106
* If one does not include any type annotation on a variable initally set to an empty array, TS will treat this new array as *evolving `any[]`*.
	* Evolving `any[]` means that this array can receive any type of content.
* Just like with evolving *any* variables, this is **not good**.
* The whole point of TS is to have clearly defined static types.o
* There are some times this may be useful--but **be careful**. see p. 107 for brief examples and more.

### 6.1.4 Multi-Dimensional Arrays p. 107
* A 2D array *aka* an *array of arrays* will have two `[]` like so p. 107:

```typescript
let 2dArray: number[][];

2dArray = [
  [1, 2, 3],
  [2, 4, 6],
  [3, 6, 9],
];

// higher dimension arrays

let 3dArray: number[][][];

3dArray = [
  [
    [ 1, 2],
    [ 3, 4],
  ],  [
    [ 2, 4],
    [ 6, 8],
  ],  [
    [ 3, 6],
    [ 9, 12],
  ],
];
```
* See TS example on p. 108:

```typescript
let arrayOfArraysOfNumbers: ( number[] )[];

```

## 8/20/2024
## 6.2 Array Members p. 108
* TS understands typical index-based access for retrieving members of an array to give back an element of that array's type.

### 6.2.1 Caveat: Unsound Members p. 108
* The TypeScript type system is known to be **technically unsound** b/c although TS gets most types right, TS *can* get types of values incorrect.
* In particular, **arrays are a source of unsoundness** in TS's type system.
* See example on p. 108-109

## 6.3 Spreads and Rests p. 109
### 6.3.1 Spreads p. 109
* Arrays can be joined together using the `...` spread operator.
* TypeScript understands the result array will contain values that can be either of the input arrays.
* If the input arrays are the same type, the output array will be that same type.
* If two arrays of *different* types are spread together to create a new array will be understood as an **union type** array of elements that either of the two original types.
* Example p. 110:

```typescript
// Type: string[]
const soldiers = [ "Harriet Tubman", "Joan of Arc", "Khutulun" ];

// Type: number[]
const soldierAges = [ 90, 19, 45 ];

// Type: ( string | number)[]
const conjoined = [...soldiers, ...soldierAges];
```

### 6.3.2 Spreading Rest Parameters p. 110
* TS recognizes and will perform type checking on the JS practie of using the `...` **spreading an array** as a rest parameter.
* Arrays used as arguments for rest parameters must have the same array type as the rest parameter.
* The **logWarriors()** function below takes in only *string* values for its `...names` rest parameter.
* Spreading an array of type **string[]** is allowed, but a **number[]** is *not*.

```typescript
function logWarriors( greeting: string, ...names: string[] ) {
	for ( const name of names ) {
		console.log( `${ greeting }, ${ name }!` );
	}
}

const warriors = [ "Cathay Williams", "Lozen", "Nzinga" ];

logWarriors( "Hello", ...warriors );

const birthYears = [ 1844, 1840, 1583 ];

logWarriors( "Born in", ...birthYears );
//                      ^^^^^^^^^^^^^
// Error: Argument of type 'number' is not assignable
// to parameter of type 'string'.
```

## 6.4 Tuples p. 109
* Although JS arrays can be any size, we can also make JS arrays a fixed size--which is called a **tuple**.
* Tuple arrays have a specific known type at each index that may be more specific than a union type of all possible members of the array.
* The syntax to declare a tuple type looks like an aray literal but with **types** instead of **elements**.
* Example p. 111

```typescript

let yearAndWarrior: [ number, string ];

yearAndWarrior = [ 508, "Tomyris" ]; // ok

yearAndWarrior = [ false, "Tomyris" ]; 
//                 ^^^^^
// Error: Type 'boolean' is not assignable to type 'number'

yearAndWarrior = [ 508 ]; 
//                 ^^^
// Error: Type '[number]' is not assignable to 
// type '[number, string]'. Source has 1 element
// but target requires 2.
```

* Tuples are often used in JS alongside array destructuring to be able to assign multiple values at once, such as setting 2 variables to initial values based on a single condition.
* For example, TS recognizes here that **year** is always going to be a *number* and **warrior** is always going to be a *string*.
* Example p. 111:

```typescript

let [ year, warrior ] = Math.random() > 0.5
	? [340, "Archidamia"]
	: [1828, "Rani of Jhansi"];
```

### 6.4.1 Tuple Assignability p. 111
* **Tuple types** are treated by TS as more specific than variable length array types.
* That means variable length array types aren't assignable to tuple types.
* Example p. 112:

```typescript
// Type: (boolean | number)[]
const pairLoose = [ false, 123 ];

const pairTupleLoose: [ boolean, number ] = pairLoose;
//    ^^^^^^^^^^^^^^
// Error: Type '( number | boolean )[]' is not
// assignable to type '[boolean, number]'
// Target requires 2 elements but source may have fewer
```
* In above example, although we as humans see **pairLoose** as having **[boolean, number]** inside, TS infers it to be the more general **(boolean | number)[]** type.
* If **pairLoose** had been declared as a **[boolean, number]** itself, the assignment of its value to *pairTuple* would have been permitted.
* Tuples of different lengths are also *not* assignable to each other.
* As TS includes knowing how many members are in the tuple in tuple types. 
* Consider this example p. 112:

```typescript
const tupleThree: [boolean, number, string] = [false, 1583, "Nzinga"];

const tupleTwoExact: [boolean, number] = [tupleThree[0], tupleThree[1]];

const tupleTwoExtra: [boolean, number] = tupleThree;
//    ^^^^^^^^^^^^^
// Error: Type '[boolean, number, string]' is not assignable
// to type '[boolean, number]'.
// Source has **3** elements but target only allows 2.
```

#### 6.4.1.1 Tuple as Rest Parameters p. 113
* B/c tuples are seen as arrays with more specific type information on length and element types, they can be particularly useful for storing arguments to be passed to a function.
* TS is able to provide accurate type checking for tuples passed as `...` rest parameters.
* Here, the **logPair** function's parameters are typed string and number.
* Trying to pass in a value of type *( string \| number)[]* as arguments wouldn't be type safe as the contents might not match up: they could both be the same type, or one of each type in the wrong order.
* However, if TS knows the value to be a *[string, number]* tuple, it understands the values match up:

```typescript
function logPair( name: string, value: number) {
	console.log(`${name} has ${value}`);
}

const pairArray = ["Amage", 1];

logPair(...pairArray);
// Error: A spread argument must either have a tuple type
// or be passed to a rest operator.

const pairTupleIncorrect: [number, string] = [1, "Amage"];

logPair(...pairTupleIncorrect);
// Error: Argument of type 'number' is not assignable
// to parameter of type 'string'.

const pairTupleCorrect: [string, number] = ["Amage", 1];

logPair(...pairTupleCorrect); // ok
```

* If you really want to go wild with your rest parameter tuples, you can mix them with arrays to store a *list of arguments* for **multiple function calls**. Example p. 113-114:

```typescript
function logTrio (name: string, value: [number, boolean]) {
	console.log( `${name} has ${value[0]} ${value[1]}` ); 
}

const trios: [ string, [number, boolean] ][] = [
  ["Amanitore", [1, true]],
  ["Aethelflaed", [2, false]],
  ["Ann E. Dunwoody", [3, false]]
];

trios.forEach( trio => logTrio(...trio) ); //ok

// Error -- see p. 114
trios.forEach(logTrio);
```

### 6.4.2 Tuple Inferences p. 114
* TS generally treats created arrays as variable length arrays, not tuples. 
* If TS sees an array being used as a vairable's initial value or the returned value for a function, TS will then assume a *flexible sized* array rather than a fixed-sized tuple.
* Example p. 114:

```typescript
// Return type:  (string | number )[]
function firstCharAndSize( input: string ) {
	return [input[0], input.length);
}

// firstChar type: string | number
// size type: string | number
const [firstChar, size] = firstCharAndSize("Gudit");
```

* There are two common ways in TS to indiciate that a vlaue should be a more specific tuple type instead of a general array type:
	1. using **explicit tuple types**; and
	1. using **const** assertions.

#### 6.4.2.1 Explicit tuple types p. 115
* Tuple types may be used in type annotations such as return type annotation for a function...

#### 6.4.2.2 Const asserted tuples p. 115

***

# Chapter 7: Interfaces p. 118

## 7.1 Type Aliases vs. Interfaces p. 118
* In general, it's better to use **interfaces** versus **aliased object types**.
	* For more on **aliased object types**, see p. 69. More concise syntax than *vanilla object type* which is semantically the same.
	* See initial example of vanilla *object type* declaration on p. 68: `let PoetLater { born:number; name:string }`.
	* Compare with *aliased object type* declaration on p. 69: `type Poet { born:number; name:string }; let poetLater: Poet;`.
* Quick comparison of aliased object type vs. interface

```typescript

// Aliased Object Type
type Poet = {
	born: number;
	name: string;
}

// Equivalent syntax for interface
interface Poet {
	born: number;
	name: string;
}
// Note: that interfaces preferentially do *not* have terminating semicolons
// whereas aliased object types.
```

* TS's assignability checking and error messages for interfaces also work and look just about the same as they do for object types.
* The following assignability errors for assigning to the **valueLater** variable would be roughly the same if *Poet* was an interface or type alias:

```typescript
let valueLater: Poet;

// ok
valueLater = {
	born: 1935,
	name: 'Sara Teasdale',
};

// Error: Type 'string' is not assignable to 'Poet'
valueLater = "Emily Dickinson";

// Error: Type 'boolean' is not assignable to type 'number'
valueLater = {
	born: true,
	name: 'Sappho'
};
```

### 7.1.1 Differences between interfaces and type aliases in this chapter
* Interfaces can *merge* together to be augmented--a feature particularly useful when working with 3rd-party code such as built-in globals or npm packages.
* In Chapter 8, we'll see that interfaces can be used to type check the structure of class declarations while type aliases cannot.
* Interfaces are generally speedier for the TS type checker to work with: they declare a named type that can be cached more easily interally, rather than a dynamic copy-and-paste of a new object literal the way type aliases do.
* B/c interfaces are considered *named objects* rather than an alias for an unnamed object literal, their error messages are more likely to be readable in hard edge cases.
* **In general, it's best to use interfaces whenever possible.** p. 120

***

## 7.2 Types of Properties p. 120
* JS objects can be wild and wacky in real-world usage, (see p. 120 for examples). 
* TS interfaces provide a system of tools that help us model that wackiness.

### 7.2.1 Optional Properties p. 120
* As with object types, interface properties don't all have to be required in the object.
* One can indicate that an interface's property is optional by including a `?` before the `:` in its type annotation.
* This **Book** interface requires only a *required* property and optionally allows an *optional*.
* Objects adhering to it may provide *optional* or leave it out as long as they provide required. Example p. 121:
* The same caveats around optional vs. regular properties when a type happens to include an **undefined** in a type union apply to interfaces and object types. see more on p. 121

```typescript
interface Book {
	author?: string; // '?' indicates that this interface property is optional
	pages: number;
};

// ok
const ok: Book = {
	author: "Rita Dove",
	pages: 80,
};

// Error: Property 'author' is missing in type 
// '{ pages: number; }' but required in type 'Book'.

const missing: Book = {
	pages: 80,
};
```

### 7.2.2 Read-Only Properties p. 121
* You may sometimes wish to block users of your interface from reassigning properties of objects adhering to an interface.
* TypeScript allows you to add a **readonly** modifier before a property name to indicate that once set, that property should not be set to a different value.
* Example p. 121, the **text** property in the below **Page** interface returns a string when accessed.
	* But TS raises a type error if the *text* property is assigned a new value:

```typescript
interface Page {
	readonly text: string;
}

function read( pageObject: Page ) {
	
	// this is ok: just accessing the 'text' property 
	// doesn't try to modify it
	console.log( pageObject.text );

	// this will cause an error b/c are trying to 
	// assign a new value to the 'text' property
	pageObject.text += "!";
}
```
* More on usage of **readonly** modifiers and how they only exist in the type system / interfaces p. 122.

***

### 7.2.3 Functions and Methods p. 122
* It is very common in JS for object members to be functions.
* TS allows declaring interface members to be function types--covered in Chapter 5: Functions.

### Two ways of declaring interface members as functions p.123
1. **Way 1--Method Syntax**: declaring that a member of the interface is a function intended to be called as a member of the object, e.g., **member(): void**.
1. **Way 2--Property Syntax**: declaring that a member of the interface is equal to a *standalone function*, e.g., **member: () => void**.

#### More notes and an example of Way 1 + Way 2  p. 123
* The two declaration forms are an analog for the two ways you can declare a JS object as having a function.

```typescript
// uses both ways to declare interface methods
interface HasBothFunctionTypes {
	property: () => string; // Way 2: Property Syntax
	method(): string;       // Way 1: Method Syntax
}

const hasBoth: HasBothFunctionTypes = {
	property: () => "",
	method() {
		return "";
	}
};

hasBoth.property(); //ok
hasBoth.method(); //ok
```

* Both ways can receive the **? optional modifier** to indicate that a *function is not needed** as part of the interface.
* Example p. 123

```typescript
interface OptionalReadonlyFunctions {
  optionalProperty?: () => string;
  optionalMethod?(): string;
}
```
* Method and property declarations can mostly be used interchangeably. Three main differences
	1. Only **Way 2: properties** can be declared **readonly**. **Way 1: method** cannot be declared readonly.
	1. Interface merging is treated differently between **Way 2** and **Way 1**. 
	1. Some of the operations performed on types treat them differently--see Chapter 15 on Type Operations.
* For now, the general style guide LTS recommends is:
	* Use **Way 1: Method function declaration** if one knows the underlying function may refer to keyword **this** (See Chapter 8 on Classes).
	* Use **Way 2: Property function declaration** otherwise.

***

### 7.2.4 Call Signatures p. 124
* Both interfaces and object types can declare **call signatures**.
* *Call Signatures* are a type system description of how a value may be called like a function.
* Example p. 124-125:

```typescript
type FunctionAlias = ( input: string ) => number;

interface CallSignature {
	( input: string ): number;
}

// Type: ( input: string ) => number
const typedFunctionAlias: FunctionAlias = (input) => input.length; // ok

// Type: ( input: string ) => number
const typedCallSignature: CallSignature = (input) => input.length; // ok
```
* Call signatures can be used to describe functions that additionally have some user-defined property on them.
* TS will recognize a property added to a function declaration as adding to that function declaration's type.
* Example p. 125:

```typescript
interface FunctionWithCount {
	count: number;
	(): void;
}

let hasCallCount: FunctionWithCount;

function keepsTrackOfCalls() {
	keepsTrackOfCalls.count += 1;
	console.log( `I've been called ${ keepsTrackOfCalls.count } times!` );
}

keepsTrackOfCalls.count = 0;

hasCallCount = keepsTrackOfCalls; //ok

function doesNotHaveCount() {
	console.log( "No idea!" );
}

// Error: property 'count' is missing in type
// '() => void' but required in type 'FunctionWithCalls'
hasCallCount = doesNotHaveCount;
```
* The above example has a **keepTrackOfCalls** function declaration which is given a **count** property of type *number*. It's assignable using the FunctionWithCount interface.
* The error on the last line is caused b/c it was *not* given a **count**.

***

### 7.2.5 Index Signatures p. 126
* TS provides a syntax called **index signature** to indicate that an interface's objects are allowed to take in *any* key and return a certain type under that key.
* This makes *"container"* objects practical in JS projects that store values that are referenced using an arbitrary *string* primary key.
* **Index Signatures** are most commonly used with string keys b/c JS object property lookcups convert keys to string implicitly.
* An index signature looks like a regular property definition but with a type after the key like so:
```typescript
{
	[ i: string]: ...
}
```

#### 7.2.5.1 Example 1

* The below **WordCounts** interface example is declared as allowing *any* **string** key with a number value.
* Objects of that type aren't bound to receiving any particular key--as long as the value is a **number** p. 126:

```typescript
interface WordCounts {
  [i: string]: number;
}

const counts: WordCounts = {};

counts.apple = 0; // ok this is a *number*
counts.banana = 1; // ok this is a *number*

counts.cherry = false; // error
// Error: Type 'boolean' is not assignable 
// to type 'number'.
```
* Index signatures are convenient for assigning values to an object but aren't completely type safe.
* Index signatures indicate that an object shoukd give back a value no matter what property is being accessed.

#### 7.2.5.2 Example 2

* Consider this example (p. 126-127). The **publishDates** value safely returns a **Frankenstein** object as a **Date** type--but *tricks* TS into thinking its **Beloved** is defined.
	* Even though **Beloved** is in fact *not* defined.

```typescript
interface DatesByName {
  [i: string]: Date;
}

const publishDates: DatesByName = {
  Frankenstein: new Date( "1 January 1818" ),
};

publishDates.Frankenstein; // Type: Date
console.log( publishDates.Frankenstein.toString() ); // ok

publishDates.Beloved; // Type: Date--but runtime value is undefined!

// OK in the type system, but it causes a runtime error
// Runtime Error: Cannot read property 'toString'
// of undefined (reading publishDates.Beloved)
console.log( publishDates.Beloved.toString() ); 
```
* When possible, if one is looking to store key-value pairs and the keys are *not* known ahead of time, it is generally better to use **Map** instead.
* The **.get()** method of Maps always returns a type with a `| undefined` to indicate that the key might not exist.
* See more in Chapter 9 on working with generic container classes such as **Map** and **Set**.

#### 7.2.5.3 Mixing properties and index signatures p. 127
* Interfaces are able to include explicitly named properties and catchall *string* index signatures...
* ...but there is *one* catch.
* Each named property's type must be assignable to its catchall index signature's type.
* One can think of mixing them as telling TS that named properties give a more specific type, and any other property falls back to the index signature's type.
* Example on p. 127-128, where **HistoricalNovels** declares that all properties are type *number*. Additionally, the *Oroonoko* property must exist to begin with:

```typescript
interface Historical Novels {
  Oroonoko: number;
  [i: string]: number;
}

// Ok
const novels: HistoricalNovels = {
  Outlander: 1991,
  Oroonoko: 1688,
};

// Error: Property 'Oroonoko' is missing in type
// '{ Outlander: number; }' but required in type
// 'HistoricalNovels'.
const missingOroonoko: HistoricalNovels = {
  Outlander: 1991,
};
```
* One common type system trick with mixed properties and index signatures is to use a more specific property type literal for the named property than an index signature's primitive.
* As long as the named property's type is assignble to the index ssignature's--which is true for a literal and a primitive, respectively--TS will allow it.
* Consider this example p. 128. The **ChapterStarts** interface declares that a property under **preface** must be *0* and all other properties have the more general **number**.
* That means any object adhering to **ChapterStarts** must have a *preface* property equal to *0*.

```typescript
interface ChatperStarts {
  preface: 0;
  [i: string]: number;
}

const correctPreface: ChapterStarts = {
  preface: 0,
  night: 1,
  shopping; 5
};

const wrongPreface: ChapterStarts = {
  preface: 1,
  // Error: Type '1' is not assignable to type '0'
};
```

#### 7.2.5.4 Numeric Index Signatures p. 128
* Although JS implicitly converts object property lookup keys to strings, it is sometimes desirable to only allow **numbers as keys**.
* TS index signatures can use a *number* type instead of a *string* but with the same catch as *named properties*--that their types must be assignable to the catchall *string* index signatures.
* Example p. 128-129

```typescript
// Ok
interface MoreNarrowNumbers {
  [i: number]: string;
  [i: string]: string | undefined;
}

//ok
const mixesNumbersAndStrings: MoreNarrowNumbers = {
  0: '',
  key1: '',
  key2: undefined,
}

interface MoreNarrowStrings {
  // Error: 'number' index type 'string | undefined' 
  // is not assignable to 'string' index type 'string'.
  [i: number]: string | undefined;
  
  [i: string]: string;
}
```
***
### 7.2.6 Nested Interfaces p. 129
* Just like object types can be nested as properties of other object types, interface types can also have properties that are themselves interface types (or object types).
#### 7.2.6.1 Example of nested interfaces p. 129-130
* This **Novel** interfae contains an **author** property that must satisfy an inline object type and a **setting** property that must satisfy the **Setting** interface:

```typescript
interface Novel {
  author: {
    name: string;
  };
  setting: Setting;
}

interface Setting {
  place: string;
  year: number;
}

let myNovel: Novel;

// OK
myNovel = {
  author: {
    name: 'Jane Austen',
  },
  setting: {
    place: 'England',
    year: 1812,
  }
};

// Error: Property 'year' is missing in type
// '{ place: string; }' but required in type 'Setting'.
myNovel = {
  author: {
    name: 'Emily Bronte',
  },
  setting: {
    place: 'West Yorkshire',
  },
};
```

***
## 8/23/2024
## 7.3 Interface Extensions p. 130

### 7.3.1 Intro
* Sometimes, you end up with multiple interfaces that look similar.
* Let's reduce keyboard-typing and complexity by using the **extends** keyword to let one interface extend another interface.
* The parent/original interface is called the **base interface**. 
* One may *extend* from the base interface to a child **derived interface**. p. 130
	* A *derived interface* tells TS that all objects adhering to that derivd interface must also have all the same members of the base interface.
* **Interface extensions** are a nifty way to represt that one type of entity in your project is a *superset* of another entity.	* **Interface extensions** allow programmers to avoid having to type out the same code repeatedly across multiple interfaces. p. 131

#### 7.3.1.1 Example p. 130-131
* In this example, the **Novella** interface extends from **Writing**.
* Thus, the **Novella** interface requires objects to have members that belong to both **Novella.pages** and **Writing.title**.

```typescript
interface Writing {
  title: string;
}

interface Novella extends Writing {
  pages: number;
}

// ok
let myNovella: Novella = {
  pages: 195,
  title: "Ethan Frome",
};

let missingPages: Novella = {
  //^^^^^^^^^^^^

  // Error: Property 'pages' is missing in type
  // '{ title: string; }' but required in type 'Novella'
  title: "The Awakening",
}

let extraProperty: Novella = {
  //^^^^^^^^^^^^^

  // Error: Type '{ genre: string; name: string; strategy: string;}'
  // is not assignable to type 'Novella'.
  //   Object literal may only specify known properties,
  //   and 'genre' does not exist in type 'Novella'
  pages: 300,
  strategy: "baseline",
  style: "Naturalism",

};
```
***

### 7.3.2 Overriden Properties p. 131
* Derived interfaces may *override* properties from their base interface by declaring the property again with a different type.
* TS's type checker will enforce that an overridden property must be assignable to its base property.
* Most derived interfaces that redeclare properties do so either to make thos properties a more specific subset of a type union or to make the properties a type that extends from the base interface's type. 

#### 7.3.2.1 Example p. 132
* For example, this **WithNullableName** type is properly made non-nullable in **WithNonNullableName**.
* However, **WithNumericName** is *not* allowed as `number | string` and is not assignable to `string | null`:

```typescript
inteface WithNullableName {
  name: string | null;
}

// ok
interface WithNonNullableName extends WithNullableName {
  name: string;
}

// Error: Interface 'WithNumericName' incorrectly extends
// extends interface 'WithNullableName'.
// Type of property 'name' are incompatible.
// Type 'string | number' is not assignable to type 'string | null'.
// Type 'number' is not assignable to type 'string'.
interface WithNumericName extends WithNullableName {
  name: number | string;
}
```
***

### 7.3.3 Extending Multiple Interfaces p. 132
* An interface in TS is allowed to be declared as extending multiple other interfaces at once.
* Any number of **base interface** names separated by commas may be used after the `extends` keyword following the **derived interface's** name.
* *The derived interface will receive **all** members from every parent/base interface.*
* By marking an interface as extending multiple other base interfaces, one can both reduce code duplications and make it easier for object shapes to be reused across different areas of code. p. 133

#### 7.3.3.1 Example p. 132-133
* Here, the **GivesBothAndEither** has 3 methods:
	1. One on its own
	1. One from **GivesNumber**
	1. One from **GivesString**

```typescript
interface GivesNumber {
  givesNumber(): number;
}

interface GivesString {
  givesString(): string;
}

interface GivesBothAndEither extends GivesNumber, GivesString {
  giveEither(): number | string;
}

function useGivesBoth( instance: GivesBothAndEither ) {
  instance.giveEither(); // Type: number | string
  instance.giveNumber(); // Type: number 
  instance.giveString(); // Type: string
}
```

***

## 7.4 Interface Merging p. 133

* One of the important features of interfaces is their ability to **merge** with each other.
* Interface merging means that if 2 interfaces are declared within the same scope with the *same name*, they will join into one bigger interface under that name using all the fields of both base interfaces.

### 7.4.1 Merged interface examples p. 133-134
* Interface merging is not used a lot in regular TypeScript and LTS recommends avoiding it.
* However, merging interfaces *can* be useful when augmenting interfaces from **external packages**.
* This snippet declares a **Merged** interface with 2 properties: *fromFirst* and *fromSecond*.

```typescript
interface Merged {
  fromFirst: string;
}

interface Merged {
  fromSecond: number;
}
```
* which is equivalent to...

```typescript
interface Merged {
  fromFirst: string;
  fromSecond: number;
}
```

* Example of good use case for merged interface on p. 134. Consider the built-in global JS interface **Window**. You can do this (explained more in Chapter 11 / Chapter 13):

```typescript
interface Window {
  myEnvironmentVariable: string;
}

window.myEnvironmentalVariable; // Type: string 
```


### 7.4.2 Member Naming Conflicts p. 134
* Note that merged interfaces may not declare the same name of a property multiple times with **different types**. i.e., when you use the same property name, it *must be the same type for each occurrence!

#### 7.4.2.1 Examples of naming conflict p. 134-135
* In the below **MergedProperties** interface, the **same** property is allowed because it has the same type in both decclarations.
* But the **different** property raises an error b/c of a difference in type in the 2 declarations.

```typescript

interface MergedProperties {
  same: ( input: boolean ) => string;
  different: ( input: string ) => string;
}

interface MergedProperties {
  same: ( input: boolean ) => string; //ok
  
  different: ( input: number ) => string; //ok
  // Error: subsequent property declarations must have the same type
  // Property 'different' must be of type '(input: string) => string', 
  // but here has type '(input: number) => string'.

}
```
* Merged interfaces may, however, define a method of the same name and a different signature. Doing so creates a function overload for the method.
* The following example p. 135 has a **MergedMethods** interface which creates a *different* method that has 2 overloads:

```typescript

interface MergedMethods {
  different( input: string ): string;
}

interface MergedMethods {
   different( input: number): string; // ok
}
```
## 7.5 Summary
* Next chapter on **classes** will show how to set up multiple objects that have the same properties.

***

# Chapter 8: Classes p. 137
## 8/24/2024
## 8.1 Class Methods p. 137
### 8.1.1 Introduction
* TS generally understands methods the same way it understands standalone functions. 
* Parameter types default to *any* unless given a type or default value; calling a method requires an acceptable number of argumetns; return types can generally be inferred if the function is not recursive.

### 8.1.2 Example p. 137-138
* This code snippet defines a **Greeter** class with a *greet()* class method that takes in a single required parameter of type *number*:

```typescript
class Greeter {
  greet( name: string) {
    console.log( `${name}, do your stuff!`);
  }
}
// Ok
new Greeter().greet("Miss Frisby");

// Error: expected 1 argument, received 0 arguments
new Greeter().greet();

```
* Class Constructors are treated like typical class methods wrt their parameters.
* TS will perform type checking to make sure a correct number of arguments with correct types are provided to method calls.
* This **Greeted** constructor example also expects its *message: string* parameter to be provided (p. 138)

```typescript
class Greeted {
  constructor( message: string ) {
    console.log( `As I always say: ${message}!` );
  }
}

// ok
new Greeted( "take chances, make mistakes, get messy" );

// Error: expected 1 argument, received 0 arguments
new Greeted();
```

***

## 8.2 Class Properties
### 8.2.1 Introduction p. 138
* In TS, to read from or write to a property in a class, one must explicitly declare it in the class.
* Class properties are declared using the same syntax as interfaces: their name followed optionally by a type annotation.
* TS will not attempt to deduce what members may exist on a class from their assignments in a constructor.

#### 8.2.1.1 Examples p. 139
* In this example, **destination** is allowed to be assigned to and accessed on instances of the **FieldTrip** class because it is explicitly declared as a *string*.
* The *this.nonexistent* assignment in the constructor is not allowed because the class does not declare a *nonexistent* property:

```typescript
class FieldTrip {
  destination string;

  constructor( destination: string ) {
    this.destination = destination; // ok
    console.log( `We're going to ${this.destination}!` );

    this.nonexistent = destination;
    //   ^^^^^^^^^^^
    //  Error: Property 'nonexistent' does not exist on
    //  type 'FieldTrip'
  }
}
```
* Explicitly declaring class properties allows TS to quickly understand what is or is not allowed to exist on instances of classes.
* Later, when class instances are in use, TS uses that understanding to give a type error if code attempts to access a member of a class instance not known to exist, such as with this continuation's **trip.nonexistent**:

```typescript
const trip = new FieldTrip( "planetarium" );

//ok
trip.destination; 

//Error -- Property 'nonexistent' does not exist on type 'FieldTrip'.
trip.nonexistent;
```

***
### 8.2.2 Function Properties p. 139
#### 8.2.2.1 Introduction
* Let's recap the fundamentals of JS method scoping and syntax.
* JS contains 2 syntaxes for declaring a member on a class is callable function: **method** and **property**.
* LTS has already illustrated the method of approach: `myFunction() {...}`.
* Example p. 140:

```typescript
class WithMethod {
  myMethod() {...}
}

new WithMethod().myMethod === new WithMethod().MyMethod; // true
```
* The other syntax is to declare a property whose value happens to be a function.
* This creates a new function *per instance* of the class. This can be useful with the `() =>` arrow functions. whose **this** scope should always point to the class instance.
* This **WithProperty** class contains a single property of name **myProperty** and `type() => void` that will be recreated for each class instance:

```typescript
class WithProperty {
  myProperty: () => {...}
}

new WithMethod().myProperty === new WithMethod().MyProperty; // false
```



#### 8.2.2.2 Passing a function as an argument to a class *WithPropertyParameters*

* Function properties can be given parameters and return types using the same syntax as class methods and standalone functions. p. 140
* After all, they're a value assigned to a class member; the value just happens to be a function.
* The following example (p. 140-141) has a **WithPropertyParameters** class which has a *takesParameters* property.
* The *takesParameters* property is of type: `( input: string ) => number`, which is an arrow function.

```typescript
class WithPropertyParameters {
  takesParameters = ( input: boolean ) => input ? "Yes" : "No";
}

const instance = new WithPropertyParameters();

//ok
instance.takesParameters( true );

// Error: Argument of type 'number' is not
// Assignable to parameter of type 'boolean'
instance.takesParameters( 123 );
                          ^^^

```

*** 
### 8.2.3 Initialization Checking p. 141
* With strict compiler settings enabled, TS will check that each property declared--whose type does not include *undefined*--is assinged a value in the constructore.
* This strict initialization checking is useful b/c it prevents code from accidentally forgetting to assign a value to a class property.

#### 8.2.3.1 Intialization Examples p. 141-142
* The following **WithValue** class does not assign a value to its *unused* property; TS recognizes this as an error:

```typescript

class WithValue {

  //ok
  immediate = 0;
  
  // ok -- set in the constructor
  later: number;
  
  // ok -- allowed to be undefined
  mayBeUndefined: number | undefined;
  
  //Error: property 'unused' has no intializer
  // and is not definitely assigned in the constructor
  constructor() {
    this.later = 1;
  }
}
```
* Without strict initialization checking, a class instance could be allowed to access a value that might be *undefined* even though the type system says it *can't be*.
* This following example (p. 142) would compile happily *if strict initialization checking didn't happen; but the resultant JS would crash at runtime:

```typescript
class MissingInitializer {
  property: string;
}

// TypeError: Cannot read property 'length' of undefined
new MissingInitializer().property.length;
```
* The billion-dollar mistake strikes again!
* See Chapter 12 on Using IDE features for more on the *strictPropertyInitialization* compiler option.

***

### 8.2.3.2 Definitely assigned properties p. 142
* Although strict initialization checking is useful most of the time, one may comr across some cases where a class property is *intentionally* able to stay unassigned after the class constructor.
* One may use a `!` exclaimation point (bang) after the name of a property to disable it's initialization check.
* This tells TS that the peropty will be assigned a value other than *undefined* before its first usage.
* Example p. 142-143:

```typescript
class ActivitiesQueue {
  pending!: string[]; //ok

  initialize( pending: string[] ) {
    this.pending = pending;
  }

  next() {
    return this.pending.pop();
  }
}

const activities = new ActivitiesQueue();

activities.initialize( ['eat', 'sleep', 'learn'])
activities.next();
```

***
### 8.2.4 Optional Properties p. 143
* Classes in TS may declare a property as optional with a `?` question mark after its declaration name, just like with TS interfaces.
* In this Example (p. 143), the optional **property** property is not allowed to be assigned in the class constructor regardless of strict property initialization checking:

```typescript
class MissingInitializer {
  property?: string;
}

//ok
new MissingInitializer().property?.length; 

// Error: Object is possibly 'undefined'
new MissingInitializer().property.length;
```



***
### 8.2.5 Read-Only Properties p. 143
* TS classes may declare a property as read-only by adding the **readonly* keyword before its declaration name--just like with TS interfaces.
* Per note in textbox on p. 144, might be best to use `#` (pound sign / hashtag) to specify private fields in case external 3rd party devs of your library might not realize that you've marked a property as read only. So probably use **JS private fields with *#*** instead of TS read-only properties.
* Example p. 144

```typescript
class Quote {
  readonly text: string;

  constructor( text: string ) {
    this.text = ;
  }

  emphasize() {

    // Error: cannot assign to 'text' bc it is a 
    // read-only property
    this.text += "!";
         ^^^^
  }
}

const quote = new Quote(
  "There is a brilliant child locked in every student."
);

// Error: Cannot assign to 'text' because it is a
// read-only property
Quote.text = "Ha!";
```
* Additional more complicated corner-case example on p. 144-145.

***

## 8.3 Classes as Types p. 145
* Classes are relatively unique in the type system in that a class declaration creates both a runtime value--the class *itself*--as well as a **type** that can be used in type annotations.
* Consider Example (p. 145-146). 
	* The name of the *Teacher** class is used to annotate a **teacher** variable. 
	* This tells TS that it should be assigned *only* values that are assignable to the **Teacher** class--including instances of the **Teacher** class itself!

```typescript
class Teacher {
  sayHello() {
    console.log("Take chances, make mistakes, get messy!");
  }
}

let teacher: Teacher;

teacher = new Teacher(); //ok

// Error: type 'string' is not assignable to 
// type 'Teacher'
teacher = "Wahoo!";
```
* Interestingly, TS will consider any object type that happens to include all the same members of a class to be assignable to the class.
* This is bc TS's structural typing cares *only* about the shape of the objects--*not* how the object is declared.
* Example (p. 146), **withSchoolBus** takes in a parameter of type **SchoolBus**. That can be satisfied by *any* object that happens to have a **getAbilities** property of type `() => string[]`, such as an instance of the **SchoolBus** class.

```typescript
class SchoolBus {
  getAbilities() {
    return [ "magic", "shapeshifting" ];
  }
}

function withSchoolBus( bus: SchoolBus ) {
  console.log( bus.getAbilities() );
}

// ok
withSchoolBus( new SchoolBus() );

// ok
withSchoolBus(
  {
    getAbilities: () => [ "transmogrification" ],
  }
);

withSchoolBus( {

  // Error: Type 'number' is not assignable to type
  // 'string[]'
  getAbilities: () => 123,

});
```

***
## 8/25/2024
## 8.4 Classes and Interfaces p. 147
### 8.4.1 Introduction
* Back in Chapter 7: Interfaces, I showed you how interfaces allow TS developers to set up expectations for object shapes in code.
* TS allows a class to declare its instances as adhering to an interface by adding the **implements** keyword after the class name, followed by the name of an interface.

### 8.4.2 Examples p. 147-148
* In this example, the **Student** class correctly implements the **Learner** interface by including its property *name* and its method *study()*, but the **Slacker** is missing a *study()* and thus results in a type error.

```typescript
interface Learner {
  name: string;
  study( hours: number ): void;
}

class Student implements Learner {
  name: string;

  constructor( name: string ) {
    this.name = name;
  }

  study( hours: number ) {
    for ( let i=0; i < hours; i += 1 ) {
      console.log( "...studying..." );
    }
  }
}

// Error: Class Slacker doesn't implement interface 
// 'Learner' properly b/c Property 'study' is missing 
class Slacker implements Learner {
  name = "Rocky";
}
```
* Marking a class as implementing an interface does not change anything about how the class is used.
* If the class already happened to match up to the interface, TS's type checker would have allowed its instances to be used in places where an instance of the interface is required anyways.
* TS won't even infer the types of methods/properties on the class from teh interface: if we had added a **study( hours ) {}** method to the **Slacker** example, TS would consider the **hours** parameter an implicit **any** unless we gave it a type annotation.
* Consider this new version (p. 148) of the **Student** class created in the previous example

```typescript
class Student implements Learner {
  // error: Member 'name' implicitly has 
  // type 'any' which is not allowable
  name;

  study( hours) {
    // Error: Parameter 'hours' implicitly
    // has an 'any' type
  }
}
```
* This is raising type errors with the *any* type.
* Implementing an interface is purely a safety check.
* It does not copy any interface members onto the class definition for you.
* Rather, implementing an interface signals your intention to the type checker and raises type errors int he class definition--rather than later on where class instances are used.
* It's similar in purpose to adding a type annotation to a variable even though it has an initial value.

***

### 8.4.3 Implementing Multiple Interfaces p. 149
* Classes in TypeScript are allowed to be declared as implementing multiple interfaces.
* The list of implemented interfaces for a class may be any number of interface names with commas in-between.

#### 8.4.3.1 Examples p. 149-150
* **Example 1**, p. 149, both classes are required to have a least a *grades* property to implement the **Graded** interface and a *report* property to implement the **Reporter** interface.
	* The **Empty** class has two type errors for failing to implement either of the interfaces properly.

```typescript
interface Graded {
  grades: number[];
}

interface Reporter {
  report: () => string;
}

class ReportCard implements Graded, Reporter {
  grades: number[];

  constructor( grades: number[] ) {
    this.grades = grades;
  }

  report() {
    return this.grades.join(", ");
  }

}

class Empty implements Graded, Reporter {}
      ^^^^^
// Error, class 'Empty' incorrectly implements 
// interface 'Graded' (see more on p. 149)


// Error, class 'Empty' incorrectly implements 
// interface 'Reporter' (see more on p. 149)
```

* In practice, there may be some interfaces whose definitions make it impossible to have a class that implements both interfaces.
* Attempting to declare a class implementing two conflicting interfaces will result in at least one type error on the class.
* **Example 2**, p. 150, has two interfaces: (a) **AgeIsANumber**; and (b) **AgeIsNotANumber**. Neither the **AsNumber** class nor the **NotAsNumber** class properly implements both interfaces.

```typescript
interface AgeIsANumber {
  age: number;
}

interface AgeIsNotANumber {
  age:() => string;
}

// Error: Property 'age' in type 'AsNumber' is not assignable
// to the same property in base type 'AgeIsNotANumber'
class AsNumber implements AgeIsNumber, AgeIsNotANumber {
  age = 0;
}


// Error: Property 'age' in type 'NotAsNumber' is not assignable
// to the same property in base type 'AgeIsANumber'
class NotAsNumber implements AgeIsNumber, AgeIsNotANumber {
  age() { return ""; }
}
```

***

## 8.5 Extending a Class p. 151

### 8.5.1 Intro p. 151
* When one extends a class in JS, one can add type checking to the derived class using TS.
* Example on p. 151:

```typescript
class Teacher {
  teach() {
    console.log( "The surest test of discipline..." );
  }
}

class StudentTeacher extends Teacher {
  learn() {
    console.log( "I cannot afford the luxury of a closed mind." );
  }
}

const teacher = new StudentTeacher();

// OK (defined on base class)
teacher.teach();

// OK (defined on subclass aka derived class)
teacher.learn();

// Error: Property 'otherFunction' does not exist 
// on type 'StudentTeacher'
teacher.otherFunction();
```
***

### 8.5.2 Extension Assignability p. 151
* Subclasses inherit members from their base class much like derived interfaces extend base interfaces.
* Instances of subclasses have all the members of their base class and thus may be used wherever an instance of the base is required.
* If a base class doesn't have all the members of a subclass does, then it can't be used when the more specific subclass is required.

#### 8.5.2.1 Examples 
* **Example 1** p. 151-152: instances of the following **Lesson** class may not be used where instances of its derived **OnlineLesson** are required, but derived instances may be used to satisfy either the base class or the subclass:

```typescript
class Lesson {
  subject: string;

  constructor( subject: string ) {
    this.subject = subject;
  }
}

class OnlineLesson extends Lesson {
  url: string;

  constructor( subject: string, url: string ) {
    super( subject );
    this.url = url;
  }
}

let lesson: Lesson;

// ok
lesson = new Lesson( "coding" );

// ok
lesson = new OnlineLesson( "coding", "oreilly.com");

let online: OnlineLesson;
online = new OnlineLesson( "coding", "oreilly.com" ); // ok

// error: property 'url' is missing in type 'Lesson'
// but required in type 'OnlineLesson'
online = new Lesson( "coding" );
```

* Per TS' structural typing, if all members on a subclass already exist on its base class with the same type, then instances of the base class are still allowed to be used in place of the subclass.
* **Example 2**, p. 152, has **LabeledPastGrades** only adds an optional property to **PastGrades**, so instances of the base class may be used in place of the subclass:

```typescript
class PastGrades {
  grades: number[] = [];
}

class LabeledPastGrades extends PastGrades {
  label?: string;
}

let subClass: LabeledPastGrades;

subClass = new LabeledPastGrades(); // ok
subClass = new PastGrades(); //ok
```
***

### 8.5.3 Overridden Constructors p. 153
#### 8.5.3.1 Intro
* As with vanilla JS, subclasses are not required by TS to define their own constructor. 
* Subclasses (aka derived classes) without their own constructor implicitly use the constructor of their base class (aka superclass) using the *super* keyword.

#### 8.5.3.2 Examples p. 153-154
* **Example 1**, the constructor for the **PassingAnnouncer** derived class correctly calls the constructor fromt eh base class using a *number* argument, while the **FailingAnnouncer** gets a type error.

```typescript
class GradeAnnouncer {
  message: string;
  
  constructor( grade: number ) {
    this.number = grade >= 65
    ?
      "Maybe next time..."
    :
      "You pass!";
  }
}

class PassingAnnouncer extends GradeAnnouncer {
  constructor() {
    super( 100 );
  }
}

class FailingAnnouncer extends GradeAnnouncer {
  constructor() {}

  // Error: constructors for subclasses must contain
  // a 'super' keyword call.
}
```
* Per JS rules, the constructor of a subclass must call the base constructor before accessing **this** or **super**.
* TS will report a type error if it sees a *this* or a *super* bbeing accessed before **super()**.
* **Example 2**, the following **ContinuedGradesTully** class erroneously refers to *this.grades* in its constructor **before** calling to *super()*.

```typescript
class GradesTally {
  grades: number[] = [];

  addGrades( ...grades; number[] ) {
    this.grades.push(...grades);
    return this.grades.length;
  }
}

class ContinuedGradesTally extends GradesTally {
  constructor( previousGrades: number[] ) {

    // Error b/c this is called *before* super()
    this.grades = [...previousGrades]:

    super();

    // ok b/c this is called *after* super()
    console.log("Starting with length", this.grades.length);
  }
}
```

***
### 8.5.4 Overridden Methods p. 154
* Subclasses may redeclare new methods with the same names as the base class.
* Remember, since subclasses can be used wherever the original class is used, the types of the new methods must be usable in place of the original methods.
* Example on p 155:

```typescript
class GradeCounter {
  countGrades( grades: string[], letter: string ) {
    return grades.filter( grade => grade === letter ).length;
  }
}

class FailureCounter extends GradeCounter {
  countGrades( grades: string[] ) {
    return super.countGrades( grades, "F" );
  }
}

class AnyFailureChecker extends GradeCounter {
  countGrades( grades: string[] ) {

    // Error see full text on p. 155
    return super.countGrades( grades, "F" ) !== 0;
  }
}

const counter: GradeCounter = new AnyFailureChecker();

// Expected type: number
// Actual number: boolean

const count = counter.countGrades( ["A", "C", "F"] );
```
***

### 8.5.5 Overridden Properties p. 155
* Subclasses may explicitly redeclare properties of their base class with the same name, as long as the new type is assignable to the type on the base class.
* As with overridden methods, subclasses must structurally match up with base classes.

#### 8.5.5.1 Examples p. 155-156
* **Example 1**, the base class **Assignment** declares its *grade* to be of type `number | undefined`.
	* Meanwhile, the subclass **GradedAssignment** declares it as a `number` that must always exist.
	* Expanding the allowed set of values of a property's union type is not allowed, as doing so would make the subclass property no longer assignable to the base class property's type.

```typescript
class Assignment {
  grade?: number;
}

class GradedAssignment extends Assignment {
  grade: number;

  constructor( grade: number ) {
    super();
    this.grade = grade;
  }
}
```
* **Example 2**  (p. 156), **VagueGrade**'s *value* tries to add `| string` on top of the base class **NumericGrade**'s number type, causing a type error:

```typescript
class NumericGrade {
  value = 0;
}

class VagueGrade extends NumericGrade {

  // Error: Property 'value' in type 'NumberOrString'
  // is not assignable to the same property in base 
  // type 'JustNumber'.
  // Type 'string | number' is not assignable to type
  // 'number'. Type 'string' is not assignable to
  // type 'number'.

  value = Math.random() > 0.5
    ? 1: "...";
}

const instance: NumericGrade = new VagueGrade();

// Expected type: number
// Actual type: number | string
instance.value;
```

***

## 8/26/2024
## 8.6 Abstract Classes p. 156
### 8.6.1 Intro p. 156-158
* Sometimes, it's useful to create a base class that does not declare any methods; instead, it must rely on derived subclasses to provide methods.
* These are called **abstract classes**, and created using the *abstract* keyword in front of the class name and in front of any method intended to be abstract.

### 8.6.2 Examples p. 157-158
* In this example, the **School** class and its **getStudentTypes** method are marked as *abstract*.
* Its subclasses--**Preschool** and **Absence**--are therefore expected to implement *getStudentStypes()*.

```typescript
abstract class School {
  readonly name: string;

  constructor( name: string ) {
    this.name = name;
  }

  abstract getStudentTypes(): string[];

}

class Preschool extends School {
  getStudentTypes() {
    return ["preschooler"];
  }
}

// Error: nonabstract class 'Absence' does not
// implement inherited abstract member 'getStudentTypes'
// from class 'School'
class Absence extends School { }
```
* **An abstract class *cannot* be instantiated directly.**
	* This is because that abstract class does not have definitions for some methods that its implementation may assume do exist.
* Only nonabstract classes (aka **concrete class**) can be instantiated.
* Continuing the previous example, attempting to call a new **School** results in a TS type error b/c *School* is an abstract class:

```typescript
let school: School;

school = new Preschool("Signal Hill Day Care"); //ok

// Error!
school = new School("Burr's Lane Jr. High");
```
* Abstract classes are often used in frameworks where consumers are expected to fill out details of a class.
* The class may be used as a type annotation to indicate values must adhere to the class--as with the earlier example of **school: School**--but creating new instances must be done with subclasses.

***

## 8.7 Member Visibility p. 158
### 8.7.1 JS Intro and TS History p. 158
* JS includes the ability to start the name of a class member with the `#` pound sign to mark it as a **private** class member.
* Private class members may *only* be accessed by instances of that class.
* JS runtimes enforce that privacy by throwing an error if an area of code outside the class tries to access the private method or property.
* TS's class support predates the introduction of **'officially supported *true*' privacy by # prefix** by JS in [ES2022](https://www.w3schools.com/js/js_2022.asp#mark_private_methods).
* While TS supports private class members, it also allows a more nuanced set of privacy definitions on class methods and class properties.
* TS's member visibilities are achieved by adding one fo the following keywords before the declaration name of a class member:
	1. **public** (default)-- allowed to be accessed by anybody, anywhere
	1. **protected** -- allowed to be accessed only by the class itself and its subclasses
	1. **private** -- allowed to be accessed *only* by the class itself
* The above keywords exist purely within the type system.
* The keywords are *removed* along with other type system syntax when TS code is transpiled to pure JS.

### 8.7.2 Example 1 p. 159
* Here, the **Base** class declares two *private* members, one *protected* and one *private*. It also has one 'true' private member using ES2022 native JS syntax **#truePrivate**.
* **Subclass** is allowed to access the *private* and *protected* members but not the **private** or **#truePrivate** members.

```typescript

class Base {
  isPublicImplicit = 0;
  public isPublicExplicit = 1;
  protected isProtected = 2;
  private isPrivate = 3;
  #truePrivate = 4;
}

class Subclass extends Base {
  examples() {
    this.isPublicImplicit; // ok
    this.isPublicExplicit; // ok
    this.isProtected; // ok

    // Error: Property 'isPrivate' is private
    // and only accessible within class 'Base'
    this.isPrivate;
    
    // Error: Property '#truePrivate' is private
    // and only accessible within class 'Base'
    this.#truePrivate;
  }
}

new Subclass().isPublicImplicit; //ok
new Subclass().isPublicExplicit; //ok

new Subclass().isProtected; //Error
new Subclass().isPrivate; //Error
```
* The key difference between TS's member visibilities and JS's true private declarations is that TS's exist only in the type system whereas JS's private declarations persist in the JS runtime.
* A TS class member declared as *protected* or *private* will compile to the same JS as if it were declared *public* explicitly or implicitly.
* As with interfaces and type annotations, **visibility keywords are erased when outputting JS.**
* *Only `#private` field*s are truly private in runtime JS.

***
### 8.7.3 Example 2 p. 160
* Visibility modifiers may be marked along with *readonly*. To declare a member both as *readonly* and with an explicit visibility, the visibility comes **first**.
* This **TwoKeywords** class declares its *name* member as both *private* and *readonly*.

```typescript
class TwoKeywords {
  private readonly name: string;

  constructor() {
    this.name = "Anne Sullivan"; // ok
  }

  log() {
    console.log( this.name ); // ok
  }
}

const two = new TwoKeywords();

// Error: Property 'name' is private and
// only accessible within class 'TwoKeywords'
// Error: Cannot assign to 'name' bc
// it is a read-only property
two.name = "Savitribai Phule";
```
* Note that it is *not* permitted to mix the *old TS member visibility keywords* (**public**, **protected**, **private**) and the *newer official ES2022* **#private** fields.
	* Private fields are always private by default--so there is no need to additionally mark them with the old TS **private** keyword.

### 8.7.4 Static Field Modifiers p. 161
* JS allows declaring members on a class itself--rather than on its instances.
* Declaring members on a class *itself* is accomplished with the **static** keyword.
* TS supports using the *static* keyword both on its own and with readonly and/or with visibility keywords.
* **Note the order:** (1) First the visibility keywords; (2) then *static*; and (3) finally, *readonly*. 

#### 8.7.4.1 Static field example p. 161

```typescript
class Question {
  protected static readonly answer: "bash";
  protected static readonly prompt = 
    "What's an ogre's favorite programming language?";

  guess( getAnswer: (prompt: string) => string ) {
    const answer = getAnswer(Question.prompt);

    //ok
    if ( answer === Question.answer ) {
      console.log( "You got it!" );
    } else {
      console.log( "Try again..." )
    }
  }
}

// Error: Property 'answer' is protected and only
// accessible within class 'HasStatic' and its subclasses
Question.answer;
```

* Using read-only and/or visibility modifiers for static class fields is useful for restricting those fields from being accessed or modified outside their class.
***

## 8.8 Summary of Chapter 8: Topics covered p. 161
1. Declaring and using class methods and properties
1. Marking properties *read-only* and/or *optional*
1. Using class names as **types** in type annotations
1. Interfaces to enforce class instance shapes
1. Extending base classes to create derived/subclasses
1. Abstract Classes
1. Adding Type System modifiers to class fields 

***

# Chapter 9: Type Modifiers p. 163
* JH: I believe the point of this chapter is to show how one can *change* types, called *casting* and *coercion* in other languages.

## 9.1 Top Types 
* Recall the concept of a *bottom type* from Chapter 4; it is a type that can have no possible values and can't be reached.
* The opposite is a **top type** aka a **universal type**.
	* This is type that can represent *any* possible value in a system.
* Values of all other types can be provided to a location whose type is a top type.
* i.e., *all* types are assignable to a top type. 

***

### 9.1.1 any, Again p. 163
* The **any** type can act as a *top type*--b/c a value of any type can be assigned into that variable.
* **any** is generally used when a location is allowed to accept data of any type, such as parameters being captured by `console.log()`.

```typescript
let anyValue: any;
anyValue = "Lucille Ball"; //ok
anyValue = 123; //ok

console.log( anyValue ); // ok
```

* However, the problem with **any* is that it explicitly tells TS *not* to perform the usual type checking on that variable's *assignability* or *members*.
* That evades the entire point of TS's type safety! 
* Example p. 164, the **name.toUpperCase()** call definitely will not crash. But b/c *name* is declared as type **any**, TS will not register a type complaint.

```typescript
function greetComedian( name: any ) {
  // No type error...
  console.log( `Announcing ${name.toUpperCase()}!` );
}

// No compiler typechecking error--Passes!
// But! runtime error: name.toUpperCase() is not a legit function
greetComedian( { name: "Bea Arthur" } );
```

* The **unknown** type is much safer than **any**.

***

### 9.1.2 Unknown p. 164
* The **unknown** type in TS is its true *top type*.
* **unknown** is similar to *any* in that all objects may be passed to variables of type **unknown**.
* The key differene with **unknown** is that TypeScript is much more restrictive about values of type **unknown**
	* TS does not allow directly accessig properties of **unknown** typed values
	* **unknown** is not assignable to types that are *not* a top type (i.e., *any* or *unknown*)
* Attempting to access a property of any *unknown* typed value will cause a TS type error, per this Example p. 164 - 165:

```typescript
function greetComedian( name: unknown ) {

  // Error: Object is of type 'unknown'
  console.log( `Announcing ${ name.toUpperCase() }!` );
}
```
* The only way TS will allow code to access members on a variable of type **unknown** is if the value's type is *narrowed*, such as using type assertion, or using *instanceof*, or using *typeof*.
* Example, p. 165

```typescript
function greetComedianSafety( name: unknown ) {
  if ( typeof value === "string" ) {

    // ok
    console.log( `Announcing ${ name.toUpperCase() }!` ); 
  } else {
    console.log( "Well, I'm off!" );
  }
}

greetComedianSafety( "Betty White" ); // Logs: 4 (why??)
greetComedianSafety( {} ); // Does not log
```
* Those two restrictions make **unknown** a much safer type to use than **any**.
* **Note: one should generally prefer to use *unknown* instead of *any* when possible.**

***
## 8/27/2024
## 9.2 Type Predicates
* We've previously seen how JS constructs like *instanceof* and *typeof* can be used to narrow types. But this may get lost within the logic of a function().

***

### 9.2.1 Examples 1 + 2, p. 165 - 166

```typescript
function isNumberOrString( value: unknown ) {
  return [ 'number', 'string' ].includes( typeof value );
}

function logValueIfExists( value: number | string | null | undefined ) {
  if( isNumberOrString( value ) ) {

    // Type of value: number | string | null | undefined
    // Error: Object is possibly undefined
    value.toString();

  } else {
    console.log( "Value does not exist: ", value);
  }
}
```

* TS has a special syntax for functions that return a boolena meant to indicate whether an argument is a particular type.
* This is referred to as a **type predicate**, also sometimes called a 'user-defined type guard': you the developer are creating your own type guard akin to **instanceof** or **typeof**.
* Type predicats are commonly used to indicate whether an argument passed in as a parameter is a more specific type than the parameter's.
* Type predicate's return types can be declared as the name of a parameter, the **is** keyword, and the type:

```typescript
function typePredicate( input: WideType ): input is NarrowType;
```
***

### 9.2.2 Example 3 p. 166 - 167
* We can change the previous example's helper function to ahve an explicit return type that explicitly states `value is number | string`.
* TS will then be able to infer that blocks of code...


```typescript
function isNumberOrString( value: unknown ): value is number | string {
  return ['number', 'string'].includes(typeof value);
}

function logValueIfExists( value: number | string | null | undefined ) {
  if ( isNumberOrString(value) ) {
    
    // Type of value: number | string
    value.toString(); //ok

  } else {

    // Type of value: null | undefined
    console.log( "value does not exist: ", value );
  }
}
```
* You can think of a type predicate as returning not just a boolean, but also an indication that the argument was that more specific type.
* Type predicates are often used...

***

### 9.2.3 Example 4 p. 167
```typescript

interface Comedian {
  funny: boolean;
}

interface StandupComedian extends Comedian {
  routine: string;
}

function isStandupComedian( value: Comedian ): value is StandupComedian {
  return 'routine' in value;
}

function workWithComedian ( value: Comedian ) {
  if ( isStandupComedian(value) ) {

    // Type of value: StandupComedian
    console.log( value.routine ); // ok
  }

  // Type of value: Comedian
  // Error: Property 'routine' does not exist on type 'Comedian'
  console.log( value.routine );
                     ^^^^^^^
}
```
***

### 9.2.4 Example 5 p. 168

```typescript
function isLongString( input: string | undefined ): input is string {
  return !!( input && input.length >= 7 );
}

function workWithText( text: string | undefined ) {
  if( isLongString(text) ) {

    // Type of text: string
    console.log( "Long text: ", text.length );

  } else {
    
    // Type of text: undefined
    // Error: Property 'length' does not exist on type 'never'
    console.log( "Short text: ", text?.length);
                                       ^^^^^^
  }
}
```
* Type predicates that do more than verify the tyep of a property or value are easy to misuse.
* LTS generally recommends avoiding them when possible.
* *Simpler* type predicates are sufficient for most cases. 

***
## 9.3 Type Operators
### 9.3.0 Introduction
* Not all types can be represented using only a keyword or a name of an existing type.
* It can sometimes be necessary to create a new type that *combines* both keyword *and* an existing type, performing some transformation on the properties of an existing type.

***
### 9.3.1 keyof p. 169
* JS objects can have members retrieved using dynamic values, which are commonly (but not necessarily) *string* typed.
* Representing these keys in the type system can be tricky.
* Using a catchall primitive such as *string* would allow invalid keys for the container value.
* That's why TS when using stricter configuration settings--covered in Chapter 13--would report an error on the **ratings[key]** as seen in the next example.
* Type *string* allows values not allowed as properties on the **Ratings** interface and **Ratings** doesn't declare an index signature to allow any *string* keys.

#### 9.3.1.1 keyof Examples 1, 2, and 3 p. 169-170
```typescript
interface Ratings {
  audience: number;
  critics: number;
}

function getRatings( ratings: Ratings, key: string ): number {
  
  // Error: Element implicitly has an 'any' type because 
  // expression of type 'string' can't be used to index
  // type 'Ratings'.
  // No index signature with a parameter of type 'string'
  // was found on type 'Ratings'.
  return ratings[key];
         ^^^^^^^^^^^^
}

const ratings: Ratings = { audience: 66, critic: 84 };

getRating( ratings, 'audience' ); // ok

getRating( ratings, 'not valid' ); // Ok, but *shouldn't* be
```
* Another option would be to use a type union of literals for the allowed keys.
* That would be more accurate in properly restricting to only the keys that exist on the container value:

```typescript
function getRating( ratings: Ratings, key: 'audience' | 'critic' ): number {
  return ratings[key]; // ok
}

const ratings: Ratings = { audience: 66, critic: 84 };

getCountLiteral(ratings, 'audience'); // ok

// Error: Argument of type 'not valid' is not assignable
// to parameter of type 'audience | critic'
getCountLiteral(ratings, 'not valid');
                          ^^^^^^^^^
```
* However, what if the interface has dozens or more members?
* you would have to type out each of those members' keys into the union type and keep them up-to-date. What a pain!
* Instead, TS provides the **keyof** operator that takes in an existing type and gives back a union of all the keys allowed on that type, such as a type annotation.
* Here, **keyof Ratings** is equivalent to 'audience | critic' but is much quicker to write out and won't need to be manually updated if the **Ratings** interface ever changes.

```typescript
function getCountKeyof( ratings: Ratings, key: keyof Ratings ): number {
  return ratings[key]; // ok
}

const ratings: Ratings = { audience: 66, critic: 84 };

getCountKeyof( ratings, 'audience' ); // ok

// Error: Argument of type 'not valid' is not assignable
// to parameter of type 'keyof Ratings'.
getCountKeyof( ratings, 'not valid' );
                        ^^^^^^^^^^^
```
* **keyof** is a great feature for creating union types based on the keys of existing types.
* It also combines well with other type operators in TS, allowing for some very nifty patterns you'll see later in this chapter an in Chapter 15.

***
### 9.3.2 typeof p. 170
* Another type operator provided by TS is *typeof*.
* This keyword returns the type of a provided value.
* This can be useful if the value's type would be annoyingly complex to write manually.

#### 9.3.2.1 typeof example p. 171
* In this example, the **adaptation** variable is declared as being the same type as **original**:

```typescript
const original = {
  medium = "movie",
  title = "Mean Girls",
};

let adaptation: typeof original;

if (Math.random() > 0.5 ) {
  adaptation = {...original, medium: "play"}; // ok
} else {

  // error: type 'number' is not assignable to type 'string'
  adaptation = {...original, medium: 2 };
                             ^^^^^^

}
```
* Although the **typeof type operator** visually looks like the ***runtime* typeof operator** used to return a string description of the value's type, the **two are different**!
* the JS operator is a *runtime* operator that returns the string of a type.
* in contrast, the TS version can *only* be used in types and *won't* appear in compiled code. B/c the TS version is a type operator!

***
### 9.3.3 keyof typeof p. 171
* *typeof* retrieves the type of a value; *keyof* retrieves the allowed keys on a type.
* TS allows the 2 keywords to be chained together to succinctly retrieve the allowed keys on a value's type.
* Putting them together, the *typeof* operator becomes wonderfully useful for working with *keyof* operations.
#### 9.3.3.1 logRating example p. 171-172
* In this example, the **logRating** function is meant to take in one of the keys of the *ratings* value.
* Instead of creating an interface, this code uses **keyof typeof** to indicate that *key* must be one of the keys on the type of the *ratings* value:

```typescript
const ratings = {
  imdb: 8.4,
  metacritic: 82,
};

function logRating( key: keyof typeof ratings ) {
  console.log( ratings[key] );
}

logRating( "imdb" ); //ok

// error: Argument of type 'missing' is not assignable
// to the parameter of type ' imdb | metacritic '
logRating( "invalid" );
```
* By combining *typeof* and *keyof*, we get to save ourselves the pain of writing out--and having to update--types representing the allowed keys on objects that don't have an explicit interface type.

***

## 9.4 Type Assertions
### 9.4.1 Introduction
* TS works best when your code is *strongly typed* aka all the values in your code have precisely known types.
* Features such as top types and type guards provide ways to wrangle complex code into being understood by TS's type checker.
* However, sometimes it's not reasonably possible to be 100% accurate in telling the type system how your code is meant to work.
* For example, **JSON.parse** intentionally returns the top type **any**.
* There's no way to safely inform the type system that a particular string value given to **JSON.parse** should return any particular value type.
* TS provides a syntax for overriding the type system's understanding of a value's type: a 'type assertion', also known as a **type cast**.
* On a value that is meant to be a different type, you can place the **as** keyword followed by a type.
* TypeScript will defer to your assertion and treat the value *as that type*.

#### 9.4.1.1 Example p. 174
* In this snippet, it is possible that the returned result from **JSON.parse** is meant to be a type such as *string[]*, *[string, string]*, or `["grace", "frankie"]`.
* The snippet uses type assertions for 3 of the lines of the code to switch the type from **any** to one of these:

```typescript
const rawData = `["grace", "frankie"]`;

// Type: any
JSON.parse(rawData);

// Type: string[]
JSON.parse(rawData) as string[];

// Type: [string, string]
JSON.parse(rawData) as [string, string];

// Type: ["grace", "frankie"]
JSON.parse(rawData) as ["grace", "frankie"];
```
* Type assertions exist only in the TS type system. As usual, they are removed when transpiled into JS and are not available during runtime.
* The previous code would like like **this** when compiled:

```typescript
const rawData = `["grace", "frankie"]`;

// Type: any
JSON.parse(rawData);

// Type: string[]
JSON.parse(rawData);

// Type: [string, string]
JSON.parse(rawData);

// Type: ["grace", "frankie"]
JSON.parse(rawData);
```
* **Note: there is an older casting syntax in the textbox at the bottom of p. 173. it should not be used b/c it conflicts with JSX syntax.** 
* TS best practice is generally to **avoid using type assertions when possible.**
* It's best for your code to be fully typed and to not need to interfere with TS' understanding of its types using assertions.
* But occasionally there will be cases where type assertions are useful, even necessary.

***
### 9.4.2 Asserting Caught Error Types p. 174
* Error handling is another place where type assertions may come in handy.
* It is generally impossible to know what type a caught error in a **catch** block will be bc the code in the **try** block will be bc the code in the *try* block may unexpectedly throw any object different from what you expect.
* Furthermore, although JS best practic is to always throw an instance of the **Error** class, some projects instead throw string literals aor other surprising values.
* If you are *absolutely* confiden that an area of code will only throw an instance of the **Error** class you can use a type assertion to treat a caught assertion as an **Error**.
* This snippet accesses the *message* property of a caught *error* that it assumes is an instance of the **Error** class:

```typescript
try  {
  // ... code may the throw an error ...
} catch (error) {
  console.warn( "Oh no!", (error as Error).message );
}
```
* It is generally safer to use a form of type narrowing such as an *instanceof* check to ensure the thrown error is the expected error type.
* This snippet checks whether the thrown error is an instance of the **Error** class to know whether to log that message or the error itself:

```typescript
try {
  // ... code may the throw an error ...
} catch(error) {
  console.warn( "Oh no!", (error instanceof Error ? error.message: error);
}
```

***

### 9.4.3 Non-null Assertions  p. 175
* Another common use case for type assertions is to remove *null* and/or *defined* from a variable that only theoretically, not practically, might include them.
* That situation is so common that TS includes a shorthand for it.
* Instead of writing out **as** and the full type of whatever a value is excluding **null** and **undefined**, you can use a **!** to signify the same thing.
* In other words, the **!** non-null assertion asserts that the variable *cannot* be of type *null* or *undefined*.
* The following two type assertions are identical in that they both result in **Date** and *not* **Date \| undefined**.

```typescript

// Inferred type: Date | undefined
let maybeDate = Math.random() > 0.5
  ? undefined
  : new Date();

// Asserted type: Date
maybeDate as Date;

// Asserted type: Date
maybeDate!;
```
* Non-null assertions are particularly useful with APIs such as **Map.get** that return a value or **undefined** if it doesn't exist.
* Here, **seasonCounts** is a general **Map<string, number>**.
* We know that it contains an `"I Love Lucy"` key so the **knownValue** variable can use a **!** to remove `| undefined` from its type:

```typescript
const seasonCounts = new Map([
  ["I Love Lucy", 6],
  ["The Golden Girls", 7],
]);

// Type: string | undefined
const maybeValue = seasonCounts.get("I Love Lucy");


// Error: Object is possibly 'undefined'
// Type: string
console.log( maybeValue.toUpperCase() );
             ^^^^^^^^^^

const knownValue = seasonCounts.get("I Love Lucy")!;

console.log( knownValue.toUpperCase() ); // ok
```

***

### 9.4.4 Type Assertion Caveats p. 176
* Type assertions, like the *any* type, are a necessary escape hatch for TS's type system.
* Therefore, also like the *any* type, they should be avoided whenever reasonably possible.
* It is often better to have more accurate types representing your code than it is to make it easier to assert on a value's type.
* Those assertions are often wrong--either already so at the time of writing, or they become wrong later on as the codebase changes.
* For example, suppose the **seasonCounts** example were to change over time to have different values in the map.
* Its non-null assertion might still make the code pass TypeScript type checking, but there might be a runtime error:

```typescript
const seasonCounts = new Map([
  ["Broad City", 5],
  ["Community", 6],
]);

// Type: string
const knownValue = seasonCounts.get("I Love Lucy")!;

// No compile-time type error, but...
// Runtime TypeError: Cannot read property 'toUpperCase' of undefined
console.log( knownValue.toUpperCase() ); 
```
* Type assertions should generally be used sparingly, an donly when you're absolutely certain it is safe to do so.

#### 9.4.4.1 Assertions versus declarations p. 176
* There is a difference between using a **type annotation** to declare a variable's type *versus* using a **type assertion** to change the type of a variable with an initial value. end of p. 176
* TS's type checker performs assignability checking on a variable's initial value against the variable's type annotation when both exist.
* **A type assertion *explicitly* tells TS to skip some of its type checking**!
* The following code creates two objects of type **Entertainer** with the same flaw: a missing *acts* member.
* TypeScript is able to catch the error in the **declared** variable because of its `: Entertainer` type annotation.
* It is not able to catch the error on the **asserted** variable because of the type assertion:

```typescript
interface Entertainer {
  acts: string[];
  name: string;
}

// Error: Property 'acts' is missing in type
// '{ one: number; }' but required in type
// 'Entertainer'
const declare: Entertainer = {
  name: "Moms Mabley",
};

const asserted = {
  name: "Moms Mabley",
} as Entertainer; // ok, but...

// Both of these statements would fail at runtime with:
// Runtime TypeError: Cannot read properties of undefined
// (reading 'toPrecision')
console.log( declared.acts.join(", ") );
console.log( asserted.acts.join(", ") );
```
* It is therefore strongly preferable to either use a type annotation or allow TS to infer a variable's type from its initial value.

***

#### 9.4.4.2 Assertion assignability p. 176
* Type assertions are meant to be only a small escape hatch, for situations where some value's type is slightly incorrect.
* TS will only allow type assertions between two types if one of the types is assignable to the other.
* If the type assertion is between two completely unrelated types, then TS will notice and report a type error.

* Example p. 177-178

```typescript
// Error: Conversion of type 'string' to type 
// 'number' may be a mistake because neither 
// type sufficiently overlaps with the other. 
// If this was intentional, convert the 
// expression to 'unknown' first.
let myValue = "Stella!" as number;
```
* If one absolutely must switch a value from one type to a totally unrelated type, you can use a double type assertion.
* First cast the value to a top type--**any** or **unknown**--and then cast that result to the unrelated type:

```typescript
let myValueDouble = "1337" as unknown as number; //Ok but... ummmm
```
* `as unknown as...` double type assertions are dangerous and almost always a sign of something incorrect in the types of the surrounding code.
* Using them as an escape hatch from the type system means the type system may not be able to save you when changes to surrounding code would cause an issue with previously working code.

***
## 9.5 Const Assertions p. 178
### 9.5.1 Introduction
* Back in Chapter 4, we introduced the **as const** syntax for changing a mutable array type into a read-only tuple type.
* Now let's use something similar!
* **Const assertions** can generally be used to indicate that any value (e.g., array, primitive, value, etc.) should be treated as a constant, immutable version of itself.
* Here are the 3 rules that **as const** applies to any type it's applied to:
	1. Arrays are treated ad **readonly tuples**, *not* mutable arrays.
	1. Literals are treated as literals, *not* as their general primitive equivalents.
	1. Properties on objects are considered **readonly**.
* We've already seen arrays become tuples (see example on p. 179) in Chapter 4. Let's see rules 2 and 3 now.

***
### 9.5.2 Literals to Primitives p. 179
* It can be useful for the type system to understand a literal value to be that specific value, rather than *widening* it to its general primtive.
* **Example 1**, p. 179. It might be useful for a fuction to be known to produce a specific literal instead of a general primtive.
	* These functions also return values that can be made more specific.
	* Here, **getNameConst()**'s return type is the more specific "Maria Bamford" rather than the more general **string**.

```typescript

// Type: () => string
const getName = () => "Maria Bamford";

// Type: () => "Maria Bamford"
const getNameConst = () => "Maria Bamford" as const;
```
* It may also be useful to have specific fields on a value be more specific literals.
* Many popular libraries ask that a discriminant field on a value be a specific literal so the types of their code can more specifically make inferences on the value.
* **Example 2**, p. 179-180, the **narrowJoke** variable has a *style* of type **"one-liner"** instead of **string**. so it can be provided in a location that needs a type **Joke**.

```typescript
interface Joke {
  quote: string;
  style: "story" | "one-liner";
}

function tellJoke( joke: Joke ) {
  if( joke.style === "one-liner" ) {
    console.log( joke.quote );
  } else {
    console.log( joke.quote.split("\n") );
  }
}

// Type: { quote: string; style: "one-liner" }
const narrowJoke = {
  quote: "If you stay alive for no other reason do it for spite." ,
  style: "one-liner" as const,
};

tellJoke( narrowJoke ); // ok

// Type: { quote: string; style: string }
const wideObject = {
  quote: "Time flies when you are anxious!" ,
  style: "one-liner",
};

// Error: Argument of type '{ quote: string; style: string; }'
// is not assignable to parameter of type 'LogAction'.
// Types of property 'style' are incompatible.
// Type 'string' is not assignable to 
// type '"story" | "one-liner"'.
tellJoke( wideObject );
```
***
### 9.5.3 Read-Only Objects p. 180
#### 9.5.3.1 Intro
* Object literals such as those used as the initial value of a variable generally widen the types of properties the sam way the initial values of **let** variables widen.
* String values such as **'apple'** become primitives such as **string**, arrays are typed as tuples, etc.
* This can be inconvenient when some or all of those values are meant to later be used in a place that requires their specific literal type.
* Asserting a value literal with **as const**, however, switches the inferred type to be specific as possible.
* All member properties become **readonly**, literals are considered their own literal type instead of their general primitive type, arrays become read-only tuples, etc.
* In other words, applying a const assertion to a value literal makes that value literal *immutable* and recursively applies the same const assertion logic to all its members.

#### 9.5.3.2 Example p. 181
* As an example, the **preferencesMutable** value that follows is declared *without* an **as const**.
* So its names are the primitive type **string** and it's allowed to be modified.
* In contrast, **favoritesConst** is declared with an **as const** so its member values are literals and are not allowed to be modified.

```typescript
function describePreference( preference: "maybe" | "no" | "yes" ) {
  switch(preference) {
    case "maybe":
      return "I suppose...";
    case "no":
      return "No thanks.";
    case "yes":
      return "Yes please!";
  }
}

// Type: { movie: string, standup: string )
const preferencesMutable = {
  movie: "maybe",
  standup: "yes",
};

// Error: Argument of type 'string' is not assignable 
// to parameter of type '"maybe" | "no" | "yes"'.
describePreference( preferencesMutable.movie);
                    ^^^^^^^^^^^^^^^^^^^^^^^^

preferencesMutable.movie= "no"; // ok

// Type: readonly { readonly movie: "maybe", readonly standup: "yes" }
const preferencesReadonly = {
  movie: "maybe",
  standup: "yes",
} as const;

describePreference( preferencesReadonly.movie ); // ok

// Error: Cannot assign to 'movie' because it is a read-only property.
preferencesReadonly.movie = "no";
                    ^^^^^
```
## 9.6 Summary of Chapter 9

***

# Chapter 10: Generics p. 183
## 8/28/2024
## 10.1 Introduction p. 183 - 184
* All the type syntaxes we've learned so far are meant to be used with types that are completely known when they're being written.
* Someties, however, a piece of code may be intended to work with various different types depending on how it's called.

### 10.1.1 Examples p. 183
* Consider the below **identity()** function in JS meant to receive an input of any possible type and return that same inpute as output.
* How would you describe its parameter type and return type?

```typescript
function identity( input ) {
  return input;
}

identity( "abc" );
identity( 123 );
identity( {quote: "I think your self emerges more clearly over time."} );
```
* We could declare **input** as type **any**. But then the return type of the function would *also* be **any**.

```typescript
function identity( input: any ) {
  return input;
}

let value = identity(42); // Type of value: any
```
* Given that **input** is allowed to be any input, we need a way to say that there is a relationship btween the **input** type and the type the function returns.
* TS captures this kind of relationship between types using **generics**.
* In TS, constructs such as functions may declare any number of generic **type parameters**: types that are determined for each usage of the generic construct.
* These *type parameters* are used as types in the construct to represent some type that can be different in each instance of the construct.
* Type parameters may be provided with different types, referred to as **type arguments**, for each instance of the construct but will remain consistent within that instance.
* Type Parameters typically have single-letter names like **T** and **U** or PascalCase names like **Key** and **Value**.
* In all of the constructs covered in this chapter, generics may be declared using angle brackets like `<` and `>`, like so: `someFunction<T>` and `SomeInterface<T>`.
***

## 10.2 Generic Functions p. 184
### 10.2.1 Intro
* A function may be made generic by placing an alias for a type parameter, wrapped in angle brackets `<>`, immediately before the parameters parentheses.
* That type parameter will then be available for usage in parameter type annotations, return type annotations, and type annotations inside the function's body.

#### 10.2.1 Examples p. 184 - 185
* The following version of **identity()** declares a type parameter **T** for its **input** parameter, which allows TS to infer that the return type of the function is **T**.
* TS can then infer a different type for **T** every time **identity()** is called.

```typescript
function identity<T>( input: T ) {
  return input;
}

const numeric = identity( "me" ); // Type: me
const stringy = identity( 123 ); // Type: 123
```
* **Arrow functions** can also be generic. 
* Their generic declarations are also placed immediately before the **(** before their list of parameters.
* The following arrow function is functionally the same as the previous declaration:

```typescript
const identity = <T>( input: T ) => input;
identity(123); // Type: 123
```
* Warning about syntax clashes in *.tsx and JSX files p. 185

***

### 10.2.2 Explicit Generic Call Types
* Most of the time when calling generic functions, TS will be able to infer type arguments based on how the functgion is being called.
* e.g., in the **identity()** functions in the most recent examples above, TS's type checker use an argument provided to **identity()** to infer the corresponding function parameter's type argument.
* Unfortunately, as with class members and variable types, sometimes there isn't enough information from a function's call to inform TS what its type argument should resolve to.
* This will commonly happen if a generic construct is provided another generic construct whose type arguments aren't known.
* TS will default to assuming the **unknown** type for any type argument it cannot infer.
* For example, the following **logWrapper** function takes in a callback with a parameter type set to **logWrapper's** type parameter **Input**.
* TS can infer the type argument if **logWrapper** is called with a callback that explicitly declares its parameter type.
* If the parameter type is implicit, however, TS has no way of knowing what **Input** should be:

```typescript
function logWrapper<Input> ( callback: (input: Input) => void ) {
  return (input: Input) => {
    console.log("Input: ", input);
    callback(input);
  };
}

// Type: (input: string) => void
logWrapper( (input: string) => {
  console.log(input.length);
});

// Type: (input: unknown) => void
logWrapper( (input) => {

  // Error: Property 'length' does not exist on type 'unknown'
  console.log( input.length );
});
```
* To avoid defaulting to **unknown**, functions may be called with an explicit generic type argument that explicitly tells TS what that type argument should be instead.
* TS will perform type checking on the generic call to make sure the parameter being requested matches up to what's provided as a type argument.
* In the next example p. 186, the **logWrapper()** seen previously is provided with an explicit **string** for its **Input** generic.
* TS can then infer that the callback's **input** parameter of generic type **Input** resolves to type **string**:

```typescript
logWrapper<string> ( (input) => {
  console.log( input.length );
});

logWrapper<string> ( (input: boolean) => {

  // Argument of type '(input: boolean) => void' is not
  // assignable to parameter of type '(input: string) => void'. 
  // Typesofparameters'input'and'input'areincompatible.
  // Type 'string' is not assignable to type 'boolean'.

});
```
* Much like explicit type annotations on variables, explicit type arguments may always be specified on a generic function but often aren't necessary.
* In fact, many TS developers generally only specify them when needed.
* Example p. 187. The following **logWrapper()** usage explicitly specifies **string** both as a type argument and as a function parameter type. *Either* can be omitted.

```typescript

// Type: (input: string) => void
logWrapper<string>( (input: string) => { /* ... */ } );
```

* The **Name\<Type\>** syntax for specifying a type argument will be the same for other generic constructs throughout this chapter.

***

### 10.2.3 Multiple Function Type Parameters p. 187
* Functions may define any number of type parameters, separated by commas.
* Each call of the generic function may resolve its own set of values for each of the type parameters.
* **Example 1** p. 187-188, **makeTuple()** declares two type parameters and returns a value typed as a read-only tuple with one, then the other:

```typescript
function makeTuple<First, Second> ( first: First, second: Second ) {
  return [first, second] as const;
}

let tuple = makeTuple( true, "abc" ); // Type of value; readonly [boolean, string]
```
#### 10.2.3.1 Different types for different parameters all input to the same function p. 187-188
* Note that if a function declares multipe type parameters, calls to that function must explicitly declare either *none* of the generic types or *all* of the generic types.
* TS does not yet support inferring only *some* of the types of a generic call.
* **Example 2** p. 188, the **makePair()** also accepts two type parameters. So either *neither* of the parameters are explicitly specified or *both* of them are explicitly specified

```typescript
function makePair<Key, Value>( key: Key, value: Value ) {
  return { key, value };
}

// OK bc neither type argument is provided
// Type: { key: string; value: number }
makePair( "abc", 123 );


// OK bc both type arguments are provided
makePair<string, number>( "abc", 123 ); // Type: { key: string; value: number }
makePair<"abc", 123>( "abc", 123 ); // Type: { key: "abc"; value:   123 }

// Error: Expected 2 type arguments, only received one
// TS currently only supports *all* parameters with types specified..
// ...or *none* specified. Can't just have *some* specified.
makePair<string>( "abc", 123 );
```
***

## 10.3 Generic Interfaces p. 188
### 10.3.1 Intro to Generic Interfaces
* Interfaces may be declared as generic as well.
* Similar rules as generic functions. Generic functions may have any number of type parameters declared between angle brackets `<` and `>` after the name of the interface.
* That generic type may later be used elsewhere in their declaration, such as on member types.

### 10.3.2 Examples p. 188-189
* The following **Box** declaration has a **T** type parameter for a property.
* Creating an objct declared to be a **Box** with a type argument enforces that the **inside: T** property matches that type argument

```typescript
interface Box<T> {
  inside: T;
}

let stringyBox: Box<string> = {
  inside: "abc",
};

let numberBox: Box<number> = {
  inside: 123,
}

let incorrectBox: Box<number> = {

  //Error: type 'boolean' is not assignable to type 'number'
  inside: false,

}
```
* Fun fact: the built-in **Array** methods are defined in TS as a generic interface!
* **Array** uses a type parameter **T** to represent the data storedwithin an array.
* Therefore, its **pop()** and **push()** methods look roughly like this:

```typescript
interface Array<T> {
  // ...

  /*
   * Remooves the last element from an array and returns it
   * If the array is empty, *undefined* is returned and the array
   * is not modified.
   */
   pop(): T | undefined;

  /*
   * Appends new elements to the end of an array,
   * and returns the new length of the array
   * @param items new elements to add to the array.
   */
   push( ...items: T[] ): number;

   // ...
}
```
***

### 10.3.3 Inferred Generic Types p. 189
* As with generic functions, generic interface type arguments may be inferred from usage. 
* TS will do its best to infer type arguments from the type of values provided to a location declared as taking in a generic type.

#### 10.3.3.1 Examples p. 189 - 191
* This **getLast()** function declares a type parameter **Value** that is then used for its **node** parameter.
* TS can then infer **Value** based on the type of whatever value is passed in as an argument.
* It can even report a type error when an inferred type argument does not match the type of a value.
* Providing **getLast()** with an object that doesn't include **next**--*or* whose inferred **Value** type argument is the same type--is allowed.
* Mismatching the provided object's **value** and **next.value**, though is a type error: p. 190

```typescript
interface LinkedNode<Value> {
  next?: LinkedNode<Value>;
  value: Value;
}

function getLzst<Value> ( node: LinkedNode<Value> ): Value {
  return node.next ? getLast( node.next ) : node.value;
}


// Inferred Value type argument: Date
let lastDate = getLast( {
  value:new Date( "09-13-1993" ),
} );

// Inferred Value type argument: string
let lastFruit = getLast( {
  next: {
    value: "banana",
  },
  value: "apple",
} );

// Inferred Value type argument: number
let lastMismatch = getLst( {
  next: {
    value: 123
  },

  // Error: type 'boolean' is not assignable to type 'number'
  value: false
  ^^^^^
} );
```

* Note that if an interface declares type parameters, any *type annotations* referring to that interface must provie corresponding type arguments.
* **Example 3** p. 190-191, the usage of **CrateLike** is *incorrect* for not including a type argument:

```typescript
interface CrateLike<T> {
  contents: T;
}

let missingGeneric: Cratelike = {
                    ^^^^^^^^^
  // Error: Generic type 'Crate<T>' requires 1 type argument inside : ??
  inside: "??"
};
```

* Later in this chapter, I'll show how to provide default values for type parameters to get around this requirement.

***

## 10.4 Generic Classes p. 191
* Classes, like interfaces, can also declare several type parameters that will apply to members.
* Each instance of the class may have a **different set of type arguments** for its type parameters.

### 10.4.1 Example p. 191
* This **Secret** class declares **Key** and **Value** type parameters, then uses them for member properties, constructor parameter types, and a method's parameter and return types:

```typescript
class Secret<Key, Value> {
  key: Key;
  value: Value;

  constructor( key: Key, value: Value ) {
    this.key = key;
    this.value = value;
  }

  getValue( key: Key ): Value | undefined {
    return this.key === key
      ? this.value
      : undefined;
  }
}

const storage = new Secret( 1234, "luggage" ); // Type: Secret<number, string>

storage.getValue(1987); // Type: string | undefined
``` 
* As with Generic interfaces, **type annotations** using a class must indicate to TS what any generic types on that class are.

***

### 10.4.2 Explicit Generic Class Types p. 192
* Instantiating generic classes goes by the same type arguments inference rules as calling generic functions.
* If the type argument can be inferred from the type of a parameter to the class constructor, such as the **new Secret( 12345, "luggage" )** earlier, TS will used the inferred type.
* Otherwise, if a class type argument can't be inferred from the arguments passed to its constructor, the type argument will default to **unknown**.

#### 10.4.2.1 Examples p. 192-193
* **Example 1** p. 192 below **CurriedCallback** class declares a constructor that takes in a generic function.
* If the generic function has a known type--such as from an explicit type argument type annotation--then the class instance's **Input** type argument can be informed by it.
* Otherwise, the class instance's **Input** type argument will default to **unknown**.

```typescript
class CurriedCallback<Input> {
  #callback: ( input: Input ) => void;

  constructor( callback: (input: Input) => void ) {
    this.#callback = ( input: Input ) => {
      console.log( "Input: ", input);
      callback( input );
    };
  }

  call( input: Input ) {
    this.#callback( input );
  }
}

// Type: CurriedCallback<string>
new CurriedCallback( (input: string) => {
  console.log( input.length );
});

// Type: CurriedCallback<unknown>
new CurriedCallback( (input) => {
  // Error: Property 'length' does not exist on type 'unknown'
  console.log( input.length );
                     ^^^^^^
});
```
* Class instances may also avoid defaulting to **unknown** by providing explicit type argument(s) the same way other generic function calls do.
* **Example 2** p. 193, **CurriedCallback** from before is now being provided with an explicit **string** for its **Input** type argument, so TS can infer that the callback's **Input** type parameter resolves to **string**:

```typescript

// Type: CurriedCallback<string>
new CurriedCallback<string>( (input) => {
  console.log( input.length );
});

// Argument of type '(input: boolean) => void' is not
// assignable to parameter of type '(input: string) => void'. 
// Types of parameters 'input' and 'input' are incompatible. 
// Type 'string' is not assignable to type 'boolean'.
new CurriedCallback<string>( (input: boolean) => {
  ...
}
```
***

### 10.4.3 Extending Generic Classes p. 193
#### 10.4.3.1 Intro
* Generic classes can be used as the base class following an **extends** keyword.
* TS will not attempt to infer arguments for the base class from usage.
* Any type arguments *without* defaults will need to be specified using an explicit type annotation.

#### 10.4.3.1 Examples
* **Example 1** p. 193-194, the following **SpokenQuote** class provides **string** as the **T** type argument for its base class **Quote<T>**:

```typescript
class Quote<T> {
  lines: T;

  constructor( lines: T ) {
    this.lines = lines;
  }
}

class SpokenQuote extends Quote<string[]> {
  speak() {
    console.log( this.lines.join("\n") );
  }
}

// Type: string
new Quote( "The only real failure is the failure to try." ).lines; 

// Type: number[]
new Quote( [4,8,15,16,23,42] ).lines; 

// Type: string[]
new SpokenQuote([
  "Greed is so destructive.",
  "It destroys everything",
]).lines; 

// Error: Argument of type 'number' is not 
// assignable to parameter of type 'string'.
new SpokenQuote( [4,8,15,16,23,42] );
                 ^^^^^^^^^^^^^^^^^
```
* Generic derived classes can alternately pass their own type argument through to their base class.
* The type names don't have to match. Just for fun, see **Example 2**, p. 194 below

```typescript
class AttributedQuote<Value> extends Quote<Value> {
  speaker: string

  constructor( value: Value, speaker: string ) {
    super(value);
    this.speaker = speaker;
  }
}

// Type: AttributedQuote<string>
// (extending Quote<string>)
new AttributedQuote( 
  "The road to success is always under construction.",
  "Lily Tomlin",
);
```
***

### 10.4.4 Implementing Generic Interfaces p. 194
#### 10.4.4.1 Intro
* Generic classes may also implement generic interfaces by providing them any necessary type parameters.
* This works similarly to extending a generic base class: any type parameters on the base interface must be declared by the class.

#### 10.4.4.2 Example
* Here, the **MoviePart** class specifies the **ActingCredit** interace's **Role** type argument as a **string**.

```typescript
interface ActingCredit<Role> {
  role: Role;
}

class MoviePart implements ActingCredit<string> {
  role: string;
  speaking: boolean;

  constructor( role: string, speaking: boolean ) {
    this.role = role;
    this.speaking = speaking;
  }
}

const part = new MoviePart( "Miranda Priestly", true );

part.role; // Type: string

// Error: Property 'role' in type 'IncorrectExtension' is not
// assignable to the same property in base type 'ActingCredit<string>'. 
// Type'boolean'is not assignable to type 'string'.
class IncorrectExtension implements ActingCredit<string> {
  role: boolean;
        ^^^^^^^
}
```

***

### 10.4.5 Method Generics p. 196
* Class methods may declare their own generic types separate from their class instance.
* Each call to a generic class method may have a different type argument for each of its type parameters.
* In **Example** below p. 197, the generic **CreatePairFactory** class declares a **Key** type and includes a **createPair()** method that also declares a separate **Value** generic type.
* The return type for **createPair()** is then inferred to be **{ key: Key, value: Value }**.

```typescript
class CreatePairFactory<Key> {
  key: Key;

  constructor( key: Key ) {
    this.key = key;
  }

  createPair<Value>( value: Value ) {
    return { key: this.key, value };
  }
}

 // Type: CreatePairFactory<string>
const factory = new CreatePairFactory("role"); 

// Type: { key: string, value: number }
const numberPair = factory.createPair(10); 

// Type: { key: string, value: string }
const stringPair = factory.createPair("Sophie");
```

***

### 10.4.6 Static Class Generics p. 197
* Static members of a class are separate from instance members and aren't associated with any particular instance of the class.
* They dont' have access to any class instances or type information specific to any class instance.
* As a result, while static class methods can declare their own type parameters, they cannot access any type parameters declared on a class.
* **Example** p. 196-197, a **BothLogger** class declares an **OnInstance** type parameter for its **instanceLog()** method and a separate **OnStatic** type parameter for its static **staticLog()** method.
* The static method is not able to access the instance **OnInstance** b/c **OnInstance** is declared for class instances.

```typescript
class BothLogger<OnInstance> {
  instanceLog( value: OnInstance ) {
    console.log(value);
    return value;
  }

  static staticLog<OnStatic>( value: OnStatic ) {

    // Error: Static members cannot reference class type arguments
    let fromInstance: OnInstance;
                      ^^^^^^^^^^
    console.log(value);
    return value;
  }
}

const logger = new BothLogger<number[]>;

// Type: number[] 
logger.instanceLog([1, 2, 3]); 

// Inferred OnStatic type argument: boolean[]
BothLogger.staticLog([false, true]);

// Explicit OnStatic type argument: string
BothLogger.staticLog<string>("You can't change the music of your soul.");
```

***

## 10.5 Generic Type Aliases p. 197
### 10.5.1 Intro
* One last construct in TS that can be made generic is **type aliases**.
* Each type alias may be given any number of type parameters, such as this **Nullish** type receiving a **T**:

```typescript
type Nullish<T> = T | null | undefined;
```

* Generic type aliases are commonly used with functions to describe the type of a generic function.

```typescript
type CreatesValue<Input, Output> = (input: Input) => Output; 

// Type: (input: string) => number
let creator: CreatesValue<string, number>; 

creator = text => text.length; // Ok

// Error: Type 'string' is not assignable to type 'number'.
creator = text => text.toUpperCase();
                  ^^^^^^^^^^^^^^^^^^
```

### 10.5.2 Generic Discriminated Unions p. 198
* I mentioned back in Chapter 4 that discriminated unions are my favorite feature in all of TS.
* Discriminated unions beautifully combine a common elegant JS pattern with TS's type narrowing.
* My favorite use of discriminated unions is to add a type argument to create a generic "result" type that represents eitehr a successful result (with data) or a failure (with an error).
 
#### 10.5.2.1 Example p. 198
* This **Result** generic type features a **succeeded** discriminant that must be used to narrow a result to whether its a success or failure.
* This means any operation that returns a **Result** can indicate an error or data result, and be assured that any consumers will need to check whether the result succeed.

```typescript

type Result<Data> = FailureResult | SuccessfulResult<Data>;

interface FailureResult {
  error: Error;
  succeeded: false;
}

interface SuccessfulResult<Data> {
  data: Data;
  succeeded: true;
}

function handleResult( result: Result<string> ) {
  if (result.succeeded) {

    // Type of result: SuccessfulResult<string>
    console.log( `We did it! ${result.data}` );

  } else {

    // Type of result: FailureResult
    console.error(`Awww... ${result.error}`);
  }

  // Error: Property 'data' does not exist on type 'Result<string>'. 
  // Property 'data' does not exist on type 'FailureResult'.
  result.data;
         ^^^^
}
```
* Put together, generic types and discriminated types provide a wonderful way to model reusable types like **Result**.

***

## 10.6 Generic Modifiers
* TS includes syntax that allows you to modify the behavior of generic type parameters.

### 10.6.1 Generic Defaults
#### 10.6.1.1 Intro
* I've stated so far that if a generic type is used in a type annotation or as the base of a class that *extends* or *implements*, it must provide a type argument for *each* type parameter.
* One can avoid explicitly providing type arguments by placing an `=` equals sign followed by a default type after the type parameter's declaration.
* The default will be used in any subsequent type where the type argument isn't explicitly declared and can't be inferred.

#### 10.6.1.2 Examples 1, 2, 3 p. 199-200
* **Example 1** p. 199, here the **Quote** interface takes in a **T** type parameter that defaults to **string** if not provided.
* The **explicit** variable explicitly sets **T** to a **number** while **implicit** and **mismatch** both resolve to **string**.

```typescript
interface Quote<T = string> {
  value: T;
}

let explicit: Quote<number> = { value: 123 };

let implicit: Quote = { value: "Be yourself. The world worships the original."
};

// Error: Type 'number' is not assignable to type 'string'.
let mismatch: Quote = { value: 123 };
                               ^^^
```
* Type parameters can default to earlier type parameters in the same declaration too. Since each type parameter introduces a new type for the declaration, they are available for defaults for later parameters in that declaration.

* **Example 2** p. 200, the **KeyValuePair** type can have different types for its **Key** and **Value** generics but defaults to keeping them the same--though because **Key** doesn't have a default, it does still need to be inferrable or provided:

```typescript
interface KeyValuePair<Key, Value = Key> {
  key: Key;
  value: Value;
}

// Type: KeyValuePair<string, string>
let allExplicit: KeyValuePair<string, number> = {
  key: "rating",
  value: 10,
};


// Type: KeyValuePair<string>
let oneDefaulting: KeyValuePair<string> = {
  key: "rating",
  value: "ten",
};


// Note ERROR because there was no generic <argument> with either
// one argument <string>, e.g., KeyValuePair<string> or..
// two arguments <string, number>, e.g., KeyValuePair<string, number> 
let firstMissing: KeyValuePair = {
                  ^^^^^^^^^^^
  key: "rating",
  value: 10,
};
```

* Keep in mind that all default type parameters must come last in their declaration list, similar to default function parameters.
* Generic types without a default may *not* follow generic types with a default.
* **Example 3** p. 200. Here, **inTheEnd** is allowed because all generic types without defaults come before generic types without defaults.
* **inTheMiddle** is a problem because a generic type without a default follows types with defaults

```typescript
function inTheEnd<First, Second, Third = number, Fourth = string> () {} //ok

// Error: Required type parameters may not follow optional type parameters
function inTheMiddle<First, Second = boolean, Third = number, Fourth>() { }
                                                              ^^^^^^
```
***

## 10.7 Constrained Generic Types p. 201
### 10.7.1 Intro
* Generic types by default can be given any type in the world: classes, interfaces, primitives, unions, etc.
* However, some functions are only meant to work for a limited set of types.
* TS allows for a type parameter to declare itself as needing to *extend* at type: meaning it's only allowed to alias types that are assignable to that type.
* The syntax to constrain a type parameter is to place the *extends* keyword after the type parameter's name, followed by a type to constrain it to.

### 10.7.2 Example p. 201
* For example, by creating a **WithLength** interface to describe anything that has a **length: number**, we can then allow our generic functions to take in any type that has a **length** for its **T** generic.
* Strings, arrayus, and now even objects that just os happen to have a **length: number** are allowed, while type shapes such as **Date** missing that numeric **length** result in a type error.

```typescript
interface WithLength {
  length: number;
}

function logWithLength<T extends WithLength>( input: T ) {
  console.log( `Length: ${ input.length }` );
  return input;
}

// Type: string
logWithLength( "No one can figure out your worth but you." );

// Type: boolean[]
logWithLength( [false, true] ); 

// Type: { length: number }
logWithLength( { length: 123 } );

// Error: Argument of type 'Date' is not
// assignable to parameter of type 'WithLength'.
//   Property 'length' is missing in type
//   'Date' but required in type 'WithLength'.
logWithLength( new Date() )
               ^^^^^^^^^
```

***

### 10.7.3 keyof and Constrained Type Parameters p. 202
* The **keyof** operator introduced in Chapter 9 also works well with constrained type parameters.
* Using **extends** and **keyof** together allows a type parameter to be constrained to the keys of a previous type parameter.
* It is also the **only way to specify the key of a generic type**.


#### 10.7.3.1 Examples 1+2
* **Example 1**, p. 202. Consider this simplified version of the **get()** method from the popular JS library *Lodash*.
* It takes in a container value, typed as **T**, and a **key** name of one of the keys of **T** to retrieve from **container**.
* B/c the **Key** type parameter is constrained to be a **keyof T**, TS knows this function is allowed to return **T[Key]**.

```typescript
function get<T, Key extends keyof T>( container: T, key: Key ) {
  return container[key];
}

const roles = {
  favorite: "Fargo",
  others: ["Almost Famous", "Burn After Reading", "Nomadland"], 
};

// Type: string
const favorite = get( roles, "favorite" );

// Type: string[]
const others = get( roles, "others" ); 

// Error: Argument of type '"extras"' is not assignable 
// to parameter of type '"favorite" | "others"'.
const missing = get( roles, "extra" );
                            ^^^^^^^
```
* Without **keyof**, there would have been no way to correctly type the generic **key** parameter.
* Note the importance of the **Key** type parameter in the previous example.
* If only **T** is provided as a type parameter, and the **key** parameter is allowed to be any **keyof T**, then the return type will be the union type of all property values in **Container**.
* **Example 2** p. 202-203, this less-specific function declaration doesn't indicate to TS that each call can have a specific **key** via a type argument:

```typescript
function get<T>( container: T, key: keyof T ) {
  return container[key];
}

const roles = {
  favorite: "Fargo",
  others: [ "Almost Famous", "Burn After Reading", "Nomadland" ],
};

// Type: string | string[]
const found = get( roles, "favorite" );
```

***

## 10.8 Promises p. 203
### 10.8.1 Intro
* Promises are a core fature of modern JS--and they rely on some of what generics in TS offer!
* To review, a **Promise** in JS represents something that might still be pending, such as a network request.
* Each Promise provides methods to register *callbacks* in case the pending action **resolves** (aka completes successfully) or **rejects** (throws an error).
* A Promise's ability to represent similar actions on any arbitrary value types is a natural fit for TS's generics.
* Promises are repesented in the TS type system as a **Promise class** with a single type parameter representing the the eventual resolved value.

***

### 10.8.2 Creating Promises p. 203
* The *Promise* constructor is typed in TS as taking in a *single* parameter.
* That parameter's type type relies on a type parameter declared on the generic **Promise** class.
#### 10.8.2.1 Example 1,2, and 3 p. 204
* **Example 1** p. 204 -205 A reduced form would look something like this:

```typescript
class PromiseLike<Value> {
  constructor(
    executor: (
      resolve: ( value: Value ) => void,
      reject: ( reason: unknown ) => void,
      ) => void,
  ) { /* ... */ }
}
```
* Creating a Promise intended to eventually resolve with a value generallyl necessitates explicitly declaring the type argument of the Promise.
* TS would default to assuming the parameter type is **unknown** without that explicit generic type argument.
* **Example 2** p. 205 Explicitly providing a type argument to the **Promise** constructor would allow TS to understand the resultant Promise instance's resolved type:

```typescript
// Type: Promise<unknown>
const resolvesUnknown = new Promise( (resolve) => {
  setTimeout( () => resolve( "Done!" ), 1000 );
});

// Type: Promise<string>
const resolvesString = new Promise<string>( (resolve) => {
  setTimeout( () => resolve( "Done!" ), 1000);
});

```
* A Promise's generic **.then()** method introduces a new type parameter representing the resolved value of the Promise it returns.
* **Example 3** p. 205

```typescript
// Type: Promise<string>
const textEventually = new Promise<string>( (resolve) => {
  setTimeout( () => resolve( "Done!" ), 1000);
});

// Type: Promise<number>
const lengthEventurally = textEventually.then( (text) => text.length );
```

***

### 10.8.3 Async Functions p. 204-205
* Any function declared in JS with the **async** keyword returns a **Promise**.
* If a value returned by an **async** function in JS isn't a *Thenable* (an object with a **.then()** method; in practice almost always a Promise), it will be wrapped in a **Promise** as if **Promise.resolve** was called on it.
* TS recognizes tis and will infer the return type of an **async** function to always be a **Promise** for whatever value is returned.

***
#### 10.8.3.1 Examples 1+2, p. 205
* **Example 1** p. 205, the **lengthAfterSecond()** returns a **Promise<number>** directly. 
* while **lengthImmediately()** is inferred a **Promise<number>**, because it is **async** and directly returns a number.

```typescript

// Type: (text: string) => Promise<number>
async function lengthAfterSecond( text: string ) {
  await new Promise( (resolve) => setTimeout( resolve, 1000) )
  return text.length;
}

// Type: ( text: string ) => Promise<number>
async function lengthImmediately( text: string ) {
  return text.length;
}
```
* **Example 2** p. 205--Any manually declared return type on an **async** function therefore must always be a **Promise** type...
* ...even if the function doesn't explicitly mention Promises in its implementation:

```typescript

//Ok
async function givesPromiseForString(): Promise<string> {
  return "Done!";
}

// Error: The return type of an async function 
// or method must be the global Promise<T> type.
async function givesString(): string {
                              ^^^^^^
  return "Done!";
}
```

***

## 10.9 Using Generics Right p. 205 - 209
### 10.9.1 Intro p. 206
* As in the **Promise<Value>** implementations earlier in this chapter, although generics can give us a lot of flexibility in describing types in code, they can become complex quickly.
* Programmers new to TS frequently go through a phase of **overusing generics** to the point of making code confusing to read and overly complex to work with.
* TS best practice is generally to use generics only when necessary!
* **Warning!** Most code one writes in TS should *not* heavily use generics to the point of confusion.
	* However, **types for utility libraries**, particularly general-use modules, may sometimes need to heavily use them.
	* **Understanding generics is particularly useful to be able to work with types in *utility libraries*.**

***

### 10.9.2 The Golden Rule of Generics p. 206
* One quick test that can help decide whether a type parameter is necessary for a function is it should be used at least twice.
* Generics describe relationships between types, so if a generic type parameter only appears in one place, it can't possibly defining a relationship between types.
* Each function type parameter should be used for a parameter and then also for at least one other parameter and/or the return type of the function.
* ***Effective Typescript** by Dan Vanderkam (O'Reilly, 2019)* contains several excellent tips for how to work with generics.
* In particular, check out the section titled *The Golden Rule of Generics*. 

#### 10.9.2.1 Examples 1+2, p. 206-207
* **Example 1**, this **logInput()** function uses its **Input** type parameter exactly once, to declare its **input** parameter:

```typescript
function logInput<Input extends string>( input: Input ) {
  console.log( "Hello!", input);
}
```
* Unlike the *identify()* functions earlier in Chapter 10, **logInput()** doesn't do anything with its type parameters such as returning or declaring more parameters.
* There is therefore not much use to declaring that **Input** type parameter.
* **Example 2** p. 206-207--let's rewrite *logInput()** without it:

```typescript
function logInput( input: string ) {
  console.log( "Hello!", input)
}
```

***

### 10.9.3 Generic Naming Conventions p. 207
* The standard naming convention for type parameters in many languages, TS, included, is to default to calling a first type argument **T** (i.e., *type* or *template*).
* The, any subsequent type parameters are named **U**, **V**, **W**, etc.
* If some contextual information is known about how the type argument is supposed to be used, the convention sometimes extends to using the first letter of the term for that usage, e.g., **K** = 'key', **V** = 'value', etc.

#### 10.9.3.1 Examples 1+2, p. 207
* Unfortunately, naming a type argument with just 1 letter can be confusing. For example, what the hell do **L** and **V** refer to below?

```typescript
function labelBox<L, V>( l: L, v: V ) { /*...*/ }
```

* When the intent of a generic isn'g clear from a single-letter **T**, it's best to use descriptive names for generic types to indicate what it is used for. Rewriting the above **labelBox()** function like this is much clearer:

```typescript
function labelBox<Label, Value>( label: Label, value: Value ) {...}
```

* Whenever a construct has multiple type parameters--or the purpose of a single type argument is not immediately clear--consider using fully written names for readability. Instead of single-letter abbreviations!

***

## 10.10 Summary of Chapter 10 p. 208
* In this chapter we made generics out of: classes, functions, interfaces, and type aliases by allowing them to work with type parameters.
***











***
## register info
* to paste *```javascript* from the register **j**, type `"jp`.
* to paste *`<script>`* from the register **k**, type `"kp`.
* to yank next 3 words and store in register **a**, type `"ay3w`.

`<script>`
