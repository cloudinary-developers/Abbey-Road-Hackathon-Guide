# API Specifics

## **Catalog API Endpoint - Authentication** <a id="catalog-api-endpoint-authentication"></a>

**Hackathon specific parameters to access UMG Canada catalog**

* `consumer_key = 7d4vr6cgb392`
* `consumer_secret = m4ntskavq56rddsa`
* `shopId = 2020`

**To browse the catalog, only the consumer key and shopId are required**

* `&oauth_consumer_key=7d4vr6cgb392 (Note, oauth_consumer_key is parameter name)`
* `&shopId=2020`

`http://api.7digital.com/1.2/artist/browseshopId=2020&oauth_consumer_key=7d4vr6cgb392&letter=ki`

**If you make a mistake authenticating an API call, then an HTTP 401 status code will be returned**

* `Plain text error message will also be returned indicating cause`
* `Access to resource denied = Invalid API Key passed on call OR Missing/Invalid shopId`
* `Resource not found = Invalid API Endpoint called`

## **API Endpoint - Responses** <a id="api-endpoint-responses"></a>

**API Responses default to XML - JSON is available by using “accept JSON” header**

`Curl -H “accept: application/json” ‘http://api.7digital.com/1.2/artist/browse?shopId=2020&oauth_consumer_key=7d4vr6cgb392&letter=ki’`

**API Call standard responses \(Success\)**

```text
<response status="ok" version="1.2">   <response_content /></response>
```

**API Call error responses \(Failure\)**

```text
<response status="error" version="1.2"> <error code="1001">  <errorMessage>Missing artist ID</errorMessage> </error></response>
```

**​**[**A list of error codes and messages can be found on this page**](https://cloudinary.gitbook.io/abbey-road-hackathon-2018/7digital/api-error-codes-and-messages)​

## **API Endpoint - Paging** <a id="api-endpoint-paging"></a>

**Our catalog endpoints use paging to return large sets of results, A typical call might return these elements in the response**

```text
<searchResults><page>1</page><pageSize>10</pageSize><totalItems>460</totalItems><searchResult>
```

**You need to use - page and pagesize parameters to access the entire result set**

* `&page={int} default=1`
* `&pagesize={int} default=10, max=50`

**Example call with paging parameters**

`http://api.7digital.com/1.2/artist/browse?letter=ki&shopId=2020&oauth_consumer_key=7d4vr6cgb392&page=2&pagesize=50`

## **Accessing Artist & Album Artwork** <a id="accessing-artist-and-album-artwork"></a>

**The release and track endpoints return an URL to the album artwork**

```text
<image>http://artwork-cdn.7static.com/static/img/sleeveart/00/057/262/0005726299_50.jpg</image>
```

**We have the following sizes available**

* 33, 50, 100, 180, 182, 200, 350, 500 and 800 pixels

**50 is returned as default, to adjust this, add imageSize parameter to your api call**

**​**[**http://api.7digital.com/1.2/release/details?shopId=2020&oauth\_consumer\_key=7d4vr6cgb392&releaseId=5726299&usageTypes=adsupportedstreaming&imageSize=800**](http://api.7digital.com/1.2/release/details?shopId=2020&oauth_consumer_key=7d4vr6cgb392&releaseId=5726299&usageTypes=adsupportedstreaming&imageSize=800)

_**Please Note -**_ All the endpoints return an URL for an artist image - however the image is not always be present as we no longer support this feature  


