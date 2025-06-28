---
title: "ORA-29024: Certificate Validation Failure – What It Is and How To Fix It"
categories:
  - oracle
tags:
  - oracle
  - ssl
  - error
  - troubleshooting
date: 2025-06-27 10:00:00 +0300
---

## ORA-29024: Certificate Validation Failure

### 🧩 Error Summary
This error typically occurs when an Oracle database tries to establish a secure SSL/TLS connection but fails to validate the certificate.

### 💡 Root Causes
- The certificate chain is incomplete or invalid.
- The system clock is not in sync.
- The Oracle Wallet does not contain the correct trusted certificates.

### 🔧 How to Fix

1. Check the certificate chain:

```bash
orapki wallet display -wallet /path/to/wallet
```

2. Make sure the trusted certificate is properly imported:

```bash
orapki wallet add -trusted_cert -cert /path/to/rootCA.pem -wallet /path/to/wallet -pwd your_wallet_password
```

3. Check `sqlnet.ora` and `listener.ora` for correct wallet path.

4. Ensure system date/time is correct.

### 📌 Bonus Tip
Try setting the following in `sqlnet.ora` to disable strict certificate validation (not recommended for production):

```
SSL_SERVER_DN_MATCH = no
```

> This article is part of my Oracle troubleshooting notes.  
> Hope it helps!
