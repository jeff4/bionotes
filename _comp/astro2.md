---
title: Astro 2
permalink: /astro2/
sitemap: false
---

# 2024 Log on Astro and AstroPaper

### 6/19/2024
* See dialog in ChatGPT with suggested Astro code.

### 1/12/2025 
* Edits to original content and table created 6/20/204
* See this Claude Sonnet 3.5 dialogue for updated table adding Scheme and Haskell
* Created dev.to account and found this April, 2024 [article](https://dev.to/snikidev/astrojs-as-an-alternative-to-nextjs-pushing-the-limits-30ga) by Nikita Kakuev on how the Astro approach (if not necessarily the Astro framework) is the future. "The future is simple, vanilla JS because simplicity always wins."


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
	1. **Option 1:** install astro using `pnpm add astro` OR
	1. **Option 2:** invoke first run directly using `npx astro dev`. This command will say that we need to install `astro@5.4.3, OK to proceed (y/n)`. 
	1. Notes:
		* I chose **Option 1** and it's working now
		* On day 2, after completely deleting the `/a1-arm` directory, i did *not* need to install astro. I think this means that the astro install only has to happen once per machine?
1. Change `.bash_profile` so that we have a new shortcut to execute. instead of `np` as an alias for `npm run dev`, etc., let's use **pp** as an alias for `pnpm run dev` whih starts the local server on port ...

### III. GitHub steps
1. Verify that i have an SSH connection to github with these [instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection). Just need to use terminal to type `ssh -T git@github.com`. And reply should be `Hi xxxx! You've successfully authenticated, but GitHub does not provide shell access.`
1. Modify `.gitignore` file so that it ignores `.DS_Store`, `*.swp` files and other temporary vim files. Specifically, type in:
```
# Ignore temporary vim files
*.swp
*.swo
```
1. Create a new repo at GitHub. Just go to web interface using [these instructions](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository).
	* Do *NOT* create a readme or .gitignore file because they were already created on local system
	* Initiallly chose private visibility
	* Note, see also dialogue I had with Claude AI on 3/12/2025 for github instructions.
1. After repository is created, click green **Code** button on upper left. Under "Clone", it will have https, ssh, and GitHub CLI options. Choose `ssh` and copy that string, e.g, `git@github.com:jeff4/a1.git`.
1. Navigate to local directory, e.g, ~/demo-files/a1-arm`. 
1. Assuming SSH has been set up already, you can just type this single command to connect the local repo to the remote repo: `:git remote add origin git@github.com:jeff4/a1.git`
1. To verify that the connection is good, type: `git remote -v`
1. If your first push using `git push -u origin main` is rejected, that is probably because there is residue like an auto-generated README etc.
	* In that case, force all changes to the remote github using `git push -f origin main`

### IV. Netlify steps
1. Connect repo with Netlify so that this can run as vanilla as `https://jeffhwang-a1.netlify.app/`
1. Of the three options available at Netlify, I chose [option 1](https://docs.netlify.com/welcome/add-new-site/#import-from-an-existing-repository), to deploy a site based on an existing git repository.
1. Very simple. Just need to give Netlify access to GitHub credentials, and it all goes live very easily. Only issue is that not all GH repos automatically show up in pick-list on the Netlify side. So you need to use the Netlify module within GH.com to select other repos and then at that point, `a1` comes up as available again. It's all live now


### V. Manual changes
1. Change about page
1. remove all old AstroPaper posts
1. Experiment with having a few of the old posts ported over
1. Move all posts over
1. Change the social links
1. change DNS / custom domain over for `jeffhwang.me` over from `a4-intel` back to `a1`.
1. set up local repo on minipro-23


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

## 3/30/2025
* Need to change default color to dark mode somehow. See [main config post](https://astro-paper.pages.dev/posts/how-to-configure-astropaper-theme/) and [theme color post](https://astro-paper.pages.dev/posts/customizing-astropaper-theme-color-schemes/)
* Added more Hamlet posts.
