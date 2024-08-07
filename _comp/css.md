---
title: CSS Notes
permalink: /css/
sitemap: false
---

# Learning Web Design, 5d, Jennifer N. Robbins
## 7/28/2024
### Chapter 11: Introducing CSS p. 239
* Book arrived in mail on Friday 7/26.
* Up to p. 242

## 7/30/2024
* Three ways of attaching styles to a document
	1. Inline styles (most primitive, less modular/scalable, not recommended). e.g. `<h1 style="color : dark-grey">Chapter 1 </h1>`.
	1. Embedded style sheet where one places all styles within a `<style> ... </style>` block inside the HTML `<head>` section.
	1. External style sheet. Most scalable. Either imported via the 
		*  `<link rel="stylesheet" href="file.css">` in the `<head>` section
		* **#import** rule
* Got `st1.css` and `st2.css` working in proj3 directory. Used some sample templates from [SheCodes.io](https://palettes.shecodes.io).
* p. 242. syntax is **selector {**`declaration`**}**, where `declaration` = list of *property:value* pairs.

### Selectors p. 243
#### More detail in later chapters, but for now...
1. *Element-type* selectors include `<h1>` and `<p>` and `body`.
1. *ID* selectors select element based on **id** atributes. Indicated by `#` symbol.

***

### Conflicting Styles: The Cascade p. 249
* Priority, Specificity, Rule Order

### The Box Model p. 251

### Grouped Selectors p. 252

### Units of Measurement p. 253
* Absolute Units
	1. px - pixel, defined as 1/96 of an inch in CSS3  
	1. in - inches
	1. mm - millimeters
	1. cm - centimeters
	1. q - 0.25 mm
	1. pt - points (1/72 of an inch). Points are a unit commonly used in print design
	1. pc - picas (1 pica = 12 points aka 1/6 of an inch). Used in print design
* Relative Units
	1. em - unit of measurement equal to the capital letter **M** in the current font size
	1. ex - x-height, aka about the height of a lowercase **x** in the current font
	1. rem - aka *root em*, equal to the *em* size of the root element (html).
	1. ch - zero width, equal to the width of a **0** (zero) in the current font and size
* Relative Units - Viewport
	1. vw - viewport width, equal to 1/100 of the current viewport width
	1. vh - viewport height, equal to 1/100 of the current viewport height
	1. vmin - viewport minimum unit, equal to the value of **vw** or **vh**, whichever is smaller
	1. vmax - viewport maximum unit, equal to the value of **vw** or **vh**, whichever is larger
* More on **rem** unit p. 254
	* In modern browsers, the default root font size is **16 pixels**. 
	* Therefore, an element sized to 10rem would measure 160 pixels.
* More on **em** unit p. 254
	* In traditional publishing, the em is equal to the capital letter **M** in the current font size
	* In CSS, an *em* is calculated ad the distance between baselines when the font is set without any extra space between the lines (aka *leading*). 
	* The trick to working with *em* is to remember each em is always relevant to the current font size of the element it's in. e.g., if one sets a 2em left margin on an `<h1>`, `<h2>`, or `<p>`, those elements will not line up nicely becuse the em units are based on their respective element sizes. See Fig 11-11 on p. 255.

***

## 7/31/2024
### Viewport Percentage Length ( vw / vh ) p. 255
* Viewport Width (vw) and viewport height (vh) are relatvie to the size of the current viewport.
* 1 vw = 1/100 of the current width of the viewport
* 1 vh = 1/100 of the current height of the viewport
* Viewport based units are useful for ensuring that images and text elements stay full width or height of the viewport like so:

```css
header {
	width: 100 vw;
	height: 100 vh;
}
```

* The equivalent for ensuring that the header is always exactly 50% of the current viewport height and width is:

```css
header {
	width: 50 vw;
	height: 50 vh;
}
```

# Chapter 12: Formatting Text p. 261
* Use the `Black Goose Bistro` sample webpage from Chapter 5.
* Current work stored in `proj-3/_ch12/`

### A Word about Properties p. 262
#### This table explains how the book's formatting conveys information about how to understand CSS properties as laid out in this volume.
1. Values
1. Default
1. Applies to
1. Inherits
1. In addition, here are some CSS-wide keywords. All CSS properties accept the three CSS-wide keywords.
	1. initial - explicitly sets the property to it's default/initial value
	1. inherit - explicitly force an element to inherit a style property from its parent
	1. unset - erases declared values occurrin earlier in the cascade

### Font Names p. 263

### All about Web Fonts p. 264 - 265

### Generic Font Families p. 266
* How to stack font families p. 267

### Specifying Font Size p. 269
* Sizing text with relative values, aka *rem* values vs *em* measurements p. 270 - 272

### Bold, Italic, Small-Caps, etc.
* Bold = Font Weight p. 273
* Italic = Font Style p. 274
* Small Caps = Font Variant in CSS 2.1  p. 275
* Shortcut to consolidate fonts into the shorthand **font** property p. 276

## 8/06/2024
### Advanced Typography with CSS p. 277

### More selectors p. 281
* In the previous chapter, we saw how to group selectors together in a comma-separated list so we can apply properties to several elements at once.
* Here are examples of the selectors we've already covered:
	* Element selector `p { color: navy }`
	* Grouped selectors `p, ul, td, th { color: navy }`
* Of course, that's hard-coded and hard to maintain. So for more maintanable CSS, let's learn about 3 options: (1) descendant selectors, (2) ID selectors, (3) class selectors

#### Descendant Selectors p. 281
* A **descendent selector** targets elements that are contained within another element.
	* This is an example of a contextual selector.
	* See text box on p. 283 for other examples of contextual selectors: child selector, next-sibling selector, subsequent-sibling selectors
* For example, `li em { color: olive }` will apply an *olive* color only to the **emphasized (em)** lines (li) in the diagram on p. 282.
* Another example: `h1 em, h2 em, h3 em { color: red }` *only* targets emphasized elements that appear in h1, h2, or h3 headings.

#### ID Selectors p. 282
* Remember, the *id attribute* gives an element a unique name to identify that element.
* *id* is commonly used to give names andmeaning to **div** and **span** elements.
* When referring to a previously defined *id*, one uses the `#` hashtag/pound symbol. e.g., 

```html

<li id="cat1"> First Cat </li>
<!-- Below line references the desired id selector in CSS -->
```

```css
li#cat1 { color: olive }
```

* Because *id* values must be unique in each HTML document, one can omit the element name like so:

```css
#cat1 { color: red }
```

* One can use an `ID selector` as part of a *contextual selector*. in the below example, a style is applied only to `a` elements that appear within the element identified as *resources*.
* In this way, one can treat links in the element named 'resources' *differently* than all the other links on the page without any additional markup:

```css
#resources a { text-decoration: BOLD }
```

#### Class Selectors p. 284
* One last selector type: class selectors.
* Unlike *id elements* that must be uniquely named in a document, **class elements** can share the same name.
* Also, an element can belong to multiple classes at the same time.
* *Class elements* are indicated by a `.` prior to the name, just as *id element* are indicated by a `#`.
* e.g., to select *all* paragraphs (indicated by `<p>` in html) that have the class name `class="superman"` 

```css
p.superman { color: blue }
```

* To apply a property to *every* element of the same class, one omits the element name in the selector but **leave the period in**. Example:

```css
.superman { color: red }
```

### Specificity 101 p. 284
* Priority and specificity of when multiple selectors seem to conflict.


## 8/07

***

## register info
* to paste *```javascript* from the register **j**, type `"jp`.
* to paste *`<script>`* from the register **k**, type `"kp`.
* to yank next 3 words and store in register **a**, type `"ay3w`.

`<script>`
