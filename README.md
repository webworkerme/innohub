## Innohub Rest API

### Authorization

#### Usage

By default middleware tries to find the token from `Authorization` header. You can authorize each requests by setting
your `Authorization` header value.

`authorization` header = `Bearer (token value)`
> Noteworthy: `[{token: value}]` is created after creating a new account

> Noteworthy: `[{token: value}]` can be used as a session to retrieve user details

> Noteworthy: `[{token: value}]` is a `long string`

### Routes

#### Authentication

##### New Member (Create Account)

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

##### Sign In

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

##### Account Recovery

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
