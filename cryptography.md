🔐 **CTF Learnings: Identifying Hashes & Understanding IDOR**

While solving cryptography and web security CTF challenges, I learned an interesting lesson: sometimes, understanding the format of a hash can be the first step toward uncovering a security vulnerability.

🧩 **1. Recognizing Hash Algorithms by Length**

One of the first things I learned was how to identify *possible* hashing algorithms by looking at the length of their hexadecimal digests:

🔹 **32 hex characters** → MD5 (128-bit digest)

🔹 **40 hex characters** → SHA-1 (160-bit digest)

🔹 **64 hex characters** → SHA-256 (256-bit digest)

🔹 **96 hex characters** → SHA-384 (384-bit digest)

🔹 **128 hex characters** → SHA-512 (512-bit digest)

These lengths are useful clues, but they don't uniquely identify an algorithm. Context and verification are still necessary.

💻 **2. Verifying Hashes with Linux**

I practiced using command-line utilities such as `md5sum` and `sha256sum` to calculate hashes and compare them with values found in a challenge.

For example:

```bash
echo -n "3000" | md5sum
```

This helped me understand how an application might generate a hash from an input and why even a small change in that input produces a different digest.

🛡️ **3. Connecting Hashes to Web Security**

The challenge also introduced me to **IDOR (Insecure Direct Object Reference)** and predictable resource identifiers.

Key lessons:

- Hashing an identifier does not automatically make it secure.
- Predictable identifiers can expose weaknesses when authorization checks are missing.
- Proper server-side access control matters more than hiding or transforming an identifier.

🎯 **My biggest takeaway:** Don't just recognize a hash—investigate how it is generated, how it is used, and whether the application handles access control correctly.

Every CTF challenge is an opportunity to strengthen my analytical thinking and build practical cybersecurity skills.
