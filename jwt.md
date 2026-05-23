# JWT

![JWT](./assets/jwt.svg)

## Pros

JWTs are self-contained and embed user data directly within the payload. This allows microservices to verify them independently using cryptographic signatures, which eliminates central database lookups and significantly reduces network overhead.

```http
GET /api/v1/profile HTTP/1.1
Host: api.example.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwiaWF0IjoxNTE2MjM5MDIyfQ.t42p4AHef69Tyyi88U6-p0utZYYrg7mmCGhoAd7Zffs
```

## The Problem

JWTs are difficult to revoke instantly, meaning they remain valid until their expiration time. Additionally, because standard JWTs are only encoded and not encrypted, they can expose sensitive user information if intercepted on the client side.

## The Solution

The [phantom token](./phantom_token.md) architecture solves this by issuing a secure, opaque token to the client, which the client can easily revoke at any time. When a request hits the API Gateway, the gateway validates the opaque token and exchanges it for a stateless, self-contained JWT. Upstream microservices receive this JWT and verify it independently, combining the privacy and instant revocability of opaque tokens with the performance benefits of JWTs.
