Gulp Tasks Overview
-------------------------------------------------------------------------------

A quick guide to the various Gulp taks in this framework. If you do not have Gulp globally installed, every task covered here can also be accessed by running `npm run <gulp-task>`.

### scaffold
```
gulp scaffold
```
This task will build out the file-structure and generate a couple files for you based on the contents of `banner.json`. If you alter the banners object in `banner.json` file and re-run this command, it will build files for the new banners but will not remove any previous banners that were created.

### re-scaffold
```
gulp re-scaffold
```
This task will clear out all the files from `resources/html/pages`, `resources/scss/pages`, `resources/js/pages`, and `resources/img/pages`, and then re-scaffold your project from `banners.json`. Be careful before running this command and double-check you aren't overwriting something you need.

### develop
```
gulp develop
```	
This task will build your project, place it in `dist`, and then watch for any updates within `resources`. It will not minify your CSS or Javascript, making it easier to debug. 

This build process is for *Non-Doubleclick Banners*, which means that:

* All `{{ link(<link-name>, <class-name>) }} Sample Links {{ closeLink() }}` will be rendered as `<a href="<link-url>">Sample Links</a>`
* The class "doubleclick" will not be added to the banners.
* The Enabler script, `<script src="https://s0.2mdn.net/ads/studio/Enabler.js"></script>`, will not be included in your document <head>
* All Enabler methods will be bypassed in your Javascript files.

### develop:doubleclick
```
gulp develop:doubleclick
```	
This task will build your project, place it in `dist`, and then watch for any updates within `resources`. It will not minify your CSS or Javascript, making it easier to debug. 

This build process is for *Doubleclick Banners*, which means that:

* All `{{ link(<link-name>, <class-name>) }} Sample Links {{ closeLink() }}` will be rendered as `<span class="<link-name> <class-name">Sample Links</span>`
* The class "doubleclick" will be added to the banners.
* The Enabler script, `<script src="https://s0.2mdn.net/ads/studio/Enabler.js"></script>`, will be included in your document <head>
* All Enabler methods will be executed in your Javascript files.

### build
```
gulp build
```
This task will build your project similar to `gulp develop`, but will minify all Javascript and CSS, and will run just once.

### build:doubleclick
```
gulp build:doubleclick
```
This task will build your project similar to `gulp develop:doubleclick`, but will minify all Javascript and CSS, and will run just once.

### zip
```
gulp zip
```
This task will take each folder currently in `dist`, zip it, and place it in `dist/zips`.
