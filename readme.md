# Cryptography pratice #

This repository contais pratice for using encryption to send data using TCP.<br>
I've used the [Rust language](https://www.rust-lang.org/), the [openssl library](https://docs.rs/openssl/latest/openssl/) and the [uuid library](https://docs.rs/uuid/1.3.3/uuid/). <br>

# Server

The server simply generate and UUID and send to the user.

# Client 

Connects to the server and receive an UUID.

# Protocol

When the *server* receive a new connection, it will first create a pair of RSA public/private keys, it will send the public key encoded in the DER format to the *client* using the TCP stream. <br>
The *client* decode from the DER format and create an instance of the RSA public key. <br>
The *client* then generate a random AES key and the initialization vector. The KEY and the IV are encripted using the RSA public key and then sent to the *server*. <br>
The *server* receive the data and decode it using the RSA private key, and then it has access to the AES key and the IV. <br>
All next comunnication is done using the AES cipher. The *server* generates the UUID and encrypt with AES and send to the *client*. <br> 
Now the *client* receives the UUID and decode it. <br>

## Todo

- [ ] Error handling