## 🕵️ Cipher & Encoding Identification Guide

When analyzing an unknown string in a CTF challenge, use these visual signatures to quickly identify the underlying algorithm.

### 1. Base64
*   **Key Indicator:** Look for **trailing equals signs (`=` or `==`)** used as padding at the end of the string.
*   **Character Set:** Alphanumeric mix of uppercase letters (`A-Z`), lowercase letters (`a-z`), and numbers (`0-9`).
*   **Other Symbols:** May occasionally include `+` and `/`. It will never contain spaces.
*   **Nested Signatures:** If the output yields a Python byte literal wrapper like `b'...'`, strip the wrapper away. If the inner text still features alphanumeric characters ending in `=`, the string has been **Base64 encoded multiple times**.

### 2. Hexadecimal (Base16)
*   **Key Indicator:** Text is strictly restricted to **numbers `0-9` and letters `A-F`** (case-insensitive).
*   **Character Set:** `0123456789abcdef`
*   **Clue:** The total character length is almost always an even number. In some formats, pairs are separated by spaces or prefixed with `0x` (e.g., `0x61 0x63`).

### 3. Base32
*   **Key Indicator:** Aggressive padding featuring **up to six trailing equals signs (`======`)**.
*   **Character Set:** Uses **only uppercase letters `A-Z` and numbers `2-7`**.
*   **Clue:** It will never contain lowercase letters, nor will it contain the numbers `0`, `1`, `8`, or `9`.

### 4. Caesar Cipher (ROT)
*   **Key Indicator:** The text looks like a scrambled but pronounceable word, and **retains all original punctuation and case structure**.
*   **Clue:** Look for distorted versions of standard flag formats. For example, if a challenge flag format is `academy{...}` and you see a string starting with `hjhkltf{...}`, calculate the alphabet distance between `a` and `h` to quickly determine the rotation shift.
