# tls-cert

## What is asymmetric encription?

an encryption mechanic that uses a pair of public and private keys
if msg is encrypted with pub key it can only be decrypted with private key
the reverse is also true

## What is symetric encryption?

an encryption mechanic that uses same key for both encryption and decryption

## What are the main steps in asymetric encryption?
client: hello
server: hello, here is my public key
client: i'll encrypt a symetric key with your pub key and send it
server: i'll use my private key to decrypt that
now both parties have a symetric key they can use for further communication

## What is a certificate authority?

a trusted entity that issues and manages digital certificates which validates website identities

## What are the main steps in asymetric encryption with a certificate authority?

client: hello
server: hi ca, here is my pub key
ca: hi server, i've encrypted the server pub key with my priv key, here is your certificate
server: hi client here is my certificate, it has my pub key in clear, and my pub key encrypted by the ca
client: hi ca, give me your pub key, 
i'll use that ca pub key to decrypt cert and get server pub key, then compare clear srv pub key with decrypted pub key, if they are the same, there is no one in the middle of the commnication


## What does tls_ecdhe_rsa_with_aes_128_gcm_sha256?

tls transport layer security
ecdhe elliptic curve diffie-hellman ephemerat
(key exchange method)
rsa rivest–shamir–adleman
(public key authentication mechanism)
aes advanced encryption standard
(symetric block cypher, the thing that does the actual encription)
128 key size
gcm galois/counter mode
(mode of operation for symmetric-key cryptographic block ciphers)
sha256 secure hash algorithm 256-bit
(hashing function (turn secret into key etc))

## What steps are done in a tls 1.2 handshake?

establish tcp client server connection 
client hello 
(max tls version they support, random nr, list of cyphers they support)
server hello 
(chosen tls version, chosen cypher, another random nr)
server sends certificate 
(with pub key)
server sends server key exchange
(the params for ecdhe, digital signature)
server hello done
client key exchange 
client change cypher spec
client finish
(encrypted message with info exchanged so far)
server change cypher spec
server finish
(encrypted message with info exchanged so far)