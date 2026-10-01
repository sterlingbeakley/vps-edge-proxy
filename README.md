# VPS Edge Proxy

Shared Caddy reverse proxy for public web applications on this VPS.

## Architecture

Caddy is the only application intended to expose public HTTP/HTTPS ports.

Application frontend containers join the external Docker network named
`edge`. Databases, caches, and other backend services remain on their
application-specific private networks.

## Current status

Caddy is configured for private reverse-proxy testing only.

No Caddy ports are currently published to the VPS host.

Iomad remains directly accessible over its existing Tailscale-only
listener during setup.

## Production

When production DNS is available:

- Configure the production hostname.
- Configure Iomad's canonical URL for HTTPS.
- Publish the required Caddy HTTPS ports.
- Permit the required ports through the VPS firewall.
- Verify certificate issuance and HTTPS before public use.
