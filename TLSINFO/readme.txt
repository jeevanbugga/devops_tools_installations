# Encryption Concepts
## Key Terms

- **Public Key**: A cryptographic key that can be shared openly and is used to encrypt data. It is part of an asymmetric key pair and can only be decrypted by its corresponding private key.
  
- **Private Key**: A cryptographic key that is kept secret and is used to decrypt data that was encrypted with the corresponding public key. It should never be shared.

- **Certificate Authority (CA)**: A trusted organization that issues digital certificates to verify the authenticity of a public key. CAs help establish trust between users and servers.



## Encryption Concepts By taking example in Bank Transactions
## Symmetric Encryption (SE)

- **Definition**: Symmetric encryption uses the same key for both encryption and decryption of data. It is fast and efficient, making it ideal for encrypting large amounts of data.
  
- **Potential Issue**: If a symmetric key is intercepted by a hacker, the hacker can decrypt the data easily, compromising security. This is why symmetric encryption is not used alone for initial communication between a user and a server.

## Asymmetric Encryption (AE)

- **Definition**: Asymmetric encryption uses a pair of keys—a public key and a private key. The public key is used for encryption, and the private key is used for decryption. This approach provides secure key exchange, even over unsecured networks.

## Flow of Asymmetric and Symmetric Encryption in Bank Transactions

### 1. Initiating a Secure Connection (DNS Lookup)

- **Example Scenario**: Jeevan is trying to access the bank’s website at `https://www.sbi.com`.
- **DNS Lookup**: Jeevan’s browser performs a DNS lookup to resolve the domain `www.sbi.com` to the bank server’s IP address. Once the IP is resolved, the browser initiates a connection to the bank’s server.

### 2. SSL/TLS Handshake (Asymmetric Encryption Phase)

- **Certificate Exchange**: The bank’s server responds with its SSL/TLS certificate, which includes the server’s public key and information about the Certificate Authority (CA) that issued the certificate.
  
- **Certificate Validation**: Jeevan’s browser validates the certificate to ensure it is from a trusted CA, hasn’t expired, and hasn’t been revoked. If the certificate is invalid, the browser will warn Jeevan. If valid, the handshake proceeds.

- **Session Key Generation**: Jeevan’s browser generates a unique symmetric key, known as the session key. This key will be used for encrypting data during the session.

- **Session Key Encryption**: The browser encrypts the session key using the bank’s public key (asymmetric encryption) and sends it to the bank’s server.

- **Decryption by Bank**: The bank’s server uses its private key to decrypt the session key sent by Jeevan’s browser. Now, both the browser and the server have the same session key.

### 3. Establishing a Secure Communication Channel (Symmetric Encryption Phase)

- **Secure Tunnel Establishment**: Using the decrypted session key, a secure SSL/TLS tunnel is established between Jeevan’s browser and the bank’s server. This tunnel ensures that all subsequent data transmitted is encrypted and secure.

- **Data Encryption**: Now, both Jeevan’s browser and the bank’s server use the session key to encrypt and decrypt all data. For example, when Jeevan sends his login credentials, they are encrypted with the session key before being sent to the server.

### 4. Authentication and Session Management

- **Session Authentication**: Once Jeevan’s login credentials are verified, the bank’s server authenticates the session. Jeevan can now perform actions like viewing account details or making transactions securely.

- **Continuous Symmetric Encryption**: Throughout the session, symmetric encryption (using the session key) ensures that data remains secure and that communication is fast and efficient.

- **Session Termination**: When Jeevan logs out or after a period of inactivity, the session is terminated, and the session key is discarded. This prevents any potential reuse of the session key, enhancing overall security.

> ## Note:
Here, the user (Jeevan) is validating whether the bank site is genuine by checking the bank’s certificate (which includes the bank’s public key along with CA information).

**How Does the Bank Trust That the User Is Genuine?** The bank can also validate the client (user) by requesting the user's certificate, which includes the client’s public key and CA information. However, this process, known as mutual TLS (mTLS), is not always configured on web servers for standard user-facing applications due to its complexity. Most web servers do not require client certificates because it adds an extra step for users and is not always user-friendly. When mutual authentication is required, it is typically set up behind the scenes, often without the user’s explicit awareness. This type of configuration is more common in enterprise environments or high-security applications where both parties must authenticate each other.

In standard web transactions, user authentication is usually managed through traditional login mechanisms (username and password, OTP, etc.) rather than requiring client certificates, simplifying the user experience while maintaining security.


## Key Takeaways

- **Initial Trust Establishment**: Asymmetric encryption is primarily used during the initial connection to establish trust between Jeevan’s browser and the bank’s server. This process involves validating the server’s certificate and securely exchanging the session key.

- **Efficiency of Symmetric Encryption**: After the secure exchange of the session key, symmetric encryption takes over for the remainder of the session. It is much faster and less resource-intensive than asymmetric encryption, making it suitable for ongoing data exchange.

- **Security and Speed**: The combination of asymmetric encryption for key exchange and symmetric encryption for data transmission provides both security and efficiency.

