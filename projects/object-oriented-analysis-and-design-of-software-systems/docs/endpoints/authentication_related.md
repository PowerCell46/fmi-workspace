### Endpoint for registering a user:
A new user wants to join our system.

POST request
request format:
```json
{
    username: "String",
    password: "String"
}
```

We should make sure the username is not taken and that the username and password are valid, according to our validations. Password needs to be hashed (bcrypt/argon2).

response format:
TODO: We should discuss how the authentication works
Probably we should return the JWT token in a cookie or some error.

---
### Endpoint for logging into the system:
The session of the user has timed out and he has to log in once again or has logged out

POST request
request format:
```json
{
    username: "String",
    password: "String"
}
```

We should validate the data and check whether the credentials are correct. If they are we log him/her into the system.

response format:
Same as register basically

---
### Endpoint for logging out of the system:
The user wants to sign out of his account

POST request (or DELETE)
no request body

response format:
either success or failure

---
### Endpoint for refreshing the access token
Client makes a request, but the token is expired (401 unauthorized returned), so the browser makes a request to this endpoint to renew/refresh it.
/auth/refresh

POST request
request format:
```json
{
  "refreshToken": "eyJhbGciOiJIUzI1Ni..."
}
```

The user service validates the refresh token

response format:
either success or failure
