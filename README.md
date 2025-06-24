# 🔐 MS-GUARD-256 – Secure Encryption API

**MS-GUARD-256** is a free, in-browser encryption/decryption API built using **AES-256-GCM** and secure **Argon2id-based key derivation**. It is designed for privacy, speed, and total statelessness.

---

## 🔧 How MS-GUARD-256 Works

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

---

## 🧪 API Endpoint

```
https://guard.msnolix.com/api
```

---

## 🔢 Parameters

| Name     | Type   | Required | Description                          |
|----------|--------|----------|--------------------------------------|
| action   | string | yes      | `encrypt` or `decrypt`               |
| data     | string | yes      | Plaintext (or Base64 encrypted text) |
| key      | string | yes      | Password for encryption/decryption   |

---

## 📦 Example Usage

### 🔒 Encrypt
```
GET https://guard.msnolix.com/api?action=encrypt&data=Hello%20World&key=secret123
```

```json
{
  "success": true,
  "result": "base64_payload_here"
}
```

### 🔓 Decrypt
```
GET https://guard.msnolix.com/api?action=decrypt&data=base64_payload_here&key=secret123
```

```json
{
  "success": true,
  "result": "Hello World"
}
```

---

## 💻 Code Examples

### ✅ JavaScript
```js
fetch("https://guard.msnolix.com/api?action=encrypt&data=Hello%20World&key=secret123")
  .then(res => res.json())
  .then(json => console.log("Encrypted:", json.result));
```

### ✅ Python
```python
import requests

enc = requests.get("https://guard.msnolix.com/api", params={
  "action": "encrypt",
  "data": "Hello World",
  "key": "secret123"
}).json()["result"]

print("Encrypted:", enc)

result = requests.get("https://guard.msnolix.com/api", params={
  "action": "decrypt",
  "data": enc,
  "key": "secret123"
}).json()["result"]

print("Decrypted:", result)
```

### ✅ PHP
```php
$enc = json_decode(file_get_contents("https://guard.msnolix.com/api?action=encrypt&data=Hello%20World&key=secret123"), true);
echo "Encrypted: " . $enc['result'] . "\n";

$dec = json_decode(file_get_contents("https://guard.msnolix.com/api?action=decrypt&data=" . urlencode($enc['result']) . "&key=secret123"), true);
echo "Decrypted: " . $dec['result'] . "\n";
```

---

## 📌 Technical Details

- Encryption: AES-256-GCM
- Key Derivation: PBKDF2 (SHA-256), 256-bit key
- Output: Base64(salt + IV + tag + ciphertext)
- IV length: 12 bytes
- Tag length: 16 bytes
- Stateless API (no logs or storage)
- Rate limiting: 20 requests/minute per IP
- Max data size: 1MB

---

## ❤️ Support

If you like this tool, consider supporting us:

[![Buy Me a Coffee](assets/yellow-button.png)](https://buymeacoffee.com/msnolix)

---

## 🌐 Website

[🔗 https://guard.msnolix.com](https://guard.msnolix.com)

---

© 2025 MSNOLIX – All rights reserved.
