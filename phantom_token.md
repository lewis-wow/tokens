# Phantom Token

![Phantom Token](./assets/phantom_token.svg)

## Pros

Phantom tokens combine the privacy and instant revocability of opaque tokens on the client side with the performance benefits of stateless JWTs. The client only handles a secure opaque token, which completely protects user data from exposure and allows immediate revocation. Meanwhile, upstream microservices can verify the exchanged JWTs independently without central database lookups.

## The Problem

The internal JWTs generated during the exchange are often too generic and broadly scoped. If one of these tokens leaks within the internal microservice network, a compromised service or an attacker can reuse it to impersonate the user across any other unrelated service.

## The Solution

This vulnerability can be resolved by embedding specific transaction context into the exchanged JWT, such as a semantic tag of the exact operation the user initiated. This restricts the scope of the token to a single, specific action, transforming it into a secure [transaction token](./transaction_token.md).
