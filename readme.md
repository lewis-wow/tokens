# Token Architecture Evolution

This project explores the evolution of token-based authentication and authorization patterns within microservice architectures. It analyzes different token strategies, focusing on the trade-offs between system performance, user privacy, instant token revocability, and security scoping.

## Covered Patterns

1. [Session ID](./session_id.md) – Traditional opaque tokens that protect privacy but require central database lookups for every microservice.

2. [JWT](./jwt.md) – Stateless, self-contained tokens that eliminate database lookups but are difficult to revoke and can leak data on the client side.

3. [Phantom Token](./phantom_token.md) – A hybrid approach using secure opaque tokens on the client side and exchanging them for stateless JWTs at the API Gateway.

4. [Transaction Token](./transaction_token.md) – Tokens embedded with specific transaction context to restrict their scope and prevent internal reuse or impersonation.

5. [MultiSig Transaction Token](./multisig_transaction_token.md) – Advanced cryptographic tokens requiring multiple digital signatures to authorize high-value operations securely.
