##Working with Social data  

The HotSchedules REST API provides a user-friendly way to obtain Social data from GooglePlaces,Yelp, and WUnderground.  

If "refresh=true" query option is specified - cache will be invalidated and refreshed.

If "proxy=true" query option is specified - no cache will be used at all and requests will be forwarded directly to the endpoint.

### API endpoint

`https://api.bodhi.space/bodhi-social/controllers/vertx/cacheserver?where=<query_json>`  


#### Yelp Data

### Yelp query format

By term and location:  
    `{  
       "term":<search term, for instance KFC, McDonalds etc> - mandatory field
       "location":<location, for instance Emeryville> - mandatory field
       "limit":<number of results to return (default:10) - optional field
       "radius":<search radius in meters> (default:100) - optional field
    }`

By phone:  
`{
   "phone":<phone number in full format> (for example +15555555555)
}`

### Yelp query example: 
By term and location:  
`https://api.bodhi.space/bodhi-social/controllers/vertx/cacheserver/yelp?where={"term":"KFC","location":"Emeryville","limit":3}`

By phone:  
`https://api.bodhi.space/bodhi-social/controllers/vertx/cacheserver/yelp?where={"phone":"+15555555555"}`

#### Wunderground Data  

### Wunderground query format: 

`{"query":<query_in_wunderground format>}`

More details about WU queries could be found here:
`http://www.wunderground.com/weather/api/d/docs?d=data/index`

### Wunderground query example: 

`https://api.bodhi.space/bodhi-social/controllers/vertx/cacheserver/wu?where={"query":"conditions/q/CA/San_Francisco.json"}`

####GooglePlaces data  

### Google Places query example  
`https://api.bodhi.space/bodhi-social/controllers/vertx/cacheserver/googleplaces?where={"query":"Empire state building"}`
