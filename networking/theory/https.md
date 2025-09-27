# HTTPS

## <mark style="color:yellow;">TLS HANDSHAKE</mark>

* <mark style="color:$primary;">**ClientHello**</mark>\
  Client sends supported TLS version, cipher suites, and a random number.
* <mark style="color:$primary;">**ServerHello**</mark>\
  Server picks a TLS version and cipher suite from the client's list, sends its own random number.
* <mark style="color:$primary;">**Server Certificate**</mark>\
  Server sends its <mark style="color:red;">**digital certificate**</mark> to prove its identity.
* <mark style="color:$primary;">**Key Exchange**</mark>\
  Client and server exchange cryptographic values to generate a shared <mark style="color:red;">**premaster secret**</mark>.
* <mark style="color:$primary;">**Master Secret Derivation**</mark>\
  Both sides compute the <mark style="color:red;">**master secret**</mark> using the premaster secret and both random values.
* <mark style="color:$primary;">**ChangeCipherSpec + Finished**</mark>\
  Client and server activate encryption and verify that handshake was successful.
* <mark style="color:$primary;">**Secure Communication**</mark>\
  All further messages are encrypted using session keys derived from the master secret.

## <mark style="color:yellow;">TERMS</mark>

### <mark style="color:blue;">**Certificate**</mark>

<mark style="color:red;">**Certificate**</mark> is a <mark style="color:purple;">**digital identity document sent by the server to prove it is who it claims to be**</mark>. It follows the X.509 standard and contains the server’s public key, along with identifying information like its domain name. The certificate is signed by a trusted **Certificate Authority (CA)**, allowing the client to verify its authenticity. If the certificate is valid and trusted, the client continues the handshake.

### <mark style="color:blue;">**Premaster Secret**</mark>

<mark style="color:red;">**Premaster Secret**</mark> is a <mark style="color:purple;">**temporary value that client and server both calculate during the handshake**</mark> using key exchange methods like RSA or Diffie-Hellman. It is not transmitted directly; instead, it’s derived securely from exchanged public and private values. This secret ensures that both sides have a common foundation for encryption without exposing it to eavesdroppers. The premaster secret is used only to create the master secret.

### <mark style="color:blue;">**Master Secret**</mark>

<mark style="color:red;">**Master Secret**</mark> is the <mark style="color:purple;">**final shared key derived from the premaster secret and both the client’s and server’s random numbers**</mark>. It’s computed independently by both parties using a secure key derivation function. The master secret is never sent over the network; instead, it’s used to generate the actual encryption and authentication keys for the session. This key forms the cryptographic core of the secure connection.
