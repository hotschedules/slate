##HotSchedules API Documentation
This documentation is intended for those wanting to integrate into the HotSchedules IoT (Internet of Things) Platform.

* by building applications to the the HotSchedules IoT Platform Cloud APIs with access to real-time transactional and analytical data.  
* by building a data integration application into your point of sale system to be stored and accessed from our cloud solution utilizing a single integration point for data collection.

Accounts in the IoT Platform are called a **namespaces**. Namespaces are secured HotSchedules cloud storage locations for your business. Your namespaces are uniquely named based on your organization name.


##Access To The Cloud API 
To access the HotSchedules Cloud API, you will need to login with your user and password which is provided by HotSchedules.  The IoT Cloud API is available at this location: <a href="https://api.hotschedules.io/apidocs/index.html">https://api.hotschedules.io/apidocs/index.html</a>.  

If you enter your credentials (username and password) and click Explore, you will see a list of APIs which you can access for your namespace.  The Cloud APIs are REST APIs which returns JSON for all responses.

The Cloud API has examples and an opportunity to _**Try it out!**_.  You can add data using our provided types or create your own types.
<br><br>

**NOTE:** Should you create your own type, the new type will be available in the API Methods for your namespace.


##Logging In To The Cloud API
- Go to  <a href="https://api.hotschedules.io/apidocs/index.html">https://api.hotschedules.io/apidocs/index.html</a>
- Click Loginform from the list of Cloud API Methods
- Click POST
- Enter username
- Enter password
- Click _**Try it out!**_
- Success will be represented with a Response Code 200 message
- Scroll back to the top of the page, enter your Namespace in the box provided and click Explore 

##Exploring The Cloud API

Once logged into the Cloud API, you can both explore the provided types and their respective restful verbs: GET, PUT, DELETE, PATCH. The Cloud API is much more than API Documentation, it is a powerful interactive tool that allows the developer and/or administrator to create, update, delete data as well as manage the schema for their organization.  

- Click BodhiType
- Click GET /resources/BodhiType
- Click _**Try it out!**_
- You can scroll through the Response Body to see all the standard types that the IoT Platform team uses.
