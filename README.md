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

#### First Option (Easy Option)
Copy the below snippet and insert it right before the closing body tag on every page you want

```<script src=“//platform-api.sharethis.com/js/sharethis.js#property=5ca785209b272f00119abe29&product=inline-share-buttons”></script>```

Copy and paste the code below wherever you'd like the buttons to appear

``` <div class="sharethis-inline-share-buttons"></div> ```

You can add it to a loop and it will create a new instance every time it iterates, automatically binding it to the corresponding elements. auto count will work defaultly for each listing.

#### Second Option (Recommended Option)

Copy and paste the code below wherever you'd like the buttons to appear, best practice will be to create a component for it.

Available integrations are
> facebook, twitter, google, tumblr, email, and pinterest

Sharing button Facebook

```
<a class="resp-sharing-button__link" href="https://facebook.com/sharer/sharer.php?u=http%3A%2F%2Fsharingbuttons.io" target="_blank" rel="noopener" aria-label="">
  <div class="resp-sharing-button resp-sharing-button--facebook resp-sharing-button--small"><div aria-hidden="true" class="resp-sharing-button__icon resp-sharing-button__icon--solid">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M18.77 7.46H14.5v-1.9c0-.9.6-1.1 1-1.1h3V.5h-4.33C10.24.5 9.5 3.44 9.5 5.32v2.15h-3v4h3v12h5v-12h3.85l.42-4z"/></svg>
    </div>
  </div>
</a>
```

Sharing button Twitter

```
<a class="resp-sharing-button__link" href="https://twitter.com/intent/tweet/?text=Super%20fast%20and%20easy%20Social%20Media%20Sharing%20Buttons.%20No%20JavaScript.%20No%20tracking.&amp;url=http%3A%2F%2Fsharingbuttons.io" target="_blank" rel="noopener" aria-label="">
  <div class="resp-sharing-button resp-sharing-button--twitter resp-sharing-button--small"><div aria-hidden="true" class="resp-sharing-button__icon resp-sharing-button__icon--solid">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M23.44 4.83c-.8.37-1.5.38-2.22.02.93-.56.98-.96 1.32-2.02-.88.52-1.86.9-2.9 1.1-.82-.88-2-1.43-3.3-1.43-2.5 0-4.55 2.04-4.55 4.54 0 .36.03.7.1 1.04-3.77-.2-7.12-2-9.36-4.75-.4.67-.6 1.45-.6 2.3 0 1.56.8 2.95 2 3.77-.74-.03-1.44-.23-2.05-.57v.06c0 2.2 1.56 4.03 3.64 4.44-.67.2-1.37.2-2.06.08.58 1.8 2.26 3.12 4.25 3.16C5.78 18.1 3.37 18.74 1 18.46c2 1.3 4.4 2.04 6.97 2.04 8.35 0 12.92-6.92 12.92-12.93 0-.2 0-.4-.02-.6.9-.63 1.96-1.22 2.56-2.14z"/></svg>
    </div>
  </div>
</a>
```
Sharing button LinkedIn

```
<a class="resp-sharing-button__link" href="https://www.linkedin.com/shareArticle?mini=true&amp;url=http%3A%2F%2Fsharingbuttons.io&amp;title=Super%20fast%20and%20easy%20Social%20Media%20Sharing%20Buttons.%20No%20JavaScript.%20No%20tracking.&amp;summary=Super%20fast%20and%20easy%20Social%20Media%20Sharing%20Buttons.%20No%20JavaScript.%20No%20tracking.&amp;source=http%3A%2F%2Fsharingbuttons.io" target="_blank" rel="noopener" aria-label="">
  <div class="resp-sharing-button resp-sharing-button--linkedin resp-sharing-button--small"><div aria-hidden="true" class="resp-sharing-button__icon resp-sharing-button__icon--solid">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M6.5 21.5h-5v-13h5v13zM4 6.5C2.5 6.5 1.5 5.3 1.5 4s1-2.4 2.5-2.4c1.6 0 2.5 1 2.6 2.5 0 1.4-1 2.5-2.6 2.5zm11.5 6c-1 0-2 1-2 2v7h-5v-13h5V10s1.6-1.5 4-1.5c3 0 5 2.2 5 6.3v6.7h-5v-7c0-1-1-2-2-2z"/></svg>
    </div>
  </div>
</a>
```
Sharing button Google+

