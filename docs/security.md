# 🔐 Security Policy – MS-GUARD-256

MS-GUARD-256 is designed to be a secure, stateless AES-256-GCM encryption API built with strong cryptographic primitives. Below are the key aspects of our security policy:

---

## ✅ Security Features

- **AES-256-GCM Encryption**: Authenticated encryption with a 256-bit key, ensuring confidentiality and integrity.
- **Argon2id Key Derivation**: Secure password-based key derivation using memory-hard KDF with high resistance to GPU cracking.
- **Random IVs**: Each encryption uses a new 12-byte IV (nonce) to ensure uniqueness and protect against replay attacks.
- **Replay Prevention**: Optional server-side IV tracking ensures no nonce reuse for a given key.
- **Base64 Encoding**: All output is Base64 encoded for safe transport via query strings and APIs.

---

## 🚫 What We Don’t Do

- We **do not store** any user data, passwords, IVs, or encrypted payloads.
- We **do not log** API data beyond rate-limit control headers.
- We **do not decrypt** on your behalf—your key is required.

---

## ⚠️ Recommendations for Users

- Always use **HTTPS** when calling the API.
- Use **strong, unique passwords** for encryption keys.
- Never reuse encryption outputs (Base64 data) for different purposes.
- Do not share decrypted sensitive information publicly or with untrusted services.
- Limit requests per IP to avoid triggering rate limits (max 20 req/min).

---

## 🧪 Vulnerability Reporting

If you discover a security vulnerability, please report it privately:

- 📧 Email: `security@msnolix.com`

We will respond within **48 hours** and coordinate a responsible disclosure.

---

## 🛡️ Rate Limits and Abuse Prevention

To ensure fair usage and prevent abuse:

- Max requests: **20/minute per IP**
- Payload size: **1MB max**
- Multiple violations may result in **temporary IP bans**

---

© 2025 MS-GUARD-256 by MSNOLIX
