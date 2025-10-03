#  Double Ratchet algorithm
- It is used by two parties to exchange encrypted messages based on a shared secret key.
- It uses a new secret key to encrypt every message so that an attacker who steals a single key can not decrypt previous or future messages.
- Forward secrecy: This ensures that if a session key is ever compromised, past and future messages remain secure.
- If someone learns the key used to generate future secrets (the KDF key), they still won't be able to predict those future secrets as long as enough new, random information (entropy) has been added to the process.

## Key Derivation Function (KDF) Chains
Double Ratchet uses a key derivation function like HKDF[HMAC Key Derivation Function ]

-  KDF is a cryptographic function that takes a secret and random KDF key and some input data and returns output data.
-  In a Double Ratchet session each party stores a KDF key for three chains: a root chain, a sending chain, and a receiving chain 
- A KDF chain has the key and input and produces an output where some of the output is a key, that can be used for other things, and some of the output is a key that can be used as another KDF key. So that new KDF key can be combined with another input and produce another output, and so on.
  
![KDF_chain](https://signal.org/docs/specifications/doubleratchet/Set0_0.png)

##  Symmetric-key ratchet
- A constant and a KDF key into a KDF function gives a new KDF key and a message key. The message key is used as a symmetric key for encryption/decryption.

  ![symmteric_key_ratchet](https://signal.org/docs/specifications/doubleratchet/Set0_1.png)

##  Diffie-Hellman ratchet
- Key Generation: Each party generates a DH key pair (public and private keys) as their current ratchet keys.
- Each message includes the sender’s current ratchet public key.
- Key Update: When a new ratchet public key is received, a DH ratchet step replaces the local ratchet keys with new ones.
- The parties alternate replacing their key pairs. If an attacker compromises a key, it is eventually replaced, and the new DH calculation becomes unknown to the attacker.