```
<a class="resp-sharing-button__link" href="https://plus.google.com/share?url=http%3A%2F%2Fsharingbuttons.io" target="_blank" rel="noopener" aria-label="">
  <div class="resp-sharing-button resp-sharing-button--google resp-sharing-button--small"><div aria-hidden="true" class="resp-sharing-button__icon resp-sharing-button__icon--solid">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M11.37 12.93c-.73-.52-1.4-1.27-1.4-1.5 0-.43.03-.63.98-1.37 1.23-.97 1.9-2.23 1.9-3.57 0-1.22-.36-2.3-1-3.05h.5c.1 0 .2-.04.28-.1l1.36-.98c.16-.12.23-.34.17-.54-.07-.2-.25-.33-.46-.33H7.6c-.66 0-1.34.12-2 .35-2.23.76-3.78 2.66-3.78 4.6 0 2.76 2.13 4.85 5 4.9-.07.23-.1.45-.1.66 0 .43.1.83.33 1.22h-.08c-2.72 0-5.17 1.34-6.1 3.32-.25.52-.37 1.04-.37 1.56 0 .5.13.98.38 1.44.6 1.04 1.84 1.86 3.55 2.28.87.23 1.82.34 2.8.34.88 0 1.7-.1 2.5-.34 2.4-.7 3.97-2.48 3.97-4.54 0-1.97-.63-3.15-2.33-4.35zm-7.7 4.5c0-1.42 1.8-2.68 3.9-2.68h.05c.45 0 .9.07 1.3.2l.42.28c.96.66 1.6 1.1 1.77 1.8.05.16.07.33.07.5 0 1.8-1.33 2.7-3.96 2.7-1.98 0-3.54-1.23-3.54-2.8zM5.54 3.9c.33-.38.75-.58 1.23-.58h.05c1.35.05 2.64 1.55 2.88 3.35.14 1.02-.08 1.97-.6 2.55-.32.37-.74.56-1.23.56h-.03c-1.32-.04-2.63-1.6-2.87-3.4-.13-1 .08-1.92.58-2.5zM23.5 9.5h-3v-3h-2v3h-3v2h3v3h2v-3h3"/></svg>
    </div>
  </div>
</a>
```

Sharing button Tumblr

```
<a class="resp-sharing-button__link" href="https://www.tumblr.com/widgets/share/tool?posttype=link&amp;title=Super%20fast%20and%20easy%20Social%20Media%20Sharing%20Buttons.%20No%20JavaScript.%20No%20tracking.&amp;caption=Super%20fast%20and%20easy%20Social%20Media%20Sharing%20Buttons.%20No%20JavaScript.%20No%20tracking.&amp;content=http%3A%2F%2Fsharingbuttons.io&amp;canonicalUrl=http%3A%2F%2Fsharingbuttons.io&amp;shareSource=tumblr_share_button" target="_blank" rel="noopener" aria-label="">
  <div class="resp-sharing-button resp-sharing-button--tumblr resp-sharing-button--small"><div aria-hidden="true" class="resp-sharing-button__icon resp-sharing-button__icon--solid">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M13.5.5v5h5v4h-5V15c0 5 3.5 4.4 6 2.8v4.4c-6.7 3.2-12 0-12-4.2V9.5h-3V6.7c1-.3 2.2-.7 3-1.3.5-.5 1-1.2 1.4-2 .3-.7.6-1.7.7-3h3.8z"/></svg>
    </div>
  </div>
</a>
```

Sharingbutton E-Mail

