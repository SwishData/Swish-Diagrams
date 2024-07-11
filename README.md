# Swish-Diagrams
Repo for common diagrams we use in Engineering discussions with clients.  Most are created with draw.io or with plantuml in VSCode or another IDE.  Feel free to create your own or submit a request to suggest a new diagram.

## TCP Three Way Handshake Diagram

```mermaid
sequenceDiagram
    participant Client
    participant Server
    Client->>Server: SYN
    Server-->>Client: SYN+ACK
    Client->>Server: ACK
```

In this diagram, the client initiates the TCP connection by sending a SYN packet to the server. 
The server responds with a SYN+ACK packet, indicating its willingness to establish a connection. 
Finally, the client sends an ACK packet to acknowledge the server's response, completing the three-way handshake process and establishing a TCP connection between the client and the server.

## HTTPS Diagram

```mermaid
    sequenceDiagram
    participant Client
    participant Server
    Client->>Server: Client Hello
    Server-->>Client: Server Hello
    Server-->>Client: Certificate, Server Key Exchange, Server Hello Done
    Client->>Server: Certificate Verification
    Client->>Server: Client Key Exchange, Change Cipher Spec, Finished
    Server-->>Client: Change Cipher Spec, Finished
    Note over Client,Server: Data Exchange
```

In this diagram, the client initiates the HTTPS connection by sending a Client Hello message to the server, indicating the TLS version and preferred cryptographic algorithms. The server responds with a Server Hello message, sending its certificate, server key exchange message, and server hello done message. 
The client then conducts certificate verification to ensure that the server is authentic. The client generates a random cryptographic key, encrypts it using the server’s public key, and sends it to the server in the Client Key Exchange message along with a Change Cipher Spec message indicating that for all future messages, encryption will used. 
The server responds by also sending a Change Cipher Spec message and encrypted Finished message. If this is correct, the client responds with its own Change Cipher Spec and encrypted Finished message. Once the handshake is completed, both client and server can now exchange data securely. 
You can use the Mermaid syntax to create an HTTPS handshake diagram to track the messages sent between the client and server when establishing a secure connection.

## TCP Proxy Diagram

```mermaid
sequenceDiagram
    participant Client
    participant Proxy
    participant OriginServer
    Client->>Proxy: SYN
    Proxy-->>Client: SYN+ACK
    Client->>Proxy: ACK
    Client->>Proxy: HTTP Request
    Proxy->>OriginServer: SYN
    OriginServer-->>Proxy: SYN+ACK
    Proxy->>OriginServer: ACK
    Proxy->>OriginServer: HTTP Request
    OriginServer-->>Proxy: HTTP Response
    Proxy-->>Client: HTTP Response
    Client->>Proxy: ACK
```

In this diagram, a client initiates a TCP connection with the proxy (like Cloudflare) by sending a SYN packet. The proxy responds with a SYN+ACK packet, indicating it received the request. The client then acknowledges the proxy's response with an ACK packet. 

Once the TCP connection is established, the client sends an HTTP request to the proxy. The proxy, acting as an intermediary, establishes a separate TCP connection with the origin server (like Apache) by sending a SYN packet. The origin server responds with a SYN+ACK packet, and the proxy acknowledges it with an ACK packet.

Next, the proxy forwards the HTTP request to the origin server, which processes it and generates an HTTP response. The origin server sends the HTTP response back to the proxy. Lastly, the proxy forwards the HTTP response to the client. The client acknowledges the receipt of the response with an ACK packet.

This diagram represents a typical TCP proxied session where the client communicates with a proxy, and the proxy communicates with an origin server, allowing for enhanced security, caching, load balancing, or other reasons to route traffic through a proxy.

## SAML Authentication

'''mermaid
sequenceDiagram
    participant User
    participant IdentityProvider
    participant ServiceProvider

    User->>ServiceProvider: Request to access protected resource
    ServiceProvider->>IdentityProvider: Redirect to login page
    IdentityProvider->>User: Display login page
    User->>IdentityProvider: Provide credentials
    IdentityProvider->>IdentityProvider: Verify credentials
    IdentityProvider->>ServiceProvider: Generate SAML assertion
    ServiceProvider->>User: Redirect to access protected resource
    User->>ServiceProvider: Provide SAML assertion
    ServiceProvider->>IdentityProvider: Validate SAML assertion
    IdentityProvider->>ServiceProvider: Confirmation
    ServiceProvider->>User: Access to protected resource granted
'''

In this diagram, the user initiates a request to access a protected resource on the service provider's website.
The service provider redirects the user to the identity provider's website to initiate the SAML authentication process.
The identity provider displays the login page to the user.
The user provides their login credentials to the identity provider.
The identity provider verifies the user's credentials.
The identity provider generates a SAML assertion, which contains information about the user's identity and authentication status.
The service provider receives the SAML assertion and grants the user access to the protected resource.
The user is redirected back to the service provider's website.
The user provides the SAML assertion to the service provider.
The service provider validates the SAML assertion to make sure it comes from an authentic identity provider.
The identity provider confirms the user's authentication to the service provider.
The service provider grants the user access to the protected resource.
