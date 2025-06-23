# 🔧 How MS-GUARD-256 Works

MS-GUARD-256 is a modern encryption API using AES-256-GCM with secure password-based key derivation and stateless architecture.

---

## 🔐 Step-by-Step Encryption Process

1. **API Request**  
   You send a request to the API with:
   - `action=encrypt` or `action=decrypt`
   - `data` – your plaintext or Base64-encoded ciphertext
   - `key` – your secret password

2. **Key Derivation**  
   - The server generates a **random salt**
   - It uses **Argon2id** to derive a 256-bit key from the password:
     - Memory: 128MB  
     - Iterations: 8  
     - Output: 256-bit encryption key  

3. **AES-256-GCM Encryption**  
   - A 12-byte IV is generated randomly for each encryption
   - The key and IV are used to encrypt the data using AES-GCM
   - The authentication tag (16 bytes) is generated

4. **Encoding & Output**  
   - Final format:  
     `version + salt + iv + tag + ciphertext`  
   - The full binary blob is Base64-encoded and returned

---

## 🔁 Decryption Process

To decrypt:
- You send the **Base64 string** and the same **key (password)**
- The server:
  - Parses the version, salt, iv, tag, and ciphertext
  - Derives the key again with Argon2id using the original salt
  - Decrypts the data with AES-GCM
- If the key is wrong or the data is tampered, decryption fails securely.

---

## ⚙️ Key Points

- AES-256-GCM with Argon2id for high-security encryption
- 12-byte IV ensures nonce uniqueness
- Authentication tag provides integrity check
- No user data or password is ever stored
- Stateless server = more privacy, less risk

---

## 🛡️ Security Advice

- Always use strong passwords
- Never reuse the same password across systems
- Do not reuse encrypted outputs
- Only use the encrypted Base64 once (fresh IV each time)

---

Built with 💙 by [MSNOLIX](https://msnolix.com)
