# Innohub Rest API

### Table of Contents
**[Authorization](#authorization)**<br>
**[Routes](#routes)**<br>
  **[Authentication](#authentication)**<br>
**[File Preprocesser](#file-preprocesser)**<br>
**[Uploads](#uploads)**<br>
**[Integrations](#integrations)**<br>
**[Jobs](#jobs)**<br>
**[Social Share](#social-share)**<br>



## Authorization

### Usage

By default middleware tries to find the token from `Authorization` header. You can authorize each requests by setting
your `Authorization` header value.

`authorization` header = `Bearer (token value)`
> Noteworthy: `[{token: value}]` is created after creating a new account

> Noteworthy: `[{token: value}]` can be used as a session to retrieve user details

> Noteworthy: `[{token: value}]` is a `long string`

## Routes

### Authentication

#### New Member (Create Account)

`POST Request`

```
Endpoint   /api/v1/auth/create
```

```
Payload
{
	"email": "some&emailaddress.com",
	"name": "John Kensel",
	"password": "somestrongpassword"
}
```

Success Response

```
{
    "status": "success",
    "response": {
        "email": "some&emailaddress.com",
        "name": "John Kensel",
        "id": "1",
        "image": "default",
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczpcL1wvcG9ydGFsLmlubm90ZWNoY29uc3RydW",
        "expiration": "1555636671",
        "updated": "2019-04-04 01:17:51",
        "created": "2019-04-04 01:17:51"
    },
    "code": "200"
}
```

Account Exist

```
{
    "status": "error",
    "message": "email exist",
    "code": "401"
}
```

Invalid Payload

```
{
    "status": "error",
    "message": "Bad Request",
    "code": "401"
}
```

#### Sign In

`PUT Request`

```
Endpoint   /api/v1/auth/signin
```

```
Payload
{
	"email": "some&emailaddress.com",
	"password": "somestrongpassword"
}
```

Success Response

```
{
    "status": "success",
    "response": {
        "id": "1",
        "name": "John Kensel",
        "shares": "0",
        "status": "Active",
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.9uc3RydWN0aW9uLmNvbSIsImlh",
        "expiration": "1555636671",
        "email": "some@email.com",
        "image": "default",
        "updated": "2019-04-04 01:17:51.000000",
        "created": "2019-04-04 01:17:51.000000"
    },
    "code": "200"
}
```

Invalid Credentials

```
{
    "status": "error",
    "message": "Sign in error, Invalid credentials",
    "code": "401"
}
```

Invalid Payload

```
{
    "status": "error",
    "message": "Bad Request",
    "code": "401"
}
```

#### Account Recovery

`PUT Request`

```
Endpoint   /api/v1/auth/recovery
```

```
Payload
{
	"email": "some@emailaddress.com"
}
```

Success Response

```
{
    "status": "success",
    "message": "Recovery mail sent",
    "code": "200"
}
```

Invalid Credentials

```
{
    "status": "error",
    "message": "Recovery error, Invalid credentials",
    "code": "401"
}
```

Invalid Payload

```
{
    "status": "error",
    "message": "Bad Request",
    "code": "401"
}
```

##### Update Recovery Password

`PUT Request`

```
Endpoint   /api/v1/auth/recovery/update
```

```
Payload
{
	"code": "Recovery code sent to your mail",
	"email": "some@emailaddress.com",
	"password": "some new strong password"
}
```

Success Response

```
{
    "status": "success",
    "message": "Password Updated",
    "code": "200"
}
```

Invalid Credentials

```
{
    "status": "error",
    "message": "Invalid Reset Code",
    "code": "401"
}
```

Invalid Payload

```
{
    "status": "error",
    "message": "Bad Request",
    "code": "401"
}
```


#### File Preprocesser
> Hint: used to retrieve files from server

`GET Request`

```
Endpoint   /api/v1/preprocessor/file[/{id}/{type}/{data}]
```
> user id `id`: `integer`

> request type `type`: `string` eg profile

> name of file `data`: `string`

> example url `/api/v1/preprocessor/file/1/profile/a.png`


#### Uploads
> Hint: upload files to server

`POST Request`

```
Endpoint   /api/v1/uploads
```
> Important Note: append object to payload: `{ url: id + '/profile/', name: 'index'}`

> user id `id`: `integer`

> type `profile`: `string`

> file `name`: `string`

> example object 
`{ 
	url: 1003 + '/profile/', 
	name: 'index'
}`


#### Uploads Alternative
> Hint: convert images to base64 to store in database

`POST Request`

```
Endpoint   /api/v1/converters
```
> Important Note: append object to payload: `{ url: id + '/profile/' }`

> user id `id`: `integer`

> type `profile`: `string`

> example object 
`{ 
	url: 1003 + '/profile/'
}`

### Integrations
#### Get Status
`GET Request`

```
Endpoint   /api/v1/integrations/status/[{userid}]
```

> Noteworthy: `[{id}]` accepts `integer` eg: 1003

Response

```
{
    "status": "success",
    "response": [
        {
            "id": "1",
            "user": "1",
            "facebook": "Not Available",
            "linkedin": "Not Available",
            "twitter": "Not Available",
            "updated": "2019-04-04 02:45:49.000000"
        }
    ],
    "code": "200"
}
```

### Jobs

#### New Company (Create Account)

`POST Request`

```
Endpoint   /api/v1/jobs/create/company
```

```
Payload
{
	"name": "Menzvic Limited",
	"user": "1001",
	"location": "Prescott Arizona"
}
```

Success Response

```
{
    "status": "success",
    "response": {
        "name": "Menzvic Limited",
        "user": "1001",
        "location": "Prescott Arizona",
        "id": "1000",
        "logo": "default",
        "updated": "2019-04-04 13:38:42",
        "created": "2019-04-04 13:38:42"
    },
    "code": "200"
}
```

Company Exists

```
{
    "status": "error",
    "message": "Company profile exists",
    "code": "401"
}
```

Invalid Payload

```
{
    "status": "error",
    "message": "Bad Request",
    "code": "401"
}
```

#### New Job posting

`POST Request`

```
Endpoint   /api/v1/jobs/create/job
```

```
Payload
{
	"title": "Nuxtjs Developer",
	"description": "Collaborate with our team in every stage of a product's lifecycle",
	"location": "San Jose",
	"closeDate": "2019-04-04 13:38:42.000000",
	"company": "1000"
}
```

Success Response

```
{
    "status": "success",
    "response": {
        "title": "Nuxtjs Developer",
        "description": "Collaborate with our team in every stage of a product's lifecycle",
        "location": "San Jose",
        "closeDate": "2019-04-04 13:38:42.000000",
        "company": "1000",
        "id": "1",
        "updated": "2019-04-05 18:01:43",
        "created": "2019-04-05 18:01:43"
    },
    "code": "200"
}
```

Job Posting Exists

```
{
    "status": "error",
    "message": "Job posting exists",
    "code": "401"
}
```

Invalid Payload

```
{
    "status": "error",
    "message": "Bad Request",
    "code": "401"
}
```

#### Get all job postings

`GET Request`

```
Endpoint   /api/v1/jobs/query/all
```
Response

```
{
    "status": "success",
    "response": [
        {
            "id": "1000",
            "company": "1000",
            "title": "Nuxtjs Developer",
            "description": "Collaborate with our team in every stage of a product's lifecycle",
            "closeDate": "2019-04-04 13:38:42.000000",
            "location": "Prescott Arizona",
            "created": "2019-04-05 17:21:04.000000",
            "updated": "2019-04-05 17:21:04.000000",
            "user": "1",
            "name": "Menzvic Limited",
            "logo": "default"
        },
        {
            "id": "1000",
            "company": "1000",
            "title": "Reactjs Developer",
            "description": "Collaborate with our team in every stage of a product's lifecycle",
            "closeDate": "2019-04-04 13:38:42.000000",
            "location": "Prescott Arizona",
            "created": "2019-04-05 17:21:04.000000",
            "updated": "2019-04-05 17:21:04.000000",
            "user": "1",
            "name": "Menzvic Limited",
            "logo": "default"
        },
        {
            "id": "1000",
            "company": "1000",
            "title": "Business Manager",
            "description": "Collaborate with our team in every stage of a product's lifecycle",
            "closeDate": "2019-04-04 13:38:42.000000",
            "location": "Prescott Arizona",
            "created": "2019-04-05 17:21:04.000000",
            "updated": "2019-04-05 17:21:04.000000",
            "user": "1",
            "name": "Menzvic Limited",
            "logo": "default"
        }
    ],
    "code": "200"
}
```

#### Get all company postings

`GET Request`

```
Endpoint   /api/v1/jobs/query/company/[{company-id}]
```
Response

```
{
    "status": "success",
    "response": [
        {
            "id": "1001",
            "company": "1001",
            "title": "Project Manager",
            "description": "Collaborate with our team in every stage of a product's lifecycle",
            "closeDate": "2019-04-05 18:38:42.000000",
            "location": "London, Greater London",
            "created": "2019-04-05 18:10:25.000000",
            "updated": "2019-04-05 18:10:25.000000",
            "user": "2",
            "name": "Kwasivok Developer Services",
            "logo": "default"
        },
        {
            "id": "1001",
            "company": "1001",
            "title": "UI/UX Designer",
            "description": "Collaborate with our team in every stage of a product's lifecycle",
            "closeDate": "2019-04-05 18:38:42.000000",
            "location": "London, Greater London",
            "created": "2019-04-05 18:10:25.000000",
            "updated": "2019-04-05 18:10:25.000000",
            "user": "2",
            "name": "Kwasivok Developer Services",
            "logo": "default"
        },
        {
            "id": "1001",
            "company": "1001",
            "title": "Growth Hacker",
            "description": "Collaborate with our team in every stage of a product's lifecycle",
            "closeDate": "2019-04-05 18:38:42.000000",
            "location": "London, Greater London",
            "created": "2019-04-05 18:10:25.000000",
            "updated": "2019-04-05 18:10:25.000000",
            "user": "2",
            "name": "Kwasivok Developer Services",
            "logo": "default"
        }
    ],
    "code": "200"
}
```

#### Get open positions for a company

`GET Request`

```
Endpoint   /api/v1/jobs/query/positions/[{company-id}]
```
Response

```
{
    "status": "success",
    "response": {
        "positions": 3
    },
    "code": "200"
}
```

### Social Share
> Note: Social share can only be effectively implemented in the frontend

> Disclaimer: The below code may work effectively or not depending on the stack (framework)
> you use to code your frontend

#### First Option
Copy the below snippet and insert it right before the closing body tag on every page you want
``<script src=“//platform-api.sharethis.com/js/sharethis.js#property=5ca785209b272f00119abe29&product=inline-share-buttons”></script>``

Copy and paste the code below wherever you'd like the buttons to appear
`` <div class="sharethis-inline-share-buttons"></div> ``
You can add it to a loop and it will create a new instance every time it iterates, automatically binding it to the corresponding elements. auto count will work defaultly for each listing.

#### Second Option


