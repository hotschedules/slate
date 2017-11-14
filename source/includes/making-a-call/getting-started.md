#Getting Started

The HotSchedules IoT Platform (Bodhi) REST API allows you to query meta-data about your stores, labor, sales, and HotSchedules Agents running in your stores. You can also do some fancy things like get social information, upload files, send push notifications and emails, and even make payments.

The REST API is served over HTTPS. To ensure data privacy, unencrypted HTTP is not supported.

##IDM - Creating Your Global Profile

Identity Management, or IDM, allows you to sign in to multiple HotSchedules modules with one username and password.  With IDM, you'll have one place to go, and one username and password to access all things HotSchedules.  

_**Please note:**_  With that said, this tool is in its early stages, and does not yet cover ALL HotSchedules modules.  The plan is to incorporate all tools by mid-2018.

For more details on IDM, please click [HERE](https://help.hotschedules.com/hc/en-us/articles/115001464671-IDM-Creating-Your-Global-Profile).


##IDM How to Programatically Retrieve JWT Tokens

Before you can retrieve your token, follow these simple setup steps before proceeding.

**Step 1:** Create your global profile.<br>
**Step 2:** Obtain your API credentials from HotSchedules if you have not already done so.<br>
**Step 3:** Login into the [Account Manager](https://tools.hotschedules.io/account/#/)<br>
**Step 4:** In the upper right corner, select the wrench icon, then keychain, then your namespace.<br>
**Step 5:** Enter your API credentials as provided by hotSchedules and click save.<br>
**Step 6:** Continue with the example below to retrieve your token.



**What are JSON Web Tokens?**

JSON Web Tokens (JWT), pronounced "jot", are a standard since the information they carry is transmitted via JSON.


JSON Web Tokens work across different programming languages: JWTs work in .NET, Python, Node.js, Java, PHP, Ruby, Go, JavaScript, and Haskell. So you can see that these can be used in many different scenarios.


JWTs are self-contained: They will carry all the information necessary within itself. This means that a JWT will be able to transmit basic information about itself, a payload (usually user information), and a signature.


JWTs can be passed around easily: Since JWTs are self-contained, they are perfectly used inside an HTTP header when authenticating an API. You can also pass it through the URL.


**Endpoint**

**Dev:** [https://login.bodhi-dev.io/auth/realms/hotschedules/protocol/openid-connect/token](https://login.bodhi-dev.io/auth/realms/hotschedules/protocol/openid-connect/token)

**Prod:** [https://login.hotschedules.io/auth/realms/hotschedules/protocol/openid-connect/token](https://login.hotschedules.io/auth/realms/hotschedules/protocol/openid-connect/token)

**Header** 

* content-type: application/x-www-form-urlencoded

**Params**

* **grant_type** 
    * Value must be "password" 

* **client_id**
    * Value must be "urn:mace:oidc:hotschedules.com"

* **username** (this is your global profile username)
    * Value should reflect the username of account you’re requesting tokens for

* **password** (this is your global profile password)
    * Value should reflect the password of the account you’re requesting tokens for

**Return**

* access_token

* refresh_token

* id_token

**Sample Call (Postman)**

**Note:** Postman is the free tool used to generate these examples. Download [Postman](https://www.getpostman.com/postman).

![alt text](/images/postman.png?raw=true "Postman")  

>**Sample Call (Curl)**


```
curl -X POST \

  https://login.bodhi-dev.io/auth/realms/hotschedules/protocol/openid-connect/token \

  -H 'cache-control: no-cache' \
  
  -H 'content-type: application/x-www-form-urlencoded' \
  
  -d 'grant_type=password&client_id=urn%3Amace%3Aoidc%3Ahotschedules.com&username=username&password=password'
```

>**Sample Call (Node)**


```
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

*   **grant_type** 
    *   Value must be "refresh_token" 
*   **client_id**
    *   Value must be "urn:mace:oidc:hotschedules.com"
*   **refresh_token**
    *   Value should reflect the refresh token of account you're requesting tokens for

**Return**

*   access_token
*   refresh_token
*   id_token  

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