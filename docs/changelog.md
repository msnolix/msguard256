# 📜 Changelog – MS-GUARD-256
 
All notable changes to this project will be documented in this file.

## [1.1.0] – 2025-06-23
### Added
- Full documentation layout with modern Bootstrap design.
- New `/documentation/index.php` UI for API reference.
- Added security-focused `SECURITY.md` document.
- Added examples in JavaScript, Python, and PHP.

### Changed
- Replaced PBKDF2 with Argon2id for key derivation (enhanced security).
- Updated endpoint to `/api` with clearer structure.
- Improved response structure and error handling.

### Fixed
- IV reuse prevention through server-side storage.
- Mobile navbar animation glitch.

## [1.0.0] – 2025-06-21
### Added
- Initial release of MS-GUARD-256 encryption API.
- AES-256-GCM encryption with PBKDF2-HMAC-SHA256 key derivation.
- Stateless backend architecture.
