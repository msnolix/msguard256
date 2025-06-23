# 🔐 MS-GUARD-256 Encryption API Documentation

> **Secure AES-256-GCM API with PBKDF2 key derivation**  
> Developed by [MSNOLIX](https://msnolix.com) – Try it live at [https://guard.msnolix.com](https://guard.msnolix.com)

## 🔎 Overview

The **MS-GUARD-256** API provides secure, stateless encryption and decryption using:

- **AES-256-GCM** for encryption
- **PBKDF2 (SHA-256)** for key derivation
- Base64-safe output
- Zero data storage (100% stateless API)

## 🌐 Base API Endpoint

```
https://guard.msnolix.com/api
```

## 📥 Parameters

| Parameter | Required | Description |
|----------|----------|-------------|
| `action` | ✅ Yes | `encrypt` or `decrypt` |
| `data`   | ✅ Yes | The string to encrypt or the Base64 encoded string to decrypt |
| `key`    | ✅ Yes | Your password (8–64 chars, used in PBKDF2) |

## 🧪 Example Usage

### 🔐 Encrypt
```
GET https://guard.msnolix.com/api?action=encrypt&data=Hello%20World&key=mySecret
```
```json
{
  "success": true,
  "result": "BASE64_ENCRYPTED_STRING"
}
```

### 🔓 Decrypt
```
GET https://guard.msnolix.com/api?action=decrypt&data=BASE64_ENCRYPTED_STRING&key=mySecret
```
```json
{
  "success": true,
  "result": "Hello World"
}
```

## 💻 Code Examples

### JavaScript
```js
fetch("https://guard.msnolix.com/api?action=encrypt&data=Hello World&key=mySecret")
  .then(res => res.json())
  .then(data => console.log("Encrypted:", data.result));
```

### Python
```python
import requests
res = requests.get("https://guard.msnolix.com/api", params={
  "action": "encrypt",
  "data": "Hello World",
  "key": "mySecret"
})
print("Encrypted:", res.json()["result"])
```

### PHP
```php
$url = "https://guard.msnolix.com/api?action=encrypt&data=Hello%20World&key=mySecret";
$response = json_decode(file_get_contents($url), true);
echo "Encrypted: " . $response['result'];
$dec_url = "https://guard.msnolix.com/api?action=decrypt&data=" . urlencode($response['result']) . "&key=mySecret";
$decoded = json_decode(file_get_contents($dec_url), true);
echo "Decrypted: " . $decoded['result'];
```

## 📌 Notes

- Uses AES-256-GCM with 16-byte tag
- Key is derived with PBKDF2 + SHA-256 + random salt
- Output = Base64(salt + IV + tag + ciphertext)
- API is stateless — no data stored
- Use HTTPS to protect in transit

## 📚 Related Docs

- [How It Works](docs/how-it-works.md)
- [Security Details](docs/security.md)
- [Changelog](docs/changelog.md)

## 👨‍💻 Author

Developed by [MSNOLIX](https://msnolix.com)  
Official Tool: [https://guard.msnolix.com](https://guard.msnolix.com)

## 📜 License

MIT © [MSNOLIX](https://msnolix.com)
