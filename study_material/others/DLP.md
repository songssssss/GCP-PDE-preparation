Create a pseudonym by replacing PII data with a cryptographic format-preserving token.

Format preserving encryption: An input value is replaced with a value that has been encrypted using the FPE-FFX encryption algorithm with a cryptographic key, and then prepended with a surrogate annotation, if specified. By design, both the character set and the length of the input value are preserved in the output value. Encrypted values can be re-identified using the original cryptographic key and the entire output value, including surrogate annotation.


Cryptogenic tokens and cryptographic tokens serve different purposes and have distinct characteristics, especially when it comes to data security and privacy. Here’s a detailed comparison of the two:

### Cryptogenic Tokens

**1. Definition:**
- Cryptogenic tokens are a type of pseudonymization technique where the original data is replaced with tokens that are generated in a way that is not easily reversible. These tokens are usually random or generated based on certain algorithms but do not necessarily adhere to strict cryptographic standards.

**2. Characteristics:**
- **Non-Reversible**: Cryptogenic tokens are designed to be non-reversible, meaning the original data cannot easily be reconstructed from the tokens.
- **Randomness**: The tokens are typically random or generated with algorithms that ensure uniqueness and reduce predictability.
- **Format**: Cryptogenic tokens often do not preserve the original data's format, which might affect usability in applications that require format consistency for joins or other relational operations.

**3. Use Cases:**
- Often used in scenarios where data needs to be anonymized but is not required to maintain the original format for relational operations.
- Suitable for general pseudonymization tasks where high cryptographic strength is not essential.

**4. Security:**
- Security is based on the randomness and uniqueness of the tokens rather than cryptographic strength.
- Less stringent compared to cryptographic tokens, and may not offer the same level of protection.

### Cryptographic Tokens

**1. Definition:**
- Cryptographic tokens are generated using cryptographic algorithms and standards to ensure both security and integrity. They are designed to be secure, non-reversible, and often adhere to specific encryption or hashing standards.

**2. Characteristics:**
- **Format-Preserving**: Cryptographic tokens can be format-preserving, meaning they retain the original data's format and structure, which is crucial for maintaining referential integrity in relational databases.
- **Cryptographic Security**: They are generated using cryptographic methods (e.g., encryption or hashing) that ensure high security. This includes mechanisms like encryption keys, hashing algorithms, and secure key management practices.
- **Reversibility**: Depending on the method used, some cryptographic tokens can be reversible (e.g., encrypted values), while others (e.g., hash-based tokens) are not.

**3. Use Cases:**
- Ideal for applications requiring strong security and integrity, such as protecting sensitive data while maintaining its usability for operations like database joins or data analysis.
- Used in scenarios where both security and format preservation are critical.

**4. Security:**
- Provides high security due to the use of well-established cryptographic algorithms and protocols.
- Ensures that tokens are resistant to attacks and unauthorized access, providing robust protection for sensitive data.

### Summary

- **Cryptogenic Tokens**: Primarily used for pseudonymization where high cryptographic strength is not required. They are typically random and do not preserve the original format, which may affect certain data operations.

- **Cryptographic Tokens**: Use cryptographic techniques to ensure high security and integrity. They can be format-preserving, allowing for consistent data operations while maintaining strong protection of sensitive information.

For applications requiring data security and the ability to maintain referential integrity (such as in databases where format preservation is crucial), cryptographic tokens are generally more appropriate. Cryptogenic tokens might be suitable for less sensitive use cases where format preservation is not a concern.
