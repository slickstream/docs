# Styling Slickstream Templates for Search Results and DCM

Slickstream shows search results using a number of templates. Each template exposes some CSS properties to customize the styling of the template. This document lists the CSS custom properties exposed by each templates

### Details Template

**--slick-details-template-font-family**: Normally the font is inherited. So you can set the font on the search panel or the DCM and it will get picked up. But if you want to specify a font family that is not inherited, use this property. 

**--slick-search-card-background**: Background color of the search result item card. Default is white. 

**--slick-details-template-card-border**: Border of the card. Default is `1px solid #dfe1e5`.

**--slick-details-template-card-radius**: Card radius. Default value is `8px`.

**--slick-details-template-section-color**: Color of the *section* field in the search result. The section is like a category this result page belongs to. Default color is `#70757a`

**--slick-details-template-title-font-size**: Font size of the title of the search result. Default value is 16px.

**--slick-details-template-title-line-count**: Number of lines of title to show. Default value is 2.

**--slick-details-template-description-font-size**: Font size of the description of the item. Default size is 14px.

**--slick-details-template-description-color**: Color of the description. Default value is `#70757a`.

**--slick-details-description-title-line-count**: Number of lines of description to show. Default value is 2.

**--slick-details-template-meta-text-color**: This is the color of the *meta* information, such as rating and cooking time for recipes or reading time for articles. Default value is `#757575`

**--slick-details-template-meta-font-style**: Meta content font style. Defaults to `italic`.

**--slick-details-template-time-color**: The color of the published time.

### Title Under Image Template

**--slick-title-under-image-template-font-family**:  Normally the font is inherited. So you can set the font on the search panel or the DCM and it will get picked up. But if you want to specify a font family that is not inherited, use this property. 

**--slick-search-panel-background**: This template does not provide a solid bordered card. So the text is shown as if displayed on top of the background. So, if the search panel or DCM is using a color other than white, set this property to match that color. 

**--slick-title-under-image-template-title-font-size**: Font size of the title. Default is `14px`.

**--slick-title-under-image-template-line-count**: Number of lines of title to show. Default is 2.

**--slick-title-under-image-template-image-radius**: Radius of the result image. Default is `5px`.

**--slick-title-under-image-section-color**: Color of the *section* field in the search result. The section is like a category this result page belongs to. Default color is `#70757a`.


### Title On Image Template

**--slick-text-on-image-template-font-family**: Normally the font is inherited. So you can set the font on the search panel or the DCM and it will get picked up. But if you want to specify a font family that is not inherited, use this property. 

**--slick-text-on-image-template-card-shadow**: Cards in this template cast a box-shadow. Default value is `0 3px 1px -2px rgba(0,0,0,.2), 0 2px 2px 0 rgba(0,0,0,.14), 0 1px 5px 0 rgba(0,0,0,.12)`.

**--slick-text-on-image-template-card-radius**: Border radius of the cards. Default value is 10px.

**-slick-text-on-image-template-text-bg**: When showing text on top of image, by default the template adds a gradient background to the text to make the text more legible on top of the image. 

**--slick-text-on-image-template-font-color**: Color of the text. Default value is `white`.

**--slick-text-on-image-template-font-size**: Font size. Default value is `16px`.

**-slick-text-on-image-template-font-weight**: Font weight of the text. Default value is `400`.

**--slick-text-on-image-template-line-height**: Line height of the title text. Default is `1.35em`.

**--slick-text-on-image-template-line-count**: Number of lines of title to show. Default value is 3. 

**--slick-text-on-image-template-letter-spacing**: Letter spacing of the text. Default value is `0.5px`.

**--slick-text-on-image-template-fav-background**: When displaying a favorite button on top of the image card, the heart or favorite icon has a background set so it is more visible on the image. Default value is `rgba(255,255,255,0.75)`.

**--slick-text-on-image-template-card-hover-shadow**: When you hover of the card, the shadow changes. This cand be overriden useing this property.

