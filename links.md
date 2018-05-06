# An Important Note About Links

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
