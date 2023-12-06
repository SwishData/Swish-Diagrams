# Cloudflare Diagrams

## Basic Connection

```mermaid
    flowchart LR
        Visitor<-- Connection -->OriginServer
```

## Proxied Connection

```mermaid
    flowchart LR
        Visitor<-- Connection -->CloudflareGlobalNetwork<-- Connection -->OriginServer
```
