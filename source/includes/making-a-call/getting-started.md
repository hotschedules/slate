#Getting Started

The HotSchedules IoT Platform (Bodhi) REST API allows you to query meta-data about your stores, labor, sales, and HotSchedules Agents running in your stores. You can also do some fancy things like get social information, upload files, send push notifications and emails, and even make payments.

###Base URL

All URLs referenced in the documentation have the following base:

`https://api.bodhi.space/<organization_name>`

The Bodhi REST API is served over HTTPS. To ensure data privacy, unencrypted HTTP is not supported.

##Authenticating To The API


HTTP requests to the REST API are protected with HTTP Basic and HTTP Cookie authentication.  In short, you will use your HotSchedules IoT Platform account credentials (username and password) for HTTP Basic authentication. If you do not have credentials, you can signup at bodhi.space or directly [Here](https://bodhi.space/signup) 

Syntax:
`curl -ik -u username:password -X GET https://api.bodhi.space/me`

For example:
`curl -ik -u platform:user -X GET https://api.bodhi.space/me`

Your results will look like this:  
HTTP/1.1 200 OK  
Server: nginx/1.8.0  
Date: Sat, 21 May 2016 15:22:26 GMT  
Content-Type: application/json; charset=utf-8  
Content-Length: 456  
Connection: keep-alive  
Access-Control-Allow-Credentials: true  
Access-Control-Allow-Headers:  
Access-Control-Allow-Methods: *  
Access-Control-Allow-Origin: 
Access-Control-Expose-Headers: WWW-Authenticate, Server-Authorization, Location  
Request-Time: 383  
Set-Cookie: RUSK="8a6f98bb1033055fc04d644c0006789335f96c2b-username=platform"; Path=/; Domain=.bodhi.space; Secure; HTTPOnly

`{"lastName":"User","sys_created_at":"2016-05-21T15:22:11.157Z","authorizations":[{"namespace":"bodhi-social","read":true}],"profiles":["bodhi-social.user"],"usertype":"person","firstName":"Platform","sys_id":"57407d23b3b82c51e5cb3afb","password":"$2a$12$C/ZJYSZ4qkR5pU5yHQEkLuvcOVjP4rqLdOHlPq4zcDZt9dcYpBeMC","sys_version":1,"email":"customercare@hotschedules.com","username":"platform","sys_type_version":12}`


Next, read the Set-Cookie header to get your cookie string:  
`RUSK="8a6f98bb1033055fc04d644c0006789335f96c2b-username=platform"` in the example

Now use the cookie auth to authenticate to the API  
`curl -ik --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=platform" -X GET https://api.bodhi.space/me`

Cookie authorization does not expire and can be used to authenticate moving forward.

Once your Organization is setup in the platform (you can signup for free at https://developer.bodhi.space) you can access your data at https://api.bodhi.space/<organization_name> .

So for example, if your organization name is my-deli, your URL would be `https://api.bodhi.space/my-deli`

##IDM How to Programatically Retrieve JWT Tokens

**Endpoint**

**Dev:** [https://login.bodhi-dev.io/auth/realms/hotschedules/protocol/openid-connect/token](https://login.bodhi-dev.io/auth/realms/hotschedules/protocol/openid-connect/token)

**Prod:** [https://login.hotschedules.io/auth/realms/hotschedules/protocol/openid-connect/token](https://login.hotschedules.io/auth/realms/hotschedules/protocol/openid-connect/token)

**Header** 

* content-type: application/x-www-form-urlencoded

**Params**

* grant_type 

    * Value must be "password" 

* client_id

    * Value must be "urn:mace:oidc:hotschedules.com"

* username

    * Value should reflect the username of account you’re requesting tokens for

* password

    * Value should reflect the password of the account you’re requesting tokens for

**Return**

* access_token

* id_token

* refresh_token

**Sample Call (Postman)**

![alt text](/images/postman.png?raw=true "Postman")  

>**Sample Call (Curl)**


```
curl -X POST \

  https://login.bodhi-dev.io/auth/realms/hotschedules/protocol/openid-connect/token \

  -H 'cache-control: no-cache' \
  
  -H 'content-type: application/x-www-form-urlencoded' \
  
  -d 'grant_type=password&client_id=urn%3Amace%3Aoidc%3Ahotschedules.com&username=username&password=password'


**Sample Call (Node)**

var request = require("request");

var options = { method: 'POST',

  url: 'https://login.bodhi-dev.io/auth/realms/hotschedules/protocol/openid-connect/token',

  headers: 

   { 'cache-control': 'no-cache',

     'content-type': 'application/x-www-form-urlencoded' },

  form: 

   { grant_type: 'password',

     client_id: 'urn:mace:oidc:hotschedules.com',

     username: 'username',

     password: 'password' } };

request(options, function (error, response, body) {

  if (error) throw new Error(error);

  console.log(body);

});

```

>**Sample Results**


```
{

    "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJhWnRINE56ejBGZURjMU1FSkIyU2lIeHhGS0xuLXQtVm1DUHBHeUVnS09BIn0.eyJqdGkiOiI3NmM1YjIyMC03NjQxLTRhYzctYTA5NS02ZjU4NWY0ZGE1MzIiLCJleHAiOjE1MDM0NzU3MzYsIm5iZiI6MCwiaWF0IjoxNTAzMzY3NzM2LCJpc3MiOiJodHRwczovL2xvZ2luLmJvZGhpLWRldi5pby9hdXRoL3JlYWxtcy9ob3RzY2hlZHVsZXMiLCJhdWQiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJzdWIiOiI3NDE4MjRhYy0zMjlkLTQ4OTAtYTRmNi0zMmJmMTBiNjJhMjEiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiI4YjdkNTc2Ny04MTYyLTQyMTgtODVmNi1hMzRjYTY5ZDVkNGQiLCJhY3IiOiIxIiwiY2xpZW50X3Nlc3Npb24iOiIwYzVlMDc3Zi0yNzBjLTQ0YWUtOTllNS00ZmQwMzkyOTM4YjciLCJhbGxvd2VkLW9yaWdpbnMiOltdLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsiYWRtaW4iLCJ1bWFfYXV0aG9yaXphdGlvbiIsInVzZXIiXX0sInJlc291cmNlX2FjY2VzcyI6eyJyZWFsbS1tYW5hZ2VtZW50Ijp7InJvbGVzIjpbIm1hbmFnZS11c2VycyJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsInZpZXctcHJvZmlsZSJdfX0sInByZWZlcnJlZF91c2VybmFtZSI6InRyYXZpc2pvaG5zb25teGRldiJ9.U7YARFPbRJVHzPdQfXIvsUneZe44AQdBcR5JR8rqC8h2lFO1LkGfsO-yrLGYsnjzroJg3cJ8XD9yJOY7sLNSTAKX3FTKpBViQ2LrOlcyR4eNQrl3dfM6hVSQHAgwItJ3wSsTQk2feCj0jIj69JmT63mjkOGsBCfhO8lRvWGmVUHm3eXw4F1_h-KATKEGi4xjLgD5GoRn30FZ1BYn-7GQBgU-sAxge_dr0IQe2f8PjIqNSEKfv01NMmn4LpKjNRUiTZbb-pe1AK0j7yy6mf0reduKUTXp0S51QGuaG2Qe9uokYyfLhHuu6bja7OQ7ax8uYlpwVTF8xKpNhosDBmHw2A",

    "expires_in": 108000,

    "refresh_expires_in": 1800,

    "refresh_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJhWnRINE56ejBGZURjMU1FSkIyU2lIeHhGS0xuLXQtVm1DUHBHeUVnS09BIn0.eyJqdGkiOiJhYzcxOWI1Ny04OTA2LTRkMDYtYmU5My1mNDM3ZjM4M2M2M2IiLCJleHAiOjE1MDMzNjk1MzYsIm5iZiI6MCwiaWF0IjoxNTAzMzY3NzM2LCJpc3MiOiJodHRwczovL2xvZ2luLmJvZGhpLWRldi5pby9hdXRoL3JlYWxtcy9ob3RzY2hlZHVsZXMiLCJhdWQiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJzdWIiOiI3NDE4MjRhYy0zMjlkLTQ4OTAtYTRmNi0zMmJmMTBiNjJhMjEiLCJ0eXAiOiJSZWZyZXNoIiwiYXpwIjoidXJuOm1hY2U6b2lkYzpob3RzY2hlZHVsZXMuY29tIiwiYXV0aF90aW1lIjowLCJzZXNzaW9uX3N0YXRlIjoiOGI3ZDU3NjctODE2Mi00MjE4LTg1ZjYtYTM0Y2E2OWQ1ZDRkIiwiY2xpZW50X3Nlc3Npb24iOiIwYzVlMDc3Zi0yNzBjLTQ0YWUtOTllNS00ZmQwMzkyOTM4YjciLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsiYWRtaW4iLCJ1bWFfYXV0aG9yaXphdGlvbiIsInVzZXIiXX0sInJlc291cmNlX2FjY2VzcyI6eyJyZWFsbS1tYW5hZ2VtZW50Ijp7InJvbGVzIjpbIm1hbmFnZS11c2VycyJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsInZpZXctcHJvZmlsZSJdfX19.VPD0wzTwpyXoqVoax0FWT53PznjDLsARUPyBKsqR7e5PAv5_hpMKdPVYqVQh0bKJWpV5XDSgISyJjg4lbvW7Zb-jG7Q-bAS3vT5jfp_WE_JoPqKzgdp-oq463hVPD_vPL_UzpXH5uX1gN2x2rgt7IOU7_uYFK0preUCOsBGG_ioDLyHLZ9_0BizNc59Tzdjv5gQHammDF2jbHG2g3XurLqVbGtEjGEwkO5Zax02YfslOaOHuff_litJsw9QlN7MIFEMDRpwPT3H2hQkVpQw7Du_Sd6XZxU0BQmK599wb5D7zn2O7wlpNQcxGl1U1CA7Dqnrqn6YoVpOske8nz-qpmg",

    "token_type": "bearer",

    "id_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJhWnRINE56ejBGZURjMU1FSkIyU2lIeHhGS0xuLXQtVm1DUHBHeUVnS09BIn0.eyJqdGkiOiJjMTNkYzk4My1kZjQ1LTQ1MjgtYWEwMi1hZTIzZGUzYzhkNzYiLCJleHAiOjE1MDM0NzU3MzYsIm5iZiI6MCwiaWF0IjoxNTAzMzY3NzM2LCJpc3MiOiJodHRwczovL2xvZ2luLmJvZGhpLWRldi5pby9hdXRoL3JlYWxtcy9ob3RzY2hlZHVsZXMiLCJhdWQiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJzdWIiOiI3NDE4MjRhYy0zMjlkLTQ4OTAtYTRmNi0zMmJmMTBiNjJhMjEiLCJ0eXAiOiJJRCIsImF6cCI6InVybjptYWNlOm9pZGM6aG90c2NoZWR1bGVzLmNvbSIsImF1dGhfdGltZSI6MCwic2Vzc2lvbl9zdGF0ZSI6IjhiN2Q1NzY3LTgxNjItNDIxOC04NWY2LWEzNGNhNjlkNWQ0ZCIsImFjciI6IjEiLCJvdGhlckNsYWltcyI6eyJib2RoaWFwaSI6InRyYXZpc2pvaG5zb25teGRldiJ9LCJwcmVmZXJyZWRfdXNlcm5hbWUiOiJ0cmF2aXNqb2huc29ubXhkZXYifQ.jMRuuajwcXKdPV1NR-Ba38PWs55ES0Ff-LmMdEsVhC3ftD8__uIKOY1lBlT7ZS_b7P92h4yHTGzx6_RBS2GXEX6qSocltbY8ETVpS0uVPNShQD4EenKBXSgWtvkCvYASKUooOCfO_D7UgwdsXqojgsTR6j9fS10rA3FO_ewQGvimYvUwqpdQr844TSpPGvxmMZj4lvXPGXD77R8GyuZxOyKM2kM5vj2DFO8YZeI7dO0o3XKp2ccRnDSq0SI38sVO9mBcRcdfm6Z8gaiACS__39w3YtP6JfZMALUxfIDdYPG9Ttz264vUwrKGa25ckbzCDqUYJ4zazVrneglC6FzysA",

    "not-before-policy": 0,

    "session_state": "8b7d5767-8162-4218-85f6-a34ca69d5d4d"

}

```

##IDM How to Refresh JWT Tokens

**Endpoint**

**Dev:** [https://login.bodhi-dev.io/auth/realms/hotschedules/protocol/openid-connect/token](https://login.bodhi-dev.io/auth/realms/hotschedules/protocol/openid-connect/token)

**Prod:** [https://login.hotschedules.io/auth/realms/hotschedules/protocol/openid-connect/token](https://login.hotschedules.io/auth/realms/hotschedules/protocol/openid-connect/token)

**Header** 

*   authorization: Bearer <user refresh token>
*   content-type: application/x-www-form-urlencoded

**Params**

*   grant_type 
    *   Value must be "refresh_token" 
*   client_id
    *   Value must be "urn:mace:oidc:hotschedules.com"
*   refresh_token
    *   Value should reflect the refresh token of account you're requesting tokens for

**Return**

*   access_token
*   id_token
*   refresh_token

**Sample Call (Postman)**

![alt text](/images/refreshjwt.png?raw=true "Postman") 

>**Sample Call (Curl)**

```
curl -X POST \
  https://login.bodhi-dev.io/auth/realms/hotschedules/protocol/openid-connect/token \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJhWnRINE56ejBGZURjMU1FSkIyU2lIeHhGS0xuLXQtVm1DUHBHeUVnS09BIn0.eyJqdGkiOiJmNGQwNjQyOC1jNzIzLTQ0YWYtOTRmYS00MGI2MGQ3MWQxMmQiLCJleHAiOjE1MDMzNzA4MzQsIm5iZiI6MCwiaWF0IjoxNTAzMzY5MDM0LCJpc3MiOiJodHRwczovL2xvZ2luLmJvZGhpLWRldi5pby9hdXRoL3JlYWxtcy9ob3RzY2hlZHVsZXMiLCJhdWQiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJzdWIiOiI3NDE4MjRhYy0zMjlkLTQ4OTAtYTRmNi0zMmJmMTBiNjJhMjEiLCJ0eXAiOiJSZWZyZXNoIiwiYXpwIjoidXJuOm1hY2U6b2lkYzpob3RzY2hlZHVsZXMuY29tIiwiYXV0aF90aW1lIjowLCJzZXNzaW9uX3N0YXRlIjoiMGE4MTQzYjktNmMzNC00ZTcxLWI4YWMtZjkyNDRjZjJhZjgyIiwiY2xpZW50X3Nlc3Npb24iOiJlMDgxNDBkNi1lODVlLTQzOGQtYmZjYi03ODY2YmFkZTlkODMiLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsiYWRtaW4iLCJ1bWFfYXV0aG9yaXphdGlvbiIsInVzZXIiXX0sInJlc291cmNlX2FjY2VzcyI6eyJyZWFsbS1tYW5hZ2VtZW50Ijp7InJvbGVzIjpbIm1hbmFnZS11c2VycyJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsInZpZXctcHJvZmlsZSJdfX19.QifLXuXYanmKlh8fDpLqurhb1S3hpEVwObUWcfMvv-_M0PCWyXJ4lKZHHhWVQAD9dhTc9Eqqpy9jdrTjTR76P67wFzP4me6CVXI9tVRC1xb82ccPg4RsRu-UfEu0B87sg6pcjc4k6fp9_2YV02dLhA52rnP-19gCEPkF5SYTex2wWxzdoHwXgAaHxO4HWc4Mru_x4Pu5iLLGJ6c13Nq_t3YbsrTuAb11FV5F2IlHDBmIcqJKf0PanrWVuORyQyZuOgRaspgVsHr8nQNzHf81DiB5Fy4sa9MubRzEZvo_HEd-KcnTlo0_-WhI5gComAR-fM9hIKc5zZvLd9CO84asSg' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'grant_type=refresh_token&client_id=urn%3Amace%3Aoidc%3Ahotschedules.com&refresh_token=eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJhWnRINE56ejBGZURjMU1FSkIyU2lIeHhGS0xuLXQtVm1DUHBHeUVnS09BIn0.eyJqdGkiOiJmNGQwNjQyOC1jNzIzLTQ0YWYtOTRmYS00MGI2MGQ3MWQxMmQiLCJleHAiOjE1MDMzNzA4MzQsIm5iZiI6MCwiaWF0IjoxNTAzMzY5MDM0LCJpc3MiOiJodHRwczovL2xvZ2luLmJvZGhpLWRldi5pby9hdXRoL3JlYWxtcy9ob3RzY2hlZHVsZXMiLCJhdWQiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJzdWIiOiI3NDE4MjRhYy0zMjlkLTQ4OTAtYTRmNi0zMmJmMTBiNjJhMjEiLCJ0eXAiOiJSZWZyZXNoIiwiYXpwIjoidXJuOm1hY2U6b2lkYzpob3RzY2hlZHVsZXMuY29tIiwiYXV0aF90aW1lIjowLCJzZXNzaW9uX3N0YXRlIjoiMGE4MTQzYjktNmMzNC00ZTcxLWI4YWMtZjkyNDRjZjJhZjgyIiwiY2xpZW50X3Nlc3Npb24iOiJlMDgxNDBkNi1lODVlLTQzOGQtYmZjYi03ODY2YmFkZTlkODMiLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsiYWRtaW4iLCJ1bWFfYXV0aG9yaXphdGlvbiIsInVzZXIiXX0sInJlc291cmNlX2FjY2VzcyI6eyJyZWFsbS1tYW5hZ2VtZW50Ijp7InJvbGVzIjpbIm1hbmFnZS11c2VycyJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsInZpZXctcHJvZmlsZSJdfX19.QifLXuXYanmKlh8fDpLqurhb1S3hpEVwObUWcfMvv-_M0PCWyXJ4lKZHHhWVQAD9dhTc9Eqqpy9jdrTjTR76P67wFzP4me6CVXI9tVRC1xb82ccPg4RsRu-UfEu0B87sg6pcjc4k6fp9_2YV02dLhA52rnP-19gCEPkF5SYTex2wWxzdoHwXgAaHxO4HWc4Mru_x4Pu5iLLGJ6c13Nq_t3YbsrTuAb11FV5F2IlHDBmIcqJKf0PanrWVuORyQyZuOgRaspgVsHr8nQNzHf81DiB5Fy4sa9MubRzEZvo_HEd-KcnTlo0_-WhI5gComAR-fM9hIKc5zZvLd9CO84asSg'
```


>**Sample Call (Node)**


```
var request = require("request");

var options = { method: 'POST',
  url: 'https://login.bodhi-dev.io/auth/realms/hotschedules/protocol/openid-connect/token',
  headers: 
   { 'postman-token': '3759ed14-04f9-cc9d-9863-c8c9938c9f18',
     'cache-control': 'no-cache',
     'content-type': 'application/x-www-form-urlencoded',
     authorization: 'Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJhWnRINE56ejBGZURjMU1FSkIyU2lIeHhGS0xuLXQtVm1DUHBHeUVnS09BIn0.eyJqdGkiOiJmNGQwNjQyOC1jNzIzLTQ0YWYtOTRmYS00MGI2MGQ3MWQxMmQiLCJleHAiOjE1MDMzNzA4MzQsIm5iZiI6MCwiaWF0IjoxNTAzMzY5MDM0LCJpc3MiOiJodHRwczovL2xvZ2luLmJvZGhpLWRldi5pby9hdXRoL3JlYWxtcy9ob3RzY2hlZHVsZXMiLCJhdWQiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJzdWIiOiI3NDE4MjRhYy0zMjlkLTQ4OTAtYTRmNi0zMmJmMTBiNjJhMjEiLCJ0eXAiOiJSZWZyZXNoIiwiYXpwIjoidXJuOm1hY2U6b2lkYzpob3RzY2hlZHVsZXMuY29tIiwiYXV0aF90aW1lIjowLCJzZXNzaW9uX3N0YXRlIjoiMGE4MTQzYjktNmMzNC00ZTcxLWI4YWMtZjkyNDRjZjJhZjgyIiwiY2xpZW50X3Nlc3Npb24iOiJlMDgxNDBkNi1lODVlLTQzOGQtYmZjYi03ODY2YmFkZTlkODMiLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsiYWRtaW4iLCJ1bWFfYXV0aG9yaXphdGlvbiIsInVzZXIiXX0sInJlc291cmNlX2FjY2VzcyI6eyJyZWFsbS1tYW5hZ2VtZW50Ijp7InJvbGVzIjpbIm1hbmFnZS11c2VycyJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsInZpZXctcHJvZmlsZSJdfX19.QifLXuXYanmKlh8fDpLqurhb1S3hpEVwObUWcfMvv-_M0PCWyXJ4lKZHHhWVQAD9dhTc9Eqqpy9jdrTjTR76P67wFzP4me6CVXI9tVRC1xb82ccPg4RsRu-UfEu0B87sg6pcjc4k6fp9_2YV02dLhA52rnP-19gCEPkF5SYTex2wWxzdoHwXgAaHxO4HWc4Mru_x4Pu5iLLGJ6c13Nq_t3YbsrTuAb11FV5F2IlHDBmIcqJKf0PanrWVuORyQyZuOgRaspgVsHr8nQNzHf81DiB5Fy4sa9MubRzEZvo_HEd-KcnTlo0_-WhI5gComAR-fM9hIKc5zZvLd9CO84asSg' },
  form: 
   { grant_type: 'refresh_token',
     client_id: 'urn:mace:oidc:hotschedules.com',
     refresh_token: 'eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJhWnRINE56ejBGZURjMU1FSkIyU2lIeHhGS0xuLXQtVm1DUHBHeUVnS09BIn0.eyJqdGkiOiJmNGQwNjQyOC1jNzIzLTQ0YWYtOTRmYS00MGI2MGQ3MWQxMmQiLCJleHAiOjE1MDMzNzA4MzQsIm5iZiI6MCwiaWF0IjoxNTAzMzY5MDM0LCJpc3MiOiJodHRwczovL2xvZ2luLmJvZGhpLWRldi5pby9hdXRoL3JlYWxtcy9ob3RzY2hlZHVsZXMiLCJhdWQiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJzdWIiOiI3NDE4MjRhYy0zMjlkLTQ4OTAtYTRmNi0zMmJmMTBiNjJhMjEiLCJ0eXAiOiJSZWZyZXNoIiwiYXpwIjoidXJuOm1hY2U6b2lkYzpob3RzY2hlZHVsZXMuY29tIiwiYXV0aF90aW1lIjowLCJzZXNzaW9uX3N0YXRlIjoiMGE4MTQzYjktNmMzNC00ZTcxLWI4YWMtZjkyNDRjZjJhZjgyIiwiY2xpZW50X3Nlc3Npb24iOiJlMDgxNDBkNi1lODVlLTQzOGQtYmZjYi03ODY2YmFkZTlkODMiLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsiYWRtaW4iLCJ1bWFfYXV0aG9yaXphdGlvbiIsInVzZXIiXX0sInJlc291cmNlX2FjY2VzcyI6eyJyZWFsbS1tYW5hZ2VtZW50Ijp7InJvbGVzIjpbIm1hbmFnZS11c2VycyJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsInZpZXctcHJvZmlsZSJdfX19.QifLXuXYanmKlh8fDpLqurhb1S3hpEVwObUWcfMvv-_M0PCWyXJ4lKZHHhWVQAD9dhTc9Eqqpy9jdrTjTR76P67wFzP4me6CVXI9tVRC1xb82ccPg4RsRu-UfEu0B87sg6pcjc4k6fp9_2YV02dLhA52rnP-19gCEPkF5SYTex2wWxzdoHwXgAaHxO4HWc4Mru_x4Pu5iLLGJ6c13Nq_t3YbsrTuAb11FV5F2IlHDBmIcqJKf0PanrWVuORyQyZuOgRaspgVsHr8nQNzHf81DiB5Fy4sa9MubRzEZvo_HEd-KcnTlo0_-WhI5gComAR-fM9hIKc5zZvLd9CO84asSg' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```


>**Sample Results**


```
{
    "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJhWnRINE56ejBGZURjMU1FSkIyU2lIeHhGS0xuLXQtVm1DUHBHeUVnS09BIn0.eyJqdGkiOiI3NmM1YjIyMC03NjQxLTRhYzctYTA5NS02ZjU4NWY0ZGE1MzIiLCJleHAiOjE1MDM0NzU3MzYsIm5iZiI6MCwiaWF0IjoxNTAzMzY3NzM2LCJpc3MiOiJodHRwczovL2xvZ2luLmJvZGhpLWRldi5pby9hdXRoL3JlYWxtcy9ob3RzY2hlZHVsZXMiLCJhdWQiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJzdWIiOiI3NDE4MjRhYy0zMjlkLTQ4OTAtYTRmNi0zMmJmMTBiNjJhMjEiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiI4YjdkNTc2Ny04MTYyLTQyMTgtODVmNi1hMzRjYTY5ZDVkNGQiLCJhY3IiOiIxIiwiY2xpZW50X3Nlc3Npb24iOiIwYzVlMDc3Zi0yNzBjLTQ0YWUtOTllNS00ZmQwMzkyOTM4YjciLCJhbGxvd2VkLW9yaWdpbnMiOltdLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsiYWRtaW4iLCJ1bWFfYXV0aG9yaXphdGlvbiIsInVzZXIiXX0sInJlc291cmNlX2FjY2VzcyI6eyJyZWFsbS1tYW5hZ2VtZW50Ijp7InJvbGVzIjpbIm1hbmFnZS11c2VycyJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsInZpZXctcHJvZmlsZSJdfX0sInByZWZlcnJlZF91c2VybmFtZSI6InRyYXZpc2pvaG5zb25teGRldiJ9.U7YARFPbRJVHzPdQfXIvsUneZe44AQdBcR5JR8rqC8h2lFO1LkGfsO-yrLGYsnjzroJg3cJ8XD9yJOY7sLNSTAKX3FTKpBViQ2LrOlcyR4eNQrl3dfM6hVSQHAgwItJ3wSsTQk2feCj0jIj69JmT63mjkOGsBCfhO8lRvWGmVUHm3eXw4F1_h-KATKEGi4xjLgD5GoRn30FZ1BYn-7GQBgU-sAxge_dr0IQe2f8PjIqNSEKfv01NMmn4LpKjNRUiTZbb-pe1AK0j7yy6mf0reduKUTXp0S51QGuaG2Qe9uokYyfLhHuu6bja7OQ7ax8uYlpwVTF8xKpNhosDBmHw2A",
    "expires_in": 108000,
    "refresh_expires_in": 1800,
    "refresh_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJhWnRINE56ejBGZURjMU1FSkIyU2lIeHhGS0xuLXQtVm1DUHBHeUVnS09BIn0.eyJqdGkiOiJhYzcxOWI1Ny04OTA2LTRkMDYtYmU5My1mNDM3ZjM4M2M2M2IiLCJleHAiOjE1MDMzNjk1MzYsIm5iZiI6MCwiaWF0IjoxNTAzMzY3NzM2LCJpc3MiOiJodHRwczovL2xvZ2luLmJvZGhpLWRldi5pby9hdXRoL3JlYWxtcy9ob3RzY2hlZHVsZXMiLCJhdWQiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJzdWIiOiI3NDE4MjRhYy0zMjlkLTQ4OTAtYTRmNi0zMmJmMTBiNjJhMjEiLCJ0eXAiOiJSZWZyZXNoIiwiYXpwIjoidXJuOm1hY2U6b2lkYzpob3RzY2hlZHVsZXMuY29tIiwiYXV0aF90aW1lIjowLCJzZXNzaW9uX3N0YXRlIjoiOGI3ZDU3NjctODE2Mi00MjE4LTg1ZjYtYTM0Y2E2OWQ1ZDRkIiwiY2xpZW50X3Nlc3Npb24iOiIwYzVlMDc3Zi0yNzBjLTQ0YWUtOTllNS00ZmQwMzkyOTM4YjciLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsiYWRtaW4iLCJ1bWFfYXV0aG9yaXphdGlvbiIsInVzZXIiXX0sInJlc291cmNlX2FjY2VzcyI6eyJyZWFsbS1tYW5hZ2VtZW50Ijp7InJvbGVzIjpbIm1hbmFnZS11c2VycyJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsInZpZXctcHJvZmlsZSJdfX19.VPD0wzTwpyXoqVoax0FWT53PznjDLsARUPyBKsqR7e5PAv5_hpMKdPVYqVQh0bKJWpV5XDSgISyJjg4lbvW7Zb-jG7Q-bAS3vT5jfp_WE_JoPqKzgdp-oq463hVPD_vPL_UzpXH5uX1gN2x2rgt7IOU7_uYFK0preUCOsBGG_ioDLyHLZ9_0BizNc59Tzdjv5gQHammDF2jbHG2g3XurLqVbGtEjGEwkO5Zax02YfslOaOHuff_litJsw9QlN7MIFEMDRpwPT3H2hQkVpQw7Du_Sd6XZxU0BQmK599wb5D7zn2O7wlpNQcxGl1U1CA7Dqnrqn6YoVpOske8nz-qpmg",
    "token_type": "bearer",
    "id_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJhWnRINE56ejBGZURjMU1FSkIyU2lIeHhGS0xuLXQtVm1DUHBHeUVnS09BIn0.eyJqdGkiOiJjMTNkYzk4My1kZjQ1LTQ1MjgtYWEwMi1hZTIzZGUzYzhkNzYiLCJleHAiOjE1MDM0NzU3MzYsIm5iZiI6MCwiaWF0IjoxNTAzMzY3NzM2LCJpc3MiOiJodHRwczovL2xvZ2luLmJvZGhpLWRldi5pby9hdXRoL3JlYWxtcy9ob3RzY2hlZHVsZXMiLCJhdWQiOiJ1cm46bWFjZTpvaWRjOmhvdHNjaGVkdWxlcy5jb20iLCJzdWIiOiI3NDE4MjRhYy0zMjlkLTQ4OTAtYTRmNi0zMmJmMTBiNjJhMjEiLCJ0eXAiOiJJRCIsImF6cCI6InVybjptYWNlOm9pZGM6aG90c2NoZWR1bGVzLmNvbSIsImF1dGhfdGltZSI6MCwic2Vzc2lvbl9zdGF0ZSI6IjhiN2Q1NzY3LTgxNjItNDIxOC04NWY2LWEzNGNhNjlkNWQ0ZCIsImFjciI6IjEiLCJvdGhlckNsYWltcyI6eyJib2RoaWFwaSI6InRyYXZpc2pvaG5zb25teGRldiJ9LCJwcmVmZXJyZWRfdXNlcm5hbWUiOiJ0cmF2aXNqb2huc29ubXhkZXYifQ.jMRuuajwcXKdPV1NR-Ba38PWs55ES0Ff-LmMdEsVhC3ftD8__uIKOY1lBlT7ZS_b7P92h4yHTGzx6_RBS2GXEX6qSocltbY8ETVpS0uVPNShQD4EenKBXSgWtvkCvYASKUooOCfO_D7UgwdsXqojgsTR6j9fS10rA3FO_ewQGvimYvUwqpdQr844TSpPGvxmMZj4lvXPGXD77R8GyuZxOyKM2kM5vj2DFO8YZeI7dO0o3XKp2ccRnDSq0SI38sVO9mBcRcdfm6Z8gaiACS__39w3YtP6JfZMALUxfIDdYPG9Ttz264vUwrKGa25ckbzCDqUYJ4zazVrneglC6FzysA",
    "not-before-policy": 0,
    "session_state": "8b7d5767-8162-4218-85f6-a34ca69d5d4d"
}
```


Now that you've authenticated to the API, let's look at some data.

##Making a call
The HotSchedules REST API supports all the standard REST verbs  
**GET**  
**POST**  
**PUT**  
**PATCH**  
**DELETE**  

You can access these verbs for each of the types in the HotSchedules system. When an organization is created in the HotSchedules Platform, the organization automatically gets 32 'types' that will store standard information and data about your organization. Those 'types' can be viewed and reviewed at `https://api.bodhi.space/apidocs/index.html`

####GET
As an example, let's do a **GET** on a store via CURL
`curl -ik --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=platform" -X GET https://api.bodhi.space/bodhi-social/resources/Store`

This call will return the information about a store that's been created for the bodhi-social organization
    
`[{"sys_version":1,"image_url":"https://upload.wikimedia.org/wikipedia/commons/5/54/Golden_Gate_Bridge_0002.jpg","sys_type_version":12,"address":{"street_address":"555 Mission","extended_address":"","locality":"San Francisco","region":"CA","postal_code":"94111","country":"US"},"store_hours":[{"days":[7,1],"start":"0500","end":"0000"},{"days":[1,2],"start":"1200","end":"0200"},{"days":[2,3],"start":"1200","end":"0200"},{"days":[3,4],"start":"1200","end":"0200"},{"days":[4,5],"start":"1200","end":"0200"},{"days":[5,6],"start":"1200","end":"0200"},{"days":[6,7],"start":"0500","end":"0000"}],"sys_created_by":"admin__bodhi-social","sys_created_at":"2016-05-21T15:37:15.560Z","name":"platformstore","store_number":"1","display_name":"Platform Store","sys_id":"574080abb9a19e2dadee775b"}]`

You can also get the JSON payload by navigating directly to this URL `https://api.bodhi.space/bodhi-social/resources/Store`  

You can create your own store for your organization either by executing a **POST** command (see below) to `https://api.bodhi.space/<organization_name>/resources/Store` or using our free store manager tool at `https://bodhi.space/store-manager` . Either way, a store is a critical anchor for information in the Platform.

Next let's look up a sale for our store in bodhi-social

`curl -ik --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=platform" -X GET https://api.bodhi.space/bodhi-social/resources/SalesTransaction`

RESULT:

`[{"order_number":10184,"item_count":1,"store_id":"574080abb9a19e2dadee775b","employee":{"id":"5151","name":"Ted Morrison"},"business_day":"2016-05-20","revenue_center":{"id":"2","name":"Restaraunt"},"type":{"id":"4","name":"1"},"timestamp":"2016-05-21T03:34:00.000Z","transaction_id":"557605fc4c32e071180a46042016-05-2010184","net_total":{"value":325,"code":"USD","scale":2},"discount_total":{"value":0,"code":"USD","scale":2},"tax_total":{"value":23,"code":"USD","scale":2},"gross_total":{"value":348,"code":"USD","scale":2},"tender_total":{"value":348,"code":"USD","scale":2},"order_opened_at":"2016-05-21T03:33:00.000Z","order_closed_at":"2016-05-21T03:34:00.000Z","guest_count":1,"sys_version":1,"sys_created_at":"2016-05-21T16:02:30.800Z","sys_created_by":"admin__bodhi-social","sys_type_version":12,"sys_id":"574086965eacd06aa3db036b"}]`

We can also look up our Store using query parameters in our URL

`curl --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=platform" 'https://api.bodhi.space.io/bodhi-social/resources/SalesTransaction?where=%7Bbusiness_day:"2016-05-20"%7D&fields=business_day'`

OR alternatively:

`curl -g --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=platform" 'https://api.bodhi.space/bodhi-social/resources/SalesTransaction?where={business_day:"2016-05-20"}&fields=business_day'`

RESULT:    
`[{"order_number":10184,"item_count":1,"store_id":"574080abb9a19e2dadee775b","employee":{"id":"5151","name":"Ted Morrison"},"business_day":"2016-05-20","revenue_center":{"id":"2","name":"Restaraunt"},"type":{"id":"4","name":"1"},"timestamp":"2016-05-21T03:34:00.000Z","transaction_id":"557605fc4c32e071180a46042016-05-2010184","net_total":{"value":325,"code":"USD","scale":2},"discount_total":{"value":0,"code":"USD","scale":2},"tax_total":{"value":23,"code":"USD","scale":2},"gross_total":{"value":348,"code":"USD","scale":2},"tender_total":{"value":348,"code":"USD","scale":2},"order_opened_at":"2016-05-21T03:33:00.000Z","order_closed_at":"2016-05-21T03:34:00.000Z","guest_count":1,"sys_version":1,"sys_created_at":"2016-05-21T16:02:30.800Z","sys_created_by":"admin__bodhi-social","sys_type_version":12,"sys_id":"574086965eacd06aa3db036b"}]`

So `https://api.bodhi.space/bodhi-social/resources/SalesTransaction?where={%27business_day%27:%272016-05-20%27}` would return all SalesTransaction's for the business day of 2016-05-20.
The URL `https://api.bodhi.space/bodhi-social/resources/SalesTransaction?where={%27store_id%27:%27574080abb9a19e2dadee775b%27}` would return all SalesTransaction's for the store 574080abb9a19e2dadee775b (our Platform test store).

All Types can be queried by any parameter within the type using a ?where={} clause. It's **EXTREMELY** important for efficiency and performance to query using indexes on your types. You can review the Types for your organization as well as the Indexes and Parameters by using our free Type Tool located at `https://tools.bodhi.space/types` or by inspecting `https://api.bodhi.space/<organization_name>/resources/BodhiType`

####POST
To **POST** to a type you need to add the the header: 'Content-Type: application/json' to your cURL Command

`curl -ik -H 'Content-Type: application/json' --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=foo" -X POST -d '{
  "store_id": "l8zeL",
  "business_day": "2016-05-13",
  "timestamp": "2016-05-12T05:58:31.296Z",
  "transaction_id": "FGHG012",
     "tender_total": {
      "code": "USD",
      "scale": 2,
      "value": 620
    }
}' https://api.bodhi.space/<organization_name>/resources/SalesTransaction`

That command will post the json object to the SalesTransaction type. You can now GET on this type either using cURL or the free query tools available at https://tools.bodhi.space/query

####Bulk Post
All bulk operations are accessible through https://api.bodhi.space  
The size limitation for the body is 17MB  

###Syntax: 
**POST** `/<organization_name>/bulk` with json body  
```{
	"config": {
		"op": "insert" or "update" or "upsert" or "invite",  * see below
		 "report": true,				<- optional, need a report? (default false) 
		 "target": "target_name”		<- the name of the type (not for invite)
	},
	"payload": [{
		"the_field": "my first thing to insert or upsert or invite",
		"other_field": "the_other_field"
	}, {
		"the_field": "my second thing to insert or upsert",
		"other_field": "the_other_field2"
	}]
}```  

The payload varies depending on the type of operation and Returns 202 with header `bulk_id:<the bulk id>`

The result of a report, if requested, is accessible as soon as the processing is done on:

**GET** `/<organization_name>/bulk/<bulk_id>`

**RESPONSE:**  
returns **200** with a json array body where the order of the cells matches the order of the payload. The report can be accessed only once.  
returns **204** if the report is not ready yet  
returns **404** if no report was found with that id  

  * update/upsert is only available for types not encapsulated 
  * insert on system types only BodhiUser, BodhiType and BodhiEnumeration and any not encapsulated type

###Example:
```{
	"config": {
		"op": "insert",
		"report": true,
		"target":  "BulkTest"
	},
	"payload": [{
		"name": "leo",
		"other_field": "mauris non"
	}, {
		"name": "orci",
		"other_field": "sit amet justo"
	}, {
		"name": "nulla",
		"other_field": "pulvinar sed nisl nunc rhoncus"
	}, {
		"name": "nulla",
		"other_field": "diam cras"
	}, {
		"name": "est",
		"other_field": "dui nec nisi volutpat"
	}, {
		"name": "lorem",
		"other_field": "cursus id"
	}, {
		"name": "molestie",
		"other_field": "potenti nullam porttitor lacus at"
	}, {
		"name": "sapien",
		"other_field": "ultrices aliquet maecenas leo"
	}, {
		"name": "nibh",
		"other_field": "consectetuer eget rutrum at"
	}, {
		"name": "luctus",
		"other_field": "nisl nunc"
	}]
}```

####PUT
The HTTP verb PUT can be used on any type as long as there's a unique index on the field or fields. You can always PUT on sys_id

As an example, in the above SalesTransaction example, the sys_id is 574086965eacd06aa3db036b, a PUT to the SalesTransaction based on sys_id would be as follows:

`
curl -ik -H 'Content-Type: application/json' --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=foo" -X PUT -d '{ "store_id": "l8zeL", "business_day": "2016-05-13", "timestamp": "2016-05-12T05:58:31.296Z", "transaction_id": "FGHG012", "tender_total": { "code": "USD", "scale": 2, "value": 620 } }' https://api.bodhi.space/tutorial/resources/SalesTransaction/574086965eacd06aa3db036b
` 

####PUT Upsert
Upsert is a safe way to replace an existing record, or POST a record if the entry does not currently exist.

You can upsert by appending your URL with ?upsert=true

As an example, the above PUT example can be changed to a replace by appending the ?upsert=true to the cURL command:

`
curl -ik -H 'Content-Type: application/json' --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=foo" -X PUT -d '{ "store_id": "l8zeL", "business_day": "2016-05-13", "timestamp": "2016-05-12T05:58:31.296Z", "transaction_id": "FGHG012", "tender_total": { "code": "USD", "scale": 2, "value": 620 } }' https://api.bodhi.space/tutorial/resources/SalesTransaction/574086965eacd06aa3db036b?upsert=true
`


####PATCH
the HTTP verb PATCH will allow you to alter single parameters or fields within a record in your type. Patch commands follow the following sytax:
[ { "op": "replace", "path": "/baz", "value": "boo" }, { "op": "add", "path": "/hello", "value": ["world"] }, { "op": "remove", "path": "/foo"} ]

The HTTP verb PATCH can be used on any type as long as there's a unique index on the field or fields. You can always PATCH on sys_id

####DELETE
the HTTP verb DELETE will allow you to remove a record in your type. DELETE commands follow the following sytax:

To delete multiple records, include a ?where={} in your URL to narrow or expand then number of records removed.

####File Upload
The Platform BodhiFileUpload endpoints are special types that allow a user to upload and download any file (like a dbf file from your store's POS).

Metadata of your file is posted to type BodhiFileUpload on successful upload  

**BodhiFileUpload example record:**  
`{ "namespace": "bodhi", "original_name": "profile_pic5.jpg", "sys_version": 1, "location": "bodhi/profile_pic5.jpg", "uploaded_at": "2015-09-10T19:42:48+0000", "sys_created_by": "admin__bodhi", "sys_created_at": "2015-09-10T19:42:49+0000", "name": "profile_pic5.jpg", "media_type": "image/jpeg", "sys_id": "55f1dd39b9b5904f64c8212f" }`

**Examples:**  
The following are curl examples of how to specify file location in your upload/download/delete commands.  Everything after “upload/” or “download/” in the url is used as the destination.  Note that filename is always specified in the url.  

`curl -X POST -u <username>:<password> https://api.bodhi.space/<organization_name>/controllers/vertx/upload/recipes/food/BurritoRecipe.txt -F "upload1=@THE_FILE"`  

`curl -X PUT -u <username>:<password> https://api.bodhi.space/<organization_name>/controllers/vertx/upload/recipes/food/BurritoRecipe.txt -F "upload1=@THE_FILE"`

**Download by path:**  
`curl -X GET -u <username>:<password> https://api.bodhi.space/<organization_name>/controllers/vertx/download/recipes/food/BurritoRecipe.txt`

**Download by sys_id:**  
`curl -X GET -u <username>:<password> https://api.bodhi.space/<organization_name>/controllers/vertx/download/56f9c2b4fa92ec27934a76ae`  

**Delete a file:**  
`curl -X DELETE -u <username>:<password> https://api.bodhi.space/<organization_name>/controllers/vertx/upload/recipes/food/BurritoRecipe.txt`