```
<a class="resp-sharing-button__link" href="mailto:?subject=Super%20fast%20and%20easy%20Social%20Media%20Sharing%20Buttons.%20No%20JavaScript.%20No%20tracking.&amp;body=http%3A%2F%2Fsharingbuttons.io" target="_self" rel="noopener" aria-label="">
  <div class="resp-sharing-button resp-sharing-button--email resp-sharing-button--small"><div aria-hidden="true" class="resp-sharing-button__icon resp-sharing-button__icon--solid">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M22 4H2C.9 4 0 4.9 0 6v12c0 1.1.9 2 2 2h20c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zM7.25 14.43l-3.5 2c-.08.05-.17.07-.25.07-.17 0-.34-.1-.43-.25-.14-.24-.06-.55.18-.68l3.5-2c.24-.14.55-.06.68.18.14.24.06.55-.18.68zm4.75.07c-.1 0-.2-.03-.27-.08l-8.5-5.5c-.23-.15-.3-.46-.15-.7.15-.22.46-.3.7-.14L12 13.4l8.23-5.32c.23-.15.54-.08.7.15.14.23.07.54-.16.7l-8.5 5.5c-.08.04-.17.07-.27.07zm8.93 1.75c-.1.16-.26.25-.43.25-.08 0-.17-.02-.25-.07l-3.5-2c-.24-.13-.32-.44-.18-.68s.44-.32.68-.18l3.5 2c.24.13.32.44.18.68z"/></svg>
    </div>
  </div>
</a>
```

Sharing button Pinterest

```
<a class="resp-sharing-button__link" href="https://pinterest.com/pin/create/button/?url=http%3A%2F%2Fsharingbuttons.io&amp;media=http%3A%2F%2Fsharingbuttons.io&amp;description=Super%20fast%20and%20easy%20Social%20Media%20Sharing%20Buttons.%20No%20JavaScript.%20No%20tracking." target="_blank" rel="noopener" aria-label="">
  <div class="resp-sharing-button resp-sharing-button--pinterest resp-sharing-button--small"><div aria-hidden="true" class="resp-sharing-button__icon resp-sharing-button__icon--solid">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M12.14.5C5.86.5 2.7 5 2.7 8.75c0 2.27.86 4.3 2.7 5.05.3.12.57 0 .66-.33l.27-1.06c.1-.32.06-.44-.2-.73-.52-.62-.86-1.44-.86-2.6 0-3.33 2.5-6.32 6.5-6.32 3.55 0 5.5 2.17 5.5 5.07 0 3.8-1.7 7.02-4.2 7.02-1.37 0-2.4-1.14-2.07-2.54.4-1.68 1.16-3.48 1.16-4.7 0-1.07-.58-1.98-1.78-1.98-1.4 0-2.55 1.47-2.55 3.42 0 1.25.43 2.1.43 2.1l-1.7 7.2c-.5 2.13-.08 4.75-.04 5 .02.17.22.2.3.1.14-.18 1.82-2.26 2.4-4.33.16-.58.93-3.63.93-3.63.45.88 1.8 1.65 3.22 1.65 4.25 0 7.13-3.87 7.13-9.05C20.5 4.15 17.18.5 12.14.5z"/></svg>
    </div>
  </div>
</a>
```

#### CSS for social buttons

> Change it to fit the sizes you want

