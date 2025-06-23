# 🔒 Security Design

## Encryption Method
- AES-256 in GCM (Galois/Counter Mode)
- Provides both **confidentiality** and **integrity**

## Key Derivation
- PBKDF2 using SHA-256
- Random salt (included in output)
- Recommended password length: 12+ characters

## Output Structure
```
Base64(salt + IV + tag + ciphertext)
```

## Stateless Guarantee
- No input or result is stored
- API responses are ephemeral

> Always use HTTPS to secure data in transit