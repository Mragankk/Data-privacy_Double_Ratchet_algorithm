# Single Rachet Algorithm

#  Double Ratchet algorithm
- It is used by two parties to exchange encrypted messages based on a shared secret key.
- It uses a new secret key to encrypt every message so that an attacker who steals a single key can not decrypt previous or future messages.
- Forward secrecy: This ensures that if a session key is ever compromised, past and future messages remain secure.

## Key Derivation Function (KDF)
Double Ratchet uses a key derivation function like HKDF[HMAC Key Derivation Function ]

-  KDF as a cryptographic function that takes a secret and random KDF key and some input data and returns output data.

(img)[RDF](https://signal.org/docs/specifications/doubleratchet/Set0_0.png)
