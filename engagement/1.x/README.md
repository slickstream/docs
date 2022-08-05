# Slickstream Engagement Suite Developer Documentation (v1.x)

This documentation is to support Slickstream customers and their web developers who wish to integrate Slickstream's Engagement Suite more seamlessly into their website.

Slickstream is primarily a client-side technology -- meaning that we add functionality into a website from inside the browser, rather than when the pages are rendered by the web server.

There are three ways in which website developers can improve integration with Slickstream:

- [Positioning](#positioning)
- [Activating](#activating)
- [Styling](#styling-slickstream-widgets)
- [Javascript API](#slickstream-javascript-api-v10)

## Positioning

Slickstream injects widgets onto a page after the page has loaded.  We inject these widgets into a container (as a child element of that container).  The container is typically a `<div>` with a certain CSS class.  We are able to add that container itself if necessary.  But it is even better if the page already has the container (as rendered by the server) so that it can pre-allocate space for our widget.  Allocating space reduces the [Cumulative Layout Shift (CLS)](https://web.dev/cls/) on the page and lets you be as specific as you like about the positioning of the Slickstream widget.  Our widgets are responsive and will use the available space appropriately.

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

### Games

Slickstream lets you inject a simple game on the page based on the page's recommendations. Make sure Games are turned on in your site's config page. To specify where to inject the game, create a `div` with the class `slick-game-panel`. You may also choose to put a title for the game. 

```html
<h3>More delicious distraction...</h3>
<div class="slick-game-panel"></div>
```

Games are laid out as a square, and a footer of about `122px` with instructions for the game. So, if you add the game in a `300px` container, the height would be about `422px`. This can be useful if you'd like to pre-allocate height in your layout for the game. 

```css
.slick-game-panel {
  min-height: 422px;
}
```

## Activating

You may want to create a custom button or menu item that activates certain Slickstream features, including the search and favorites panel.  (If you wish to activate Slickstream's sign-up/sign-in dialog, use the [Client API](#slickstream-javascript-api-v1.0) below.)

To activate the search/discovery panel, there are two ways to do this:

### Use `<a>` links

Let's say you have a button and you'd like it to open Slickstream's search when clicked. You can put that button inside an anchor where the href is set to **`#search`**

```html
<a href="#search">
  <button>Search</button>
</a>
```

To open the search panel to a specific search query, set the url to **`#search?q=query`** e.g. `#search?q=curry`

Similarly you can configure the button to open the panel into different states by setting the `href` to:
* **`#list/stories`**: for listing all the stories
* **`#list/recent`**: for recent pages
* **`#list/my-recent`**: for pages recently visited by the user
* **`#list/popular`**: for popular pages
* **`#list/videos`**: lists all the videos
* **`#list/related`**: for pages related to the current page
* **`#list/my-favorites`**: to list all the user's favorites

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

**--slick-site-color**:  The site color sets the default color of our floating buttons and themes the search panel. 

e.g.

```css
body {
  --slick-site-color: #723f5f;
}
```

### Styles for Filmstrip

Filmstrip inherits the `font-family` from the container it is in. 

**--film-strip-card-image-radius**: Sets the border-radius of the images in the filmstrip

**--slick-strip-icon-bg**: Sets the background color of the scroll arrows on the filmstrip

**--slick-icon-color**: Sets the color of the scroll arrows on the filmstrip

**--slick-filmstrip-font-size**: Font size of the text

**--slick-filmstrip-line-height**: Line hight of the text content

**--slick-filmstrip-letter-spacing**: Letter spacing of the text

**--slick-filmstrip-card-background**: Background of each card in the filmstrip. 

You can also add padding around the strip by adding CSS to the container of the filmstrip, which is a div with the class `slick-film-strip`

```css
.slick-film-strip {
  padding: 0 0 16px 0;
  font-family: monospace;
}
```

### Filmstrip Toolbar

The toolbar uses all the styles in the film strip, and a couple more

**--slick-toolbar-background**: Background of the toolbar

**--slick-toolbar-shadow**: Box-shadow of the toolbar when it comes down from the top. 

### Floating Buttons

The floating buttons (heart, search) are themed automatically based on the site's theme color. But they could be further customized.

**--slick-heartbeat-color**: This is usually the same as the site color. It gives the default colors to the FABs and the floating hearts. 

**--slick-heartbeat-background**: You can override the background of the Heart FAB by setting this property

**--slick-search-fab-background**: You can override the background of the Search FAB by setting this property

**--slick-heart-fab-color**: Overrides the icon color of the Heart FAB

**--slick-search-fab-color**: Overrides the icon color of the Seart FAB

**--slick-btt-fab-background**: Overrides background of the back-to-top button 

**--slick-btt-fab-color**: Overrides color of the back-to-top icon on the button

### Search Panel

**--slick-discovery-highlight-color**: Overrides the theme color in the Search Panel. This also applies to hearts appearing within the search panel. 

**--slick-discovery-text-highlight-color**: When highlighting ingredients, color used to highlight them

**--slick-discovery-line-height**: Line height of the text in search results

### Content Grid 

Text in content grid inherits the font styles from the parent, but the `line-height` is set to `1.5`. To override the `line-height`, set the styles on the `slick-content-grid element`. This is also where you can override other font properties. 

```css
slick-content-grid {
  line-height: 1.2;
  font-family: 'Open Sans';
}
```

**--slick-grid-cell-height**: Overrides the height of images in the grid. Default value is 128px. The width of the images is flexible and adjust automatically to the grid width and the number of items in the grid.

**--slick-grid-page-item-bg**: Overrides the background of the grid. The content grid assumes it's placed on a white background. Use this property to match the color of the background of the grid. 

### Styles for Highlighter

Highlighter exposes a few CSS properties that can be configured by the user.

**--highlight-backdrop-color**: sets the color of the backdrop. Default value is rgba(0,0,0,0.6)

**--highlight-backdrop-zindex**: sets the z-index of the backdrop. Default value is 999.

**--highlight-element-zindex**: sets the z-index of the element to highlight, when highlighting. This value should be higher than the z-index of the backdrop. Default value is 999999.

In addition to these CSS properties, highlighter will add a class name highlighter-is-highlighting to the specified element when it is being highlighted. This allows you to customize the look and feel of the element if it needs to change when highlighted.


## Slickstream Javascript API v1.0

The Slickstream Javascript API provides access to a minimal set of Slickstream services from within the browser.  This API will be expanded in the next release to cover most Slickstream capabilities.  

**NOTE**: We will continue to support this 1.0 API for some time, but the 2.0 API is planned to include major changes and is unlikely to be backward-compatible.

### Events

Add an event listener on the document object to be notified when certain events occur:

- **slickstream-ready**: This event fires when the slickstream API is ready for use.
- **slickstream-user-status-change**:  This event fires when the current user's sign-in state changes.
- **slickstream-favorite-change**: This event fires when the favorite state of the current page for the current viewer has changed.

 
### Accessing the API
Once loaded, the Slickstream API is available via the window object:

```window.slickstream.v1```


### User
The user member of the API object provides access to features related to signing in, signing up, identity, etc.

* **status**:  This tells you the login status of the user (i.e., the current viewer of the page).  It is one of:
  * 'anonymous':  This is for any user that has not been authenticated;
  * 'signed-in':  This is for any user that has been authenticated via Slickstream sign-in;
  * 'client-auth':  This is for a user who has been authenticated because of meta-tags added by the site itself (e.g., based on Slickstream's WordPress plugin for viewers signed into WordPress)
* **emailAddress**:  If the current user is authenticated, this is the email address of that user.
* **name**:  If the current user is authenticated, and their name is known, this returns that value.
* **openSignInDialog(emailAddress?)**: This causes Slickstream's sign-in dialog to be shown to the viewer.  If the email address is provided, it will be used to pre-populate the corresponding field in that dialog.  Note that this covers both sign-in and sign-up scenarios.  Nothing is returned.
* **signOut()**:  This tells Slickstream to sign-out the current viewer if appropriate.  Note that this will not affect the status of a viewer in the 'client-auth' state -- as we cannot affect WordPress (or other site server) sign-in state.  This returns a Promise when the operation is complete.

 
### Favorites
The favorites member of the API object is an object supporting the Favorites feature:

- **getState()**: This method returns true if the current page is a favorite of the current viewer.
- **setState(isFavorite)**: This method sets or clears whether the current page is a favorite of the current viewer. It is asynchronous and returns a Promise.
- **getCount()**: This method returns the total number of favorites for the current page.

 
### Sample Code
```javascript
// This sample assumes you have a favorite button and
// its text content shows the current favorite state.
// Likewise, it assumes you have a login button that
// toggles between 'sign in' and 'sign out' depending
// on status
const fb = document.querySelector('#favStatusButton');
const lb = document.querySelector('#loginButton');
 
// This returns the Slickstream API object,
// waiting if necessary for loading to complete
 
async function ensureSlickstream() {
   if (window.slickstream) {
       return window.slickstream.v1;
   }
   return new Promise((resolve, reject) => {
      document.addEventListener('slickstream-ready', () => {
         resolve(window.slickstream.v1);
      });
   }); 
}
 
async function updateFavoriteButtonState() {
   const slickstream = await ensureSlickstream();
   const isFavorite = slickstream.favorites.getState();
   fb.textContent = slickstream.favorites.getState() ? `I'm a favorite` : `I'm not a favorite`;
}
 
// The login button in this example handle three different cases.
// For normal cases, it shows "log in" or "log out" appropriately.
async function updateLoginButton() {
   const slickstream = await ensureSlickstream();
   switch (slickstream.user.status) {
      case 'signed-in':
         lb.textContent = 'Log out';
         lb.disabled = false;
         break;
      case 'client-auth':
         lb.textContent = slickstream.user.emailAddress;
         lb.disabled = true; // User cannot affect state 
         break;
      case 'anonymous':
         lb.textContent = 'Log in';
         lb.disabled = false;
         break;
   }
}
 
fb.addEventListener('click', async() => {
   const slickstream = await ensureSlickstream();
   const state = slickstream.favorites.getState();
   slickstream.favorites.setState(!state);
});
 
lb.addEventListener('click', async() => {
   const slickstream = await ensureSlickstream();
   switch(slickstream.user.status) {
      case 'signed-in':
         slickstream.user.signOut();
         break;
      case 'anonymous':
         slickstream.user.openSignInDialog();
   }
});
 
// If the favorite state has changed this event will fire and
// this ensures your display of the state remains correct
document.addEventListener('slickstream-favorite-change', () => {
  updateFavoriteButtonState();
});
 
// If the current user state changes, this will update the 
// text in the login button accordingly
document.addEventListener('slickstream-user-status-change', () => {
  updateLoginButton();
}
 
// After the page loads, this will ensure your display
// is updated as soon as the info is available
updateFavoriteButtonState();
updateLoginButton();
```
