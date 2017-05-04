---
 layout: notes
 title: Message System Encryption
 scribe: Li Liu
---
 # Secion 1: End-to-End Encryption

 Using Wahtsapp, message like following will be sent:
 "Messages you sned to this chat and calls are nwo secured with end-to-end encryption"
 

 Unlike TLS and email, end-to-end will only have the two clients read messages, and service providers will not be able to do so.
 But metadata is still visible to service provider.

 # Section 2: The OTR 3-step Diffie-Hellman Ratchet
 
 Forward Secrecy:
 Diffie-Hellman: g^a and g^b used to encrypt and decrypt. Sign_sk(g^a, g^b) used to authenticate


 Encrypted coversation is a promise, and conversation in the past can't be decrypted. Session key a and b will be deleted after session.

 Third parties like iCloud has backdoor to this protocol.

 
 # Section 3: Asynch Hash Ratchet
 
 Protocol details is following:
 {k1 = H(ms), k2 = H(k1), k3 = H(k2)}
 If a key is obtained, then adversary can decrypt message that comes later, but cannot decrypt the message in the past.

 Some Drawback: 
 The key material is sensitive. However, it can be used to calculate the key material for every subsequent sequence number. So a client can’t hang on to it forever.
 
 # Section 4: Signal 2 step DH Ratchet

 1. A generates one new ECDH ephemeral key A1 and use this to send a message
 2. A receives a message from B's key B1.
 3. A wants to send a new message, destroy A1 and create new key A2.
 A hash-based ratchet is added between chain keys.
 
 
 # Section 5: Metadata leaks information

 Key distribution is problematic: how to get the key? How to know the key is real? how access the key?


 # Section 6: Tor
 It prevents people from knowing your metadata.
 Prevents other people to know the source IP, and some other metadata
 
 Mixing sitting between sources and destinations. (Random)

 Also, multi-layers of encryption is used, for example:
 Enc_k1(Enc_k2(Enc_k3(m)))
 If the attacker does not know all key, decryption is impossible.
 
 To use TOR, all communications must be under TOR, such as DNS lookups. Focus of TOR is anonymity of the communications pipe, instead of the data passes through it.
