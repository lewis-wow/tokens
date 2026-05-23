# Transaction Token

![Transaction Token](./assets/transaction_token.svg)

## Pros

Transaction tokens restrict the scope of the internal JWT to a specific, single operation by embedding transaction context like a semantic tag. They inherit all the architectural benefits of phantom tokens, including client-side privacy, instant revocability, and stateless microservice verification. By scoping the token tightly, they completely eliminate the risk of internal token reuse or lateral impersonation across unrelated microservices.

```http
POST /oauth2/introspect HTTP/1.1
Host: auth.example.com
Authorization: Basic Z2F0ZXdheV9pZDpnYXRld2F5X3NlY3JldA==
Content-Type: application/x-www-form-urlencoded

token=6c7e3a9b1f2d4e5c6a7b8c9d0e1f2a3b&operation=payment_initiate&amount=500
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "active": true,
  "scope": "write",
  "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwidHhuX3RhZyI6InBheW1lbnRfaW5pdGlhdGUiLCJhbW91bnQiOjUwMH0.lIoJXPsLVeXeW3hxTOUoSXAXstbDoLx4YHInF4E7EJo"
}
```

## The Problem

## The Solution
