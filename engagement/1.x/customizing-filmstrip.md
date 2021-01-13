## Styling the Filmstrip

The filmstrip's standard mode shows the title of the page along with it's image. The filmstrip automatically optimizes the layout based on the screen size and adapts to the site's theme colors. 

However, there are times where you'd want to change the default styling of the filmstrip. Most of it is done using CSS custom properties. 
These properties can be set on `slick-film-strip` element or the container selector `.slick-film-strip`

Say, if you want to add padding around the film strip, change its font, and update the line-height; you can add the following style to the container:

```css
.slick-film-strip {
  padding: 16px;
  font-family: monospace;
  --slick-filmstrip-line-height: 1.2;
}
```

Here are the list of custom CSS properties to style the film strip: 

**--slick-filmstrip-cell-gap**: Sets the gap in pixels between the items in the filmstrip

**--slick-filmstrip-cell-height**: Sets the height of each item in the filmstrip in pixels (do not include units)

**--slick-filmstrip-cell-width**: Sets the width of each item in the filmstrip in pixels (do not include units)

**--slick-filmstrip-image-width**: The width of the image, including units such as px.  The height is automatically set based on the item height.

So for a cell 200px wide, 100px tall, with an image width of 80px:
```css
.slick-film-strip {
  --slick-filmstrip-cell-width: 200;
  --slick-filmstrip-cell-height: 100;
  --slick-filmstrip-image-width: 80px;
}
```

**--slick-strip-icon-bg**: Sets the background color of the scroll arrows on the filmstrip

**--slick-icon-color**: Sets the color of the scroll arrows on the filmstrip

**--slick-filmstrip-card-background**: Background of each card in the filmstrip.

**--slick-filmstrip-font-size**: Font size of the text

**--slick-filmstrip-line-height**: Line height of the text content

**--slick-filmstrip-letter-spacing**: Letter spacing of the text

**--slick-filmstrip-font-weight**: Font weight of the text

**--film-strip-card-image-radius**: Sets the border-radius of the images in the filmstrip

**--slick-filmstrip-text-padding**: Sets the padding around the text

**--slick-filmstrip-text-lines**: Number of lines of text to show

## Custom Filmstrip Cells

If you'd like to break away from the standard layout of the items in the filmstrip, you can define your own layout. 
To do that you should create a `<div>` with the class name `slick-film-strip` and add your custom HTML and CSS for each item in a `<template>` element. 
Slickstream will inject the filmstrip as a child of this `div` and use the provided template to render each cell. 

For example:

```html
<div class="slick-film-strip">
  <template>
    <div style="height: 100%; padding: 6px;">
      <style>
        .pinned {
          background: pink;
        }

        label {
          font-size: 14px;
          display: block;
        }

        img[data-image] {
          width: 50px;
          height: 50px;
          display: block;
          float: left;
          border-radius: 50% 0 50% 0;
          margin-right: 6px;
        }
      </style>
      <img data-image>
      <label data-title></label>
    </div>
  </template>
</div>
```

Notice the label has an attribute `data-title` which tells Slickstream to add the title of the page as the text of the specific element. 
Similarly, the attribute `data-image` sets the `src` of the image element. If you'd like to set the image as a background of an element, give it the attribute `data-bg-image`.

Nodes can be styled by creating a `<style>` element inside your template. These styles are automatically scoped, so you do not need to worry about conflicts with the rest of your site. 



