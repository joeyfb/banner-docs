# banner-docs

[Getting Started](./getting-started.md)

## Table of Contents
1. Quick Start
   * 1.1 [Getting Started](#getting-started)
   * 1.2 [Scaffolding](./scaffolding.md)
   * 1.3 [Gulp Tasks](#gulp-tasks-overview)
   * 1.4 [Proper Banner Links](./links.md)

1. File Structure
  1. [File Structure - HTML](./file-structure-html.md)
  1. [File Structure - SCSS](./file-structure-scss.md)
  1. File Structure - Javascript
     1. [Standard Banners](file-structure-javascript-standard-banners)
     1. Static Banners
     1. Expanding Banners
     1. [ISI](javascript-isi)


# 1. Quick Start

## 1.1 Getting Started

Open up `banners.json` to customize your project. There are two objects you will need to update, banners and links.

### Banners

```javascript
"banners": {
  "<banner-name>": {
    "width": 160,              // Enter Banner Width in Pixels
    "height": 600,             // Enter Banner Height in Pixels
    "orientation": "vertical", // Enter either 'horizontal' or 'vertical'
    "static": true             // Enter either true or false
  }
}
```

The project structure will be built from this   

### Links
```json
"<link-name>": {
  "displayName": "<displayed-link-name>",
  "href": "<url-of-link>"
}
```

Banners deployed to doubleclick studio do not use traditional anchor tags, but handle all linking through javascript. The necessary javascript functions will be built from the information that is provided here.


## 1.3 Gulp Tasks Overview

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

## 1.4 Banner Links

If a banner is going to be deployed on Doubleclick Studio, it does not use anchor tags, but handles everything in Javascript. If the banner is not for Doubleclick Studio, it will have standard anchor tags. This framework is built to have one link syntax which will be rendered as Doubleclick links in one build process and anchor tags in another build process.

When inserting a link into your HTML, write it as follows:
```html
<p>A sample paragraph with a {{ link(<link-name>, '<class-name>') }}Sample Link{{ closeLink() }}</p>
```
The link name that you pass in should match a <link-name> that you placed in `banners.json`. The second paramater will be added as a class to the link when rendered. Some classes will be added automatically, but you can optionally add your own here.

### Links for Doubleclick Studio

When you run `gulp develop:doubleclick` or `gulp build:doubleclick` the links will be rendered as "span" elements. Add the class "exit-link" to underline the next and make it inherit the parent element's color (this matches the appearance of an anchor tag). If you are adding the link to an image or container <div>, you typically would not add the "exit-link" class.

```html
<!-- The following link -->

{{ link('myCoolLink', 'exit-link awesome-class') }}Click Here{{ closeLink() }}

<!-- Will be rendered to -->
<span class="exit-link awesome-class">Click Here</span>
```

### Links for Other Platforms

When your run `gulp develop` or `gulp build` the links will be rendered as anchor tags. Remeber that the "src" url will be pulled from the matching link name in `banners.json`.

```html
<!-- The following link -->

{{ link('myCoolLink', 'exit-link awesome-class') }}Click Here{{ closeLink() }}

<!-- Will be rendered to -->
<a src="http://awesome-url.com" target="_blank" class="exit-link awesome-class">Click Here</a>
```

# 2. File Structure

### Overview

##### Overview - HTML, SCSS, JS

The bulk of your development work will be working within the `resources` folder. The entry point for each banner's HTML, SCSS, and Javascript will be that banner's respective self-titled file within the `resources/<html/scss/javascript>/pages` folder.

For example, if you created a banner called `my-awesome-banner`:
* The HTML entry point would be `resources/html/pages/my-awesome-banner.html`.
* The SCSS entry point would be `resources/scss/pages/my-awesome-banner.scss`.
* The Javascript entry point would be `resources/javascript/pages/my-awesome-banner.js`. 

Each banner's HTML, SCSS, and Javascript file pulls in common components, but the individual entry point allows you a great deal of customization for each banner when necessary.

##### Overview - Images

The image folder works slightly different. If "my-awesome-banner" was marked as a "vertical" banner, it would pull in all the images from:
* `resources/img/shared`
* `resources/img/vertical`
* `resources/img/pages/my-awesome-banner`.

## 2.1 - File Structure - HTML

This framework uses Nunjucks Rendering to create HTML files during it's build prcoess. You can learn more about Nunjucks by reading their documentation <a href="https://mozilla.github.io/nunjucks/">here</a>

Navigate to `resources/html/pages` to see the HTML entry point for each banner, generated by the scaffolding process. We will quickly walk through each section in this file. 

### Set Banner-Specific Information

```nunjucks
{% set banner = "sample-standard-banner" %}
{% set width = 160 %} 
{% set height = 600 %}
{% from "./links.html" import link, closeLink, enabler %}
```

The first three lines are setting properties within the <head> component and adding the name of the banner as a class to the banner-container.

The fourth line is importing Macros to build either standard links or doubleclick links depending on the build process which is run. When `gulp develop` or `gulp build` is run, it will import the macros from `resources/html/macros/dataLinks/links.html`. When `gulp develop:doubleclick` or `gulp build:doubleclick` is run, it will import the macros from `resources/html/macros/dcLinks/links.html`. 

### Extending Layouts

```nunjucks
<!-- In Standard Banners -->
{% extends "layout.html" %}

<!-- In Static Banners -->
{% extends "layout-static.html" %}

<!-- In Expanding Banners -->
{% extends "layout-expanding.html %}
```

These three layout files can all be found within `resources/html/components`. You can edit these files for changes you would like to see across all banners of one type.

```nunjucks
{% block bannerClass %}{% endblock %}
```
As mentioned above, the name of the banner will be added as a class to the outer banner container. If you would like to add any more classes to this <div>, enter them in this block.

### Content Blocks

##### For Standard Banners - Main Content and ISI

```nunjucks
{% block content %}
  {% include './main-content.html' %}
  <!--enter page specific content here-->
{% endblock %}

{% block isi %}
  {% include './isi.html' %}
{% endblock %}
```
All standard banners will include the content located in `resources/html/components/main-content.html`. The bulk of your HTML development will happen in this file.

All standard banners will also include the "Important Safety Information" content located in `resources/html/components/isi.html`. 

##### For Static Banners - Main Content

```nunjucks
{% block content %}
  {% include './main-content-static.html' %}
  <!--enter page specific content here-->

{% endblock %}
```
All static banners will include the content located in `resources/html/components/main-content-static.html`. The bulk of your HTML development will happen in this file.

Static banners typically do not include the Important Safety Information, which is why the "isi" block is excluded by default.

##### For Expanding Banners - Main Content and ISI Collapsed, Main Content and ISI Expanded

```nunjucks
{% block mainContentCollapsed %}
  {% include './main-content-collapsed.html' %}
  <!--enter page specific content here-->
{% endblock %}

{% block isiCollapsed %}
  {% include './isi.html' %}
{% endblock %}

{% block mainContentExpanded %}
  {% include './main-content-expanded.html' %}
  <!--enter page specific content here-->
{% endblock %}

{% block isiExpanded %}
  {% include './isi.html' %}
{% endblock %}
```

The required structure for an expanding banner is to have one main panel, with a collapsed panel and expanded panel inside of it. Typically, the main content of your collapsed banner and your expanded banner will be different, so each block is pulling in a different file (either `resources/html/components/main-content-collapsed.html` or `resources/html/components/main-content-expanded.html`. 

Often your ISI will be identical on both, which is why both the collapsed ISI block and expanded ISI block are pulling in the same file by default. 

