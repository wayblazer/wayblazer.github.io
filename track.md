# Widget Tracker Documentation

The tracker widget currently supports the following use cases:

+ clients using the image widget
+ clients using the API client side

> __NOTICE__ The server side API use case is NOT currently supported.  Client would have to JSON.stringify and base64 encode their payload before sending.

## Tracker Implementation

Put the following code and pages that you want to track:
### HTML Snippet
```html
<script src="//cdn.wayblazer.com/widgets/v1.0/tracker.js"
 data-wb-id="tracker"
 data-apiKey="[API_KEY]"
 data-hotelProvider="[HOTEL_PROVIDER]"
 data-info="[INFO_ABOUT_REQUEST]"
 data-type="[PAGE_TYPE]"
 data-name="[PAGE_NAME]"></script>
```
### Atributes
+ __data-wb-id:__ must always equal "tracker"
+ __data-apiKey:__ your API key used in other widgets, like the image widget.
+ __data-hotelProvider:__ the provider for content used in other widgets, like the image widget.
+ __data-info:__ data about the request in __URL format__ (ex: key=value&key2=another+value). It can be anything on the list view (maybe search terms, etc.). **NOTE:** on the *detail* page you need include the content provider’s hotel id, so clicks from the search view to details can be tracked (ex: ```data-info="hotelId=some_hotel_id"```) Also, on the *cart* and *complete* pages include hotels in a comma delimited list that are in the cart or have been converted  (ex: ```data-info="hotelIds=some_hotel_id,other_hotel_id"```)
+ __data-type:__ the basic event on this page, this can include: 
	+ __search__: the list view / search result
	+ __detail__: the detail view of a hotel
	+ __cart__: shopping cart view
	+ __complete__: thank-you page / conversion / purchase complete
+ __data-name:__ descriptive info about the page. It is useful if the cart has multiple steps. EX: (ex: ```data-name="cart billing"``` and ```data-name="cart shipping info"```)

## Example Snippets
### Search Page Results
```html
<script src="//cdn.wayblazer.com/widgets/v1.0/tracker.js"
 data-wb-id="tracker"
 data-apiKey="XXX123XXX"
 data-hotelProvider="some_hotel_prodiver"
 data-info="search=cool+places+near+water&campaignId=123abc"
 data-type="search"
 data-name="widget list view"></script>
```

### Detail Page
```html
<script src="//cdn.wayblazer.com/widgets/v1.0/tracker.js"
 data-wb-id="tracker"
 data-apiKey="XXX123XXX"
 data-hotelProvider="some_hotel_provider"
 data-info="hotelId=some_hotel_id&campaignId=123abc"
 data-type="detail"
 data-name="property detail page"></script>
```

### Cart Page
```html
<script src="//cdn.wayblazer.com/widgets/v1.0/tracker.js"
 data-wb-id="tracker"
 data-apiKey="XXX123XXX"
 data-hotelProvider="some_hotel_prodiver"
 data-info="hotelIds=some_hotel_id,some_other_hotel_id,another_hotel_id&campaignId=123abc"
 data-type="cart"
 data-name="check out page"></script>
```

### Conversion Page
```html
<script src="//cdn.wayblazer.com/widgets/v1.0/tracker.js"
 data-wb-id="tracker"
 data-apiKey="XXX123XXX"
 data-hotelProvider="some_hotel_prodiver"
 data-info="hotelIds=some_hotel_id,some_other_hotel_id,another_hotel_id&campaignId=123abc"
 data-type="complete"
 data-name="thank you page"></script>
```

# Client-Side API
All the above snippets need to exist on the related pages. If you are not using the canned image widget and are calling the client-side api to get images, include the following code in the successful callback of the client-side api call:
```javascript
// if tracker is on the page, invoke its response handler
if (window.wbt && window.wbt.responseEventHandler && typeof
window.wbt.responseEventHandler === 'function') {
 window.wbt.responseEventHandler(res);
}
// end tracker
```
> __NOTE__: the *res* variable should be the raw response you get back from our client api.
 
