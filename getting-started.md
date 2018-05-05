Next open up `banners.json` to customize your project. There are two objects you will need to update, banners and links.

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
