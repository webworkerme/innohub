## Innohub Rest API

### Authorization

#### Usage

By default middleware tries to find the token from `Authorization` header. You can authorize each requests by setting
your `Authorization` header value.

`authorization` header = `Bearer (token value)`

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
