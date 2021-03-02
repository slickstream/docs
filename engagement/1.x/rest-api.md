# Engagement Suite REST API (BETA)

Slickstream's Engagement Suite is now supporting a limited server-to-server REST-based API.  At this time, this API has limited functionality but that will grow over time.  Please contact us at support@slickstream.com and tell us about any
capabilities that you would like to see added to this API.

## Accessing the API

The API is accessed using HTTP requests using REST conventions.  The GET method is
used for fetching data and POST is used for anything that may affect the state.  All responses are in JSON format.

When you are given access to the API, you will be given a base URL which is specific to your site such as 
`https://api.slickstream.com/example/ABC123/v1/`.  Each method in the API is relative to that base URL.  So, for example,
to access the site summary, you will append its relative path, `site`, to the base URL.

The API is secured through the use of an API key.  You will also be given a unique key for accessing your API and it must
be added as a parameter on the end of all URLs.  

## Timestamps

Throughout the API, timestamps are returned using numbers representing the number of milliseconds since January 1, 1970 GMT.  

## Site Summary Data: /site

This returns summary information about a specified site.

```json
GET https://api.slickstream.com/example/ABC123/v1/site?apiKey=XXXXXXXXXX

200 OK
{
  "added": 1614701326000,
  "siteCode": "ABC123",
  "status": "active",
  "siteHomeUrl": "https://example.org",
  "name": "Example Site",
  "lastAudit": 1614701364000,
  "last30Days": {
    "totalPageviews": 1000,
    "netPageviews": 975,
    "sessions": 810,
    "linkClicks": 310,
    "totalWidgetClicks": 100,
    "recommendationClicks": 50,
    "searches": 220,
    "favorites": 200,
    "gamesPlayed": 50,
  },
  "totalMembers": 22,
  "indexSummary": {
    "sitemapUrls": [
      "https://example.org/sitemap.xml"
    ],
    "indexedPages": 300,
    "withImages": 292,
    "withIngredients": 240,
    "searchablePages": 260,
    "recommendablePages": 240,
    "categories": 15,
    "ingredients": 45
  }
}
```

**added**: When the site was first added into the Slickstream index*

**siteCode**: The code assigned to this site by Slickstream

**status**: The current state of this site in the Slickstream index

**siteHomeUrl**: The URL of the home page of the site

**name**:  The name associated with this site

**lastAudit**:  The timestamp of the last time this site was audited (i.e., when sitemaps were fetched and reviewed)

**last30Days**

Data is consolidated once per day shortly after midnight Pacific Time.  The data here is totaled over the past
30 days ending today at midnight Pacific Time.
* **totalPageviews**: The total number of distinct page loads recorded by Slickstream
* **netPageviews**: The number of pageviews, while omitting pageviews from bots and crawlers
* **sessions**: The number of sessions, where a session is a sequence of pageviews from the same viewer
* **linkClicks**: The number of times a link (other than Slickstream widgets) was clicked on a pageview resulting in another pageview on the same site
* **totalWidgetClicks**: The number of times a Slickstream widget was clicked and resulting in another pageview on the same site
* **recommendationClicks**: The number of times a Slickstream recommendation widget (filmstrip or content-grid) was clicked resulting in another pageview on the site
* **searches**: The number of distinct searches performed by viewers
* **favorites**: The number of times that any page was marked as a favorite
* **gamesPlayed**: The number of times a viewer engaged with a Slickstream game on the site

**totalMembers**:  The current total number of viewers who have signed in using Slickstream

**indexSummary**

This shows data about the current state of the Slickstream index:
* **sitemapUrls**: This is a list of all of the sitemap URLs being monitored 
* **indexedPages**: The total number of active pages in the index
* **withImages**: The subset of pages that have an associated image
* **searchablePages**: The subset of pages that are enabled to appear within search results
* **recommendablePages**: The subset of pages that are enabled to appear as recommendations (in filmstrips, content grids, etc.)
* **categories**: The total number of distinct categories appearing on pages in the index
* **ingredients**: The total number of distinct ingredients appearing on pages in the index


## Content Analytics: /site-content-analytics

This returns a table of information about pages in the Slickstream index for the site.  The table has one record for each page and is sorted by pageviews in descending order.  You can specify the number of records to return.  This API supports
paging.  If there are more records available, the result will include a "nextPageUrl" with a complete URL that you can use
to fetch the next page (and so forth).

```json
GET https://api.slickstream.com/example/ABC123/v1/site-content-analytics?apiKey=XXXXXXXXXX&count=50

200 OK
{
  "items": [
    {
      "pageId": "342",
      "url": "https://example.org/my-funny-valentine",
      "title": "My Funny Valentine",
      "published": 1614443364000,
      "lastUpdated": 1614443364000,
      "activeTime": 49305939,
      "widgetClicks": 24335,
      "linkClicks": 72033,
      "clickthrough": 0.04235,
      "totalFavorites": 4225,
      "favoritesPerPageview": 0.062245,
      "pageviews": 244313,
      "immediateBounces": 19333,
      "headerBiddingRevenue": 10244.3556,
      "headerBiddingRpm": 41.9836
    },
    ...
  ],
  "nextPageUrl": "https://api.slickstream.com/example/ABC123/v1/site-content-analytics?apiKey=XXXXXXXXXX&count=50&offset=50"
}
```

**item**
* **pageId**: Uniquely identifies this page within the index
* **url**: The URL to access the page, as it appears in the sitemap
* **title**: The title associated with this page in the index
* **published**: Timestamp, if available, when this page was published
* **lastUpdated**: Timestamp when the index for this page was last updated
* **activeTime**: Total active time spent on this page by all viewers over the past 30 days in milliseconds.
* **widgetClicks**: Total number of times a viewer clicked on a Slickstream widget on this page to navigate to another page on the site
* **linkClicks**: Total number of times a viewer clicked on a link (other than Slickstream widgets) on this page to navigate to another page on the site
* **clickthrough**: (widgetClicks + linkClicks)/pageviews
* **totalFavorites**: Total count of favorites (over all time) for this page.  This does not include the random "seed" used which is added when being displayed to viewers.
* **favoritesPerPageviews**: Number of new favorites added over the past 30 days divided by the total number of pageviews in that timeframe
* **pageviews**: Number of page loads recorded by Slickstream on this page over the past 30 days
* **immediateBounces**: An immmediate bounce is a pageview where the viewer never interacts with the page at all (no clicks, scrolling, etc)
* **headerBiddingRevenue**:  We monitor header bidding on the page.  This is the total of the successful ad auction amounts on all pageviews on this page over the past 30 days.  Note that for most publishers, this is a fraction of the actual revenue, but is typically a consistent fraction between pages, so a good indicator of the relative value of this page compared
with others.
* **headerBiddingRpm**:  headerBiddingRevenue/(pageviews/1000):  The revenue per 1000 pageviews for this page based on header bidding.  

**nextPageUrl**: If absent, there are no more pages to fetch.  If present, use this URL to fetch the next set of records in the table.  Note that this URL will already include the apiKey, so you do not need to add these again.