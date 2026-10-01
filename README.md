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

## Production HTTPS preparation

Production ingress configuration is prepared but is not currently active.

The normal `compose.yml` publishes no Caddy host ports.

Production public port mappings are stored separately in
`compose.production.yml`.

`Caddyfile.production` contains the production reverse-proxy configuration.

The production hostname is supplied through the local `.env` file.
`.env` is excluded from Git. `.env.example` documents the required variable.

Before production activation:

1. Obtain the production hostname.
2. Point its public DNS records to this VPS.
3. Set `DOMAIN` in `.env`.
4. Set Iomad's canonical URL to the HTTPS production hostname.
5. Review Moodle/Iomad reverse-proxy HTTPS configuration.
6. Activate the production Caddyfile.
7. Publish Caddy's production ports.
8. Permit the required ports through the Hostinger firewall.
9. Verify automatic TLS certificate issuance.
10. Verify HTTP redirects to HTTPS.
11. Verify login and administrative traffic over HTTPS.
12. Verify the application is not available over public plaintext HTTP.
