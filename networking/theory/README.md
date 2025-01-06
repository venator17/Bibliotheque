---
icon: book-open
---

# Theory

## <mark style="color:yellow;">Network Sockets</mark>

<mark style="color:red;">**Socket**</mark> - is one <mark style="color:purple;">**endpoint**</mark> of a two way communication link between two programs running on the network. Sockets have two main states: They are either <mark style="color:yellow;">**connected**</mark> and facilitating an ongoing network communication, or they are <mark style="color:yellow;">**waiting**</mark> for an incoming connection to connect to them. The listening socket is called the server, and the socket that requests a connection with the listening socket is called a client. You could use **netstat** command to manage and discover your own sockets, for what and where are they used. The "Active Internet" section lists the network connections that are (or will be) established to external devices. The "UNIX domain" section lists the connections that have been established within your computer between different applications, processes, and elements of the operating system.

<mark style="color:blue;">**TCP Socket States**</mark>

| Socket State                                         | Explanation                                                                                                                |
| ---------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| <mark style="color:green;">**`LISTEN`**</mark>       | Servers-side. Socket waiting for a connection request                                                                      |
| <mark style="color:green;">**`SYN-SENT`**</mark>     | Client-side. Socket has made a connection request and wait.                                                                |
| <mark style="color:green;">**`SYN-RECEIVED`**</mark> | Server-side. Socket is waiting for a connection ack after accepting request                                                |
| <mark style="color:green;">**`ESTABLISHED`**</mark>  | Server and Client. A working connection has been established between the server and the client, allowing for data transfer |
| <mark style="color:green;">**`FIN-WAIT-1`**</mark>   | Server and Client. Socket is waiting for a termination request or for ack of previous termination request                  |
| <mark style="color:green;">**`FIN-WAIT-2`**</mark>   | Server and Client. Socket is waiting for a termination request                                                             |
| <mark style="color:green;">**`CLOSE-WAIT`**</mark>   | Socket is waiting for a termination request ack from local user                                                            |
| <mark style="color:green;">**`CLOSING`**</mark>      | Server and Client. Socket is waiting for a termination request ack from remote socket                                      |
| <mark style="color:green;">**`LAST-ACK`**</mark>     | Server and Client. Socket is waiting ack of termination from remote socket                                                 |
| <mark style="color:green;">**`TIME-WAIT`**</mark>    | Server and Client. Server and Client. Checking if termination ack was received                                             |
| <mark style="color:green;">**`CLOSED`**</mark>       | No connection, socket is terminated                                                                                        |

## <mark style="color:yellow;">DMZ</mark>

**`DMZ`**, or <mark style="color:red;">**Demilitarized Zone**</mark>, in the context of computer networks, is a <mark style="color:purple;">**segregated area**</mark> that acts as a buffer between a trusted internal network and an untrusted external network, such as the internet. It typically contains servers that need to be accessible from the internet. like web servers or email servers. The `DMZ` helps enhance security by isolation these servers from the internal network, by reducing the risk of unauthorized access to sensitive information.

## <mark style="color:yellow;">SSL</mark>

**`SSL`**, or <mark style="color:red;">**Secure Sockets Layer**</mark>, is an encryption-based <mark style="color:purple;">**Internet security protocol**</mark>. It was first developed by Netscape in **1995** for the purpose of ensuring privacy, authentication, and data integrity in Internet communications. **SSL** is the predecessor to the modern **TLS** encryption used today.

### <mark style="color:blue;">What is an</mark> <mark style="color:blue;"></mark><mark style="color:blue;">`SSL`</mark> <mark style="color:blue;"></mark><mark style="color:blue;">certificate?</mark>

`SSL` can only be implemented by websites that have an SSL certificate (technically a "TLS certificate"). An `SSL` certificate is like an ID card or a badge that proves someone is who they say they are. `SSL` certificates are stored and displayed on the Web by a website's or application's server.

One of the most important pieces of information in an `SSL` certificate is the website's public key. The public key makes encryption and authentication possible. A user's device views the public key and uses it to establish secure encryption keys with the web server. Meanwhile the web server also has a private key that is kept secret; the private key decrypts data encrypted with the public key.

### <mark style="color:blue;">What are the types of SSL certificates?</mark>

There are several different types of SSL certificates. One certificate can apply to a single website or several websites, depending on the type:

* <mark style="color:yellow;">**Single-domain**</mark>: A single-domain `SSL` certificate applies to only one domain (a "domain" is the name of a website, like www.cloudflare.com).
* <mark style="color:yellow;">**Wildcard**</mark>: Like a single-domain certificate, a wildcard SSL certificate applies to only one domain. However, it also includes that domain's subdomains. For example, a wildcard certificate could cover www.cloudflare.com, blog.cloudflare.com, and developers.cloudflare.com, while a single-domain certificate could only cover the first.
* <mark style="color:yellow;">**Multi-domain**</mark>: As the name indicates, multi-domain SSL certificates can apply to multiple unrelated domains.

## <mark style="color:yellow;">OpenSSL</mark>

<mark style="color:yellow;">**OpenSSL**</mark> is a widely-used <mark style="color:purple;">**open-source toolkit for implementing the SSL**</mark> and **TLS (Transport Layer Security)** protocols. It provides a set of cryptographic functions and utilities that enable secure communication over a computer network. OpenSSL is commonly used for creating and managing SSL/TLS certificates, generating cryptographic keys, and performing various cryptographic operations.

Here are some basic and common OpenSSL commands on Linux:

1. Check OpenSSL Version:

```bash
openssl version
```

2. Generate a Private Key:

```bash
openssl genprsa -out private-key.pem 2048
```

3. Generate a Public Key from a Private Key:

```bash
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

4. Generate a Self-Signed Certificate:

```bash
openssl req -x509 -newkey rsa:2048 -keyout private_key.pem -out certificate.pem -days 365
```

5. View Certificate Information:

```bash
openssl x509 -in certificate.pem -text -noout
```

6. Encrypt/Decrypt a File using RSA:
   *   Encrypt:

       ```bash
       openssl rsautl -encrypt -inkey public_key.pem -pubin -in plaintext.txt -out encrypted_data.bin
       ```
   *   Decrypt:

       ```bash
       openssl rsautl -decrypt -inkey private_key.pem -in encrypted_data.bin -out decrypted_data.txt
       ```
7. Hashing:
   *   Generate MD5 hash:

       ```bash
       openssl md5 file.txt
       ```
   *   Generate SHA-256 hash:

       ```bash
       openssl sha256 file.txt
       ```
