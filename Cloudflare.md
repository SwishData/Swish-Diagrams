# Cloudflare Diagrams

## Basic Connection

```mermaid
    flowchart LR
        Visitor<-- Connection -->OriginServer
```

## Proxied Connection

```mermaid
    flowchart LR
        Visitor<-- Connection 1 -->CloudflareGlobalNetwork<-- Connection 2 -->OriginServer
```

## Proxied Connection

```mermaid
    flowchart LR
        Browser<-- Connection 1 -->Cloudflare<-- Connection 2 -->OriginServer
```
