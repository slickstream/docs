# Highlighter

The Highligher script highlights any element on the web page when it scrolls into view the first time. 
This effect is achieved by placing the rest of the content behind a translucent background. 

- If you click on the background, the highlighting goes away
- If the element scrolls out of view again (75% of the element), the highlighting goes away
- You can optionally add a timer to automatically remove the highlighting after the specified amount of time.

## Usage
In your page, usually at the bottom of the body, include a `<script>` tag to source the highligher script. 
Then in your own script you can attach an element to to the highlighter by calling the `window.$highlight` function. 

The script is available at: https://r.slickstream.com/highlighter/highlighter-v1.js

```html
<html>
  ...
  <body>
    ...
    ...
    <script src="https://r.slickstream.com/highlighter/highlighter-v1.js"></script>
    <script>
      // This will highlight a div with the id 'mySpecialDiv' when it scrolls into view
      window.$highlight('#mySpecialDiv');
    </script>
  </body>
</html>
```

### window.$highlight

When the highligher script is loaded, it created a global `window.$highlight` function. This function takes in two arguments

**window.$highlight(selector: string, timeout?: number)**

_**selector**_ is a CSS selector that matches the element to highlight.

_**timeout**_ is an optional field. If set, the highligher will remove the highlight after the specified delay. The value is in seconds.

## Styling 

Highligher exposes a few CSS properties that can be configured by the user. 

**--highlight-backdrop-color** sets the color of the backdrop. Default value is `rgba(0,0,0,0.6)`

**--highlight-backdrop-zindex** sets the z-index of the backdrop. Default value is 999.

**--highlight-element-zindex** sets the z-index of the element to highlight, when highlighting. 
This value should be higher than the z-index of the backdrop. Default value is 999999.

In addition to these CSS properties, highlighter will add a class name **`highlighter-is-highlighting`** 
to the specified element when it is being highlighted. 
This allows you to customize the look and feel of the element if it needs to change when highlighted.
