# Swish-Diagrams
Repo for common diagrams we use in Engineering discussions with clients.  Most are created with draw.io or with plantuml in VSCode or another IDE.  Feel free to create your own or submit a request to suggest a new diagram.

##TCP Proxy Diagram

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
