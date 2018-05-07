# banner-docs

[Getting Started](./getting-started.md)

## Table of Contents
1. Quick Start
   * [Getting Started](#getting-started)
   * [Scaffolding](./scaffolding.md)
   * [Gulp Tasks](./gulp-tasks.md)
   * [Proper Banner Links](./links.md)
1. Developing Standard Banners
1. Developing Static Banners
1. Developing Expanding Banners

1. File Structure
  1. [File Structure - HTML](./file-structure-html.md)
  1. [File Structure - SCSS](./file-structure-scss.md)
  1. File Structure - Javascript
     1. [Standard Banners](file-structure-javascript-standard-banners)
     1. Static Banners
     1. Expanding Banners
     1. [ISI](javascript-isi)


# Getting Started

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
