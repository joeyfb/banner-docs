# File Structure Overview

The bulk of your development work will be working within the `resources` folder. The entry point for each banner's HTML, SCSS, and Javascript will be that banner's respective self-titled file within the `resources/<html/scss/javascript>/pages` folder.

For example, if you created a banner called `my-awesome-banner`:
* The HTML entry point would be `resources/html/pages/my-awesome-banner.html`.
* The SCSS entry point would be `resources/scss/pages/my-awesome-banner.scss`.
* The Javascript entry point would be `resources/javascript/pages/my-awesome-banner.js`. 

Each banner's HTML, SCSS, and Javascript file pulls in common components, but the individual entry point allows you a great deal of customization for each banner when necessary.

### Images Overview

The image folder works slightly different. If "my-awesome-banner" was marked as a "vertical" banner, it would pull in all the images from:
* `resources/img/shared`
* `resources/img/vertical`
* `resources/img/pages/my-awesome-banner`.
