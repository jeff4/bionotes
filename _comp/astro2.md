---
title: Astro 2
permalink: /astro2/
sitemap: false
---
***

## 3/12/2025
* OK, minor updates to sw and docs in AstroPaper, latest version is [**5.0.1**](https://github.com/satnaing/astro-paper/releases/tag/v5.0.1). Previous link goes to [5.0.1 release page](https://github.com/satnaing/astro-paper/releases/tag/v5.0.1).
* After deleting previous version of `/a1-arm`, everything works as advertised, including running version 5.0.1. When one runs `pnpm run dev`, console says: **`@5.0.1 dev ~/demo_files/a1-arm`**
* The directory structure has changed as of AP5. Now, blog posts are located within `HOME/src/data/blog/`. Experimental deletion of blog posts works fine

***

## 3/14/2025
* Content updates -- all completed by 3/15
	* About Page
	* Footer Social links
	* Primary welcome screen where Mingalaba is said
	* Turn off RSS
	* H1 Name on top left
	* added `alias pp = 'pnpm run dev'`
	* updated text of About page

***

## 3/15/2025
* Completed today
	* Tested blog-generator.js file to create a new post
	* Added `alias cd1m = `
	* Added `alias cd1p = `
	* Added `alias cd1sr = `
	* Added `alias cd1l = `
* Items to change in `root/src/config.ts`
	* Change value of **SITE.title** to change name of site in top left corner.
	* Tons of variables like default AUTHOR, WEBSITE (for deployed domain name), DESC (for seo description that shows up in Google SERP), title, ogImage, etc.
* Fixed jeff hwang social links at bottom, including asking claude to generate a new IG.svg icon b/c AP5 uses hardcoded SVG files rather than the generated ones in AP4
* Edited text for About page
* Edited old `blog-template-generator.js` because it was using outdated CommonJS module system from AP4. For AstroPaper5, we use the ES6 module system (from ECMAScript 2015). Asked Claude to rebuild `blog-template-generator.js` using ES6 module system and it works.

### Changes to 'PostDetails.astro' layout file
* Located in `root/src/layouts/PostDetails.astro`.
* Removed the *Edit Post* functionality that appears at the top of every post by commenting out `<EditPost class../>`
* Removed the *Share Links* functionality that appears at the bottom of every post by commenting out `<ShareLinks />` div section.

***


## 3/16/2025
* <del> Figure out what's wrong with the spacing of the newer post / older post functionality at the bottom of the `PostDetail.astro` layout file. </del> (This was fixed on 3/17.) 
* <del>For some reason, `Suggest changes` widget shows up on mobile viewport but not desktop viewport. Need to examine CSS to figure out why that is happening.</del> (This was fixed on 3/17.) 
* Fix size of new IG logo/icon at bottom. See next notes.
* Figure how to fix Favicon in browser window. Something simple like a J in a box

***

### After sleeping on it, decided to ask Claude about:
* Do i need to regenerate my old blog posts or do they conform well to AP5? Steps:
	* upload relevant templates, layouts, components
	* show the new hamlet that was freshly generated
	* compare with existing markdown from Sat Naing
	* compare with old posts like old Stepfunction blog posts
* IG and LinkedIn logos are different sizes. upload to claude:
	* screenshot of footer
	* `/src/components/Socials.astro`
	* Sample SVGs from Icon library under `/src/assets/icons/`
* Edits to `PostDetails.astro`. Changed copy from "Next Post / Previous Post" to JH preferred "Newer Post / Older Post" On lines **142** and **165**. Changes the text that appears at the bottom of the page.


***

## 3/17/2025
* Used [this Claude thread](https://claude.ai/share/a2e4e03d-fcfa-4125-8e58-828e51c16c4c) to fix the left margin of the "Newer/Older" post links to be flush left in both desktop and mobile versions. Modified `root/src/layouts/PostDetails.astro` file to do this. We can examine old v1 through v5 versions of this `PostDetails.astro` file stored in Dropbox within the `_comp/` file.
* Per [this Claude thread](https://claude.ai/share/123c4a89-dc64-4f6c-8030-3ed7a5746584), I commented out the `import EditPost` as well as the 2 references to it so that the "Suggest Edit" widget does not show up in either desktop or mobile viewports.
* Move  `jeffhwang.me` custom domain from `a7` to `a1`. Completed. See [these Claude instructions](https://claude.ai/share/d77e3d64-84ee-446f-9a4c-e9af62e9ec4b). Very quick and easy and showed up on CDN within seconds. Note: need to remove custom domain from old app before applying it to the new app.


***

## 3/20/2025
* Need to change default color to dark mode somehow