```
.resp-sharing-button__link,
.resp-sharing-button__icon {
  display: inline-block
}

.resp-sharing-button__link {
  text-decoration: none;
  color: #fff;
  margin: 0.5em
}

.resp-sharing-button {
  border-radius: 5px;
  transition: 25ms ease-out;
  padding: 0.5em 0.75em;
  font-family: Helvetica Neue,Helvetica,Arial,sans-serif
}

.resp-sharing-button__icon svg {
  width: 1em;
  height: 1em;
  margin-right: 0.4em;
  vertical-align: top
}

.resp-sharing-button--small svg {
  margin: 0;
  vertical-align: middle
}

/* Non solid icons get a stroke */
.resp-sharing-button__icon {
  stroke: #fff;
  fill: none
}

/* Solid icons get a fill */
.resp-sharing-button__icon--solid,
.resp-sharing-button__icon--solidcircle {
  fill: #fff;
  stroke: none
}

.resp-sharing-button--twitter {
  background-color: #55acee
}

.resp-sharing-button--twitter:hover {
  background-color: #2795e9
}

.resp-sharing-button--pinterest {
  background-color: #bd081c
}

.resp-sharing-button--pinterest:hover {
  background-color: #8c0615
}

.resp-sharing-button--facebook {
  background-color: #3b5998
}

.resp-sharing-button--facebook:hover {
  background-color: #2d4373
}

.resp-sharing-button--tumblr {
  background-color: #35465C
}

.resp-sharing-button--tumblr:hover {
  background-color: #222d3c
}

.resp-sharing-button--reddit {
  background-color: #5f99cf
}

.resp-sharing-button--reddit:hover {
  background-color: #3a80c1
}

.resp-sharing-button--google {
  background-color: #dd4b39
}

.resp-sharing-button--google:hover {
  background-color: #c23321
}

.resp-sharing-button--linkedin {
  background-color: #0077b5
}

.resp-sharing-button--linkedin:hover {
  background-color: #046293
}

.resp-sharing-button--email {
  background-color: #777
}

.resp-sharing-button--email:hover {
  background-color: #5e5e5e
}

.resp-sharing-button--xing {
  background-color: #1a7576
}

.resp-sharing-button--xing:hover {
  background-color: #114c4c
}

.resp-sharing-button--whatsapp {
  background-color: #25D366
}

.resp-sharing-button--whatsapp:hover {
  background-color: #1da851
}

.resp-sharing-button--hackernews {
background-color: #FF6600
}
.resp-sharing-button--hackernews:hover, .resp-sharing-button--hackernews:focus {   background-color: #FB6200 }

.resp-sharing-button--vk {
  background-color: #507299
}

.resp-sharing-button--vk:hover {
  background-color: #43648c
}

.resp-sharing-button--facebook {
  background-color: #3b5998;
  border-color: #3b5998;
}

.resp-sharing-button--facebook:hover,
.resp-sharing-button--facebook:active {
  background-color: #2d4373;
  border-color: #2d4373;
}

.resp-sharing-button--twitter {
  background-color: #55acee;
  border-color: #55acee;
}

.resp-sharing-button--twitter:hover,
.resp-sharing-button--twitter:active {
  background-color: #2795e9;
  border-color: #2795e9;
}

.resp-sharing-button--google {
  background-color: #dd4b39;
  border-color: #dd4b39;
}

.resp-sharing-button--google:hover,
.resp-sharing-button--google:active {
  background-color: #c23321;
  border-color: #c23321;
}

.resp-sharing-button--tumblr {
  background-color: #35465C;
  border-color: #35465C;
}

.resp-sharing-button--tumblr:hover,
.resp-sharing-button--tumblr:active {
  background-color: #222d3c;
  border-color: #222d3c;
}

.resp-sharing-button--email {
  background-color: #777777;
  border-color: #777777;
}

.resp-sharing-button--email:hover,
.resp-sharing-button--email:active {
  background-color: #5e5e5e;
  border-color: #5e5e5e;
}

.resp-sharing-button--pinterest {
  background-color: #bd081c;
  border-color: #bd081c;
}

.resp-sharing-button--pinterest:hover,
.resp-sharing-button--pinterest:active {
  background-color: #8c0615;
  border-color: #8c0615;
}

.resp-sharing-button--linkedin {
  background-color: #0077b5;
  border-color: #0077b5;
}

.resp-sharing-button--linkedin:hover,
.resp-sharing-button--linkedin:active {
  background-color: #046293;
  border-color: #046293;
}
```

