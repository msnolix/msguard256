# 🔧 How MS-GUARD-256 Works

1. You send a request to the API with:
   - `action=encrypt|decrypt`
   - `data`
   - `key`

2. Internally:
   - A 256-bit key is derived using PBKDF2 (SHA-256 + Salt)
   - A 12-byte IV is generated
   - AES-256-GCM is applied to encrypt or decrypt
   - Output is formatted as Base64(salt + IV + tag + ciphertext)

3. The server **does not store** any data — it's 100% stateless.

4. You must use the **same key** to decrypt successfully.