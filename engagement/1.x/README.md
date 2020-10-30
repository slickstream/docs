# Slickstream Engagement Suite Developer Documentation (v1.x)

## Widget placeholders

When Slickstream adds a widget on a page, it looks for an element (usually a `<div>`) with an appropriate class name and then injects the widget as a child of that element. 

Websites can take advantage of this by pre-allocating a space for the widget. Allocating a space reduces the [Cumulative Layout Shift (CLS)](https://web.dev/cls/) on the page. 

### Filmstrip

When allocating a space for a filmstrip, create a `<div>` with the class name `slick-film-strip` and allocating a minimum height of `72px` to it. For small screens, a width less than `600px`, the film strip only takes up `60px` in height. 

So, in your template you can add the following:

```html
<div class="slick-film-strip"></div>

<style>
.slick-film-strip {
  min-height: 72px;
}

@media (max-width: 600px) {
  .slick-film-strip {
    min-height: 60px;
  }
}
</style>
```

### Content Grid

To inject a content grid anywhere on the page, create a `div` with the class `slick-content-grid`. What shows up in the grid is configured on your site's Slickstream's portal.

```html
<div class="slick-content-grid" data-config="grid1"></div>
```

Note in this example, the `data-config` attribute is set to identify the configuration set in the portal. If it is not specified, the first or default config is used.

## Launching Slickstream's Search and Discovery Panel

You may want to create a custom button that opens up Slickstream's search panel. There are two ways to do this:

### Use `<a>` links

Let's say you have a button and you'd like it to open Slickstream's search when clicked. You can put that button inside an anchor where the href is set to `#slick-search`

```html
<a href="#slick-search">
  <button>Search</button>
</a>
```

Similarly you can configure the button to open the user's favorites by setting the `href` to **`#slick-search-favorites`**. <br>
**`#slick-search-related`** For related posts.<br>
**`#slick-search-recent`** For latest posts.<br>
**`#slick-search-popular`** For popular posts.<br>

### Launching via JavaScript

Using `<a>` elements to launch Slickstream is great but sometimes you may want to trigger it via JavaScript. You can do that by dispatching a custom event from the document. 

To open search:
```javascript
document.dispatchEvent(new CustomEvent('slick-show-discovery'));
```

If you want to open to a specific category, e.g. favories or recent, you need to provide a bit of extra data:

```javascript
// Opens favorites
document.dispatchEvent(new CustomEvent('slick-show-discovery', {detail: { page: 'favorites' } }));

// Opens related
document.dispatchEvent(new CustomEvent('slick-show-discovery', {detail: { page: 'related' } }));
```

## Styling Slickstream Widgets

Slickstream maintains a consistent styling for its widgets so they can work easily on all our client sites. We control the styling by encapsulating the widgets inside a [Shadow DOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM). We do, however, expose many styling options via CSS properties to configure certain aspects of our widgets. 

### Theme color

**--slick-site-color**  The site color sets the default color of our floating buttons and themes the search panel. 

e.g.

```css
body {
  --slick-site-color: #723f5f;
}
```

### Styles for Filmstrip

Filmstrip inherits the `font-family` from the container it is in. 

**--film-strip-card-image-radius** Sets the border-radius of the images in the filmstrip

**--slick-strip-icon-bg** Sets the background color of the scroll arrows on the filmstrip

**--slick-icon-color** Sets the color of the scroll arrows on the filmstrip

**--slick-filmstrip-font-size** Font size of the text

**--slick-filmstrip-line-height** Line hight of the text content

**--slick-filmstrip-letter-spacing** Letter spacing of the text

**--slick-filmstrip-card-background** Background of each card in the filmstrip. 

You can also add padding around the strip by adding CSS to the container of the filmstrip, which is a div with the class `slick-film-strip`

```css
.slick-film-strip {
  padding: 0 0 16px 0;
  font-family: monospace;
}
```

### Filmstrip Toolbar

The toolbar uses all the styles in the film strip, and a couple more

**--slick-toolbar-background** Background of the toolbar

**--slick-toolbar-shadow** Box-shadow of the toolbar when it comes down from the top. 

### Floating Buttons

The floating buttons (heart, search) are themed automatically based on the site's theme color. But they could be further customized.

**--slick-heartbeat-color** Color of the heart button

**--slick-heartbeat-background** Background cplor of the heart button

**--slick-search-fab-background** Background color of the search button

**--slick-search-fab-color** Color of the search icon on the button

**--slick-btt-fab-background** Background of the back-to-top button 

**--slick-btt-fab-color** Color of the back-to-top icon on the button

### Search Panel

**--slick-discovery-text-highlight-color** When highlighting ingredients, color used to highlight them

**-slick-discovery-line-height** Line height of the text in search results

