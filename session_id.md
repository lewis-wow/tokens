# Session ID

![Session ID](./assets/session_id.svg)

## Pros

Opaque tokens protect user privacy because they do not contain any embedded personal data. They are also easy to revoke instantly since the authentication server validates them directly against a database.

```http
GET /api/v1/profile HTTP/1.1
Host: api.example.com
Cookie: session_id=6c7e3a9b1f2d4e5c6a7b8c9d0e1f2a3b
```

## The Problem

Every microservice behind the API Gateway must call the authentication server to validate the token and retrieve user information, which can introduce network overhead.

## The Solution

[JSON Web Tokens](./jwt.md) (JWTs) solve this by embedding the necessary user data directly into the token, making it self-contained. This allows each microservice to verify the token independently using cryptographic signatures, completely eliminating the need to query the central authentication server for every request.
