#Useful Daigrams for IT Teams

##TCP Three Way Handshake

```mermaid
sequenceDiagram
    participant Client
    participant Server

    Client->>Server: SYN
    Server-->>Client: SYN+ACK
    Client->>Server: ACK
'''

##HTTPS Handshake

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
'''

In this diagram, the client initiates the HTTPS connection by sending a Client Hello message to the server, indicating the TLS version and preferred cryptographic algorithms. The server responds with a Server Hello message, sending its certificate, server key exchange message, and server hello done message.

The client then conducts certificate verification to ensure that the server is authentic. The client generates a random cryptographic key, encrypts it using the server’s public key, and sends it to the server in the Client Key Exchange message along with a Change Cipher Spec message indicating that for all future messages, encryption will used.

The server responds by also sending a Change Cipher Spec message and encrypted Finished message. If this is correct, the client responds with its own Change Cipher Spec and encrypted Finished message. Once the handshake is completed, both client and server can now exchange data securely.

You can use the Mermaid syntax to create an HTTPS handshake diagram to track the messages sent between the client and server when establishing a secure connection.

##TCP Proxy

'''mermaid
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
'''

In this diagram, a client initiates a TCP connection with the proxy (like Cloudflare) by sending a SYN packet. The proxy responds with a SYN+ACK packet, indicating it received the request. The client then acknowledges the proxy's response with an ACK packet.

Once the TCP connection is established, the client sends an HTTP request to the proxy. The proxy, acting as an intermediary, establishes a separate TCP connection with the origin server (like Apache) by sending a SYN packet. The origin server responds with a SYN+ACK packet, and the proxy acknowledges it with an ACK packet.

Next, the proxy forwards the HTTP request to the origin server, which processes it and generates an HTTP response. The origin server sends the HTTP response back to the proxy. Lastly, the proxy forwards the HTTP response to the client. The client acknowledges the receipt of the response with an ACK packet.

This diagram represents a typical TCP proxied session where the client communicates with a proxy, and the proxy communicates with an origin server, allowing for enhanced security, caching, load balancing, or other reasons to route traffic through a proxy.
