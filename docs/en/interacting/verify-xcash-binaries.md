---
title: Verifying XCash-Labs Binary Signatures
---

# Verify XCash-Labs Binaries

Verification **must be performed before extracting the archive and before running any XCash-Labs software**.

These instructions were tested on Linux and should also work on macOS with minor adjustments.

---

## 1. Import the lead maintainer PGP key

This is a one-time step. You can skip it for future releases once the key is trusted.

XCash-Labs releases are signed by the lead maintainer.  
Import the public key:

```bash
curl -fsSL https://raw.githubusercontent.com/Xcash-Labs/xcash-labs-core/master/utils/gpg_keys/minerjed.asc | gpg --import
```

Verify and trust the key (the fingerprint **must match exactly**):

```
0C79 760B 2656 C210 ABC6  0C88 6DAF 4E5E 07BA 77F8
```

Open the trust editor:

```bash
gpg --edit-key 0C79760B2656C210ABC60C886DAF4E5E07BA77F8
```

Then set trust:

```
gpg> trust
gpg> 4
gpg> quit
```

!!! danger
    If the fingerprint does not match, delete the key immediately:

    `gpg --delete-keys 0C79760B2656C210ABC60C886DAF4E5E07BA77F8`

    A mismatch could indicate a compromised or replaced key.

---

## 2. Verify the signed hash list

The official hash list is published here:  
https://www.xcashlabs.org/downloads/hashes.txt

Always verify the signature before trusting the file.

```bash
curl -fsSL https://www.xcashlabs.org/downloads/hashes.txt | gpg --verify
```

Expected output should include:

```
gpg: Good signature from "XCASH Maintainer (minerjed) <az0006t@protonmail>"
```

The `[unknown]` trust level is normal unless you fully signed the key locally.

---

## 3. Verify the downloaded file hash

Now confirm your downloaded archive matches the published hash.

Download the binaries (do **not** extract yet):  
[Download XCash-Labs](../interacting/download-xcash-binaries.md)

Example:

```bash
file_name=xcash-gui-linux-x64-VERSION.tar.bz2
file_hash=$(sha256sum "$file_name" | cut -c1-64)

curl -fsSL https://www.xcashlabs.org/downloads/hashes.txt > /tmp/reference-hashes.txt

grep "$file_hash" /tmp/reference-hashes.txt
```

If the hash appears in the output, the file is authentic.

!!! danger
    If no match is found:

    - Do **not** run the binaries  
    - Re-download the file  
    - Verify the signature again  

    A mismatch means the file may be corrupted or tampered with.

---

## Summary

You are safe to run the binaries only if:

- The maintainer key fingerprint matches  
- The hash list signature is valid  
- Your downloaded file hash matches the published hash  

If all checks pass, the release is authentic.