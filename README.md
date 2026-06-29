# -Hybrid-Cryptographic-Cloud-Storage-Security-
A client-side hybrid cryptographic protocol for secure cloud storage with a zero-knowledge architecture, secure file sharing, and cryptographic key management.

⸻

Overview

SecureVault is a browser-based secure cloud storage protocol that encrypts files locally before upload. The cloud provider stores only encrypted data and wrapped encryption keys, ensuring that plaintext files and private keys never leave the client.

The protocol combines symmetric and asymmetric cryptography to support secure storage, multi-user file sharing, access revocation, and optional key rotation.

⸻

## Cryptographic Design

| Component | Algorithm | Purpose |
|-----------|-----------|---------|
| File Encryption | AES-256-GCM | Confidentiality and Integrity |
| Key Wrapping | RSA-OAEP (3072-bit) | Secure key distribution |
| Master Key Derivation | PBKDF2-SHA256 (100,000 iterations) | Password-based key derivation |
| File Key Derivation | HKDF-SHA256 | Per-file key generation |
| Integrity Verification | AES-GCM Authentication Tag | Tamper detection |


⸻

## System Architecture

```text
Trusted Client
│
├── Web Crypto API
│   ├── AES-256-GCM
│   ├── RSA-OAEP
│   ├── PBKDF2
│   └── HKDF
│
├── Local Key Management
│
└── HTTPS/TLS
        │
        ▼
Untrusted Cloud
│
├── Encrypted Files
├── Wrapped Keys
└── Metadata & Access Control
```


1. User authentication derives a master key using PBKDF2.
2. An RSA-3072 key pair is generated for each user.
3. A unique file encryption key is derived using HKDF.
4. The file is encrypted locally using AES-256-GCM.
5. The file key is wrapped with the user’s RSA public key.
6. The cloud stores only ciphertext, IV, salts, and wrapped keys.
7. During download, the wrapped key is unwrapped using the user’s private key.
8. For file sharing, the file key is wrapped with each recipient’s public key.
9. Access revocation removes the recipient’s wrapped key and optionally performs key rotation.

⸻

Security Features

* Zero-knowledge storage architecture
* Client-side encryption
* AES-GCM authenticated encryption
* Secure multi-user file sharing
* Cryptographic access revocation
* Optional key rotation
* Replay attack protection using unique IVs
* Role-based access control (RBAC)

⸻

## Security Evaluation

| Scenario | Result |
|----------|--------|
| Unauthorized access | Blocked |
| Ciphertext tampering | Detected |
| Replay attack | Prevented |
| Revoked user access | Blocked after key rotation |
| Incorrect password | Authentication failed |

⸻

## Performance

| Operation | Average Time |
|-----------|--------------|
| RSA-3072 Key Generation | ~2.3 ms |
| AES-GCM Encryption (1 KB) | ~0.15 ms |
| AES-GCM Decryption (1 KB) | ~0.12 ms |
| Complete Protocol Execution | ~8.4 ms |


⸻

Technologies

* HTML5
* CSS3
* JavaScript (ES6)
* Web Crypto API
* Git & GitHub

⸻

Research Paper

Enhancing Cloud Storage Security Through Hybrid Cryptographic Techniques

Authors:

* Ghaidaa Algarni
* Ghada Alhajaji
* Joud Alharbi
* Abrar Allugmani

Department of Cybersecurity
Umm Al-Qura University
2026

⸻

My Contributions

* System architecture design
* Threat modeling
* Trust assumptions and security goals
* Cryptographic protocol design
* Key management strategy
* Security analysis
* Protocol documentation
* Limitations and future work

⸻

References

* Google Drive Client-Side Encryption
* AWS Key Management Service (KMS)
* Dropbox Security 

