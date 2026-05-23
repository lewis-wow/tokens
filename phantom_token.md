# Phantom Token

![Phantom Token](./assets/phantom_token.svg)

## Pros

Phantom tokens combine the privacy and instant revocability of opaque tokens on the client side with the performance benefits of stateless JWTs. The client only handles a secure opaque token, which completely protects user data from exposure and allows immediate revocation. Meanwhile, upstream microservices can verify the exchanged JWTs independently without central database lookups.

```http
POST /oauth2/introspect HTTP/1.1
Host: auth.example.com
Authorization: Basic Z2F0ZXdheV9pZDpnYXRld2F5X3NlY3JldA==
Content-Type: application/x-www-form-urlencoded

token=6c7e3a9b1f2d4e5c6a7b8c9d0e1f2a3b&token_type_hint=access_token
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "active": true,
  "scope": "read write",
  "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIn0.Q6CM1qIz2WTgTlhMzpFL8jI8xbu9FFfj5DY_bGVY98Y"
}
```

## The Problem

The internal JWTs generated during the exchange are often too generic and broadly scoped. If one of these tokens leaks within the internal microservice network, a compromised service or an attacker can reuse it to impersonate the user across any other unrelated service.

## The Solution

This vulnerability can be resolved by embedding specific transaction context into the exchanged JWT, such as a semantic tag of the exact operation the user initiated. This restricts the scope of the token to a single, specific action, transforming it into a secure [transaction token](./transaction_token.md).
