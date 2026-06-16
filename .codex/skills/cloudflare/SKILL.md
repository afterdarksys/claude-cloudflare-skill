---
name: cloudflare
description: Manage Cloudflare infrastructure from Codex, including DNS records, zones, SSL/TLS, caching, firewall rules, IP access rules, Page Rules, Workers, zone settings, and analytics. Use when working with Cloudflare APIs, creating or modifying DNS records, managing domain security, purging cache, deploying Workers, or analyzing traffic with the bundled Cloudflare API scripts.
---

# Cloudflare Management

Use this skill to manage Cloudflare infrastructure through the Cloudflare API v4. Prefer the bundled scripts for supported operations because they centralize authentication, error handling, and Cloudflare response parsing.

## Authentication

The scripts read credentials from `~/cloudflare_global_key`.

Use a Cloudflare API token when possible:

```text
Bearer YOUR_API_TOKEN_HERE
```

Legacy global API keys are partially supported, but API tokens are preferred because they can be scoped to the minimum required permissions.

Verify credentials before making changes:

```bash
./scripts/cf-api.sh verify-token
```

## Workflow

1. Confirm the target account, zone, DNS record, Worker, or setting before making destructive or production-impacting changes.
2. Use read/list commands first to resolve zone IDs and current state.
3. For writes, prefer the most specific script command available instead of raw API requests.
4. Show the Cloudflare API result or a concise summary after changes.
5. Never expose API tokens or credential file contents in the final response.

## Scripts

All scripts are in `scripts/` relative to this skill directory:

| Script | Purpose |
| --- | --- |
| `cf-api.sh` | Core Cloudflare API client and raw requests |
| `zones.sh` | Zone listing, lookup, creation, deletion, and activation checks |
| `dns.sh` | DNS record CRUD operations |
| `ssl.sh` | SSL/TLS modes, minimum TLS, Always Use HTTPS, and HSTS |
| `cache.sh` | Cache purge and cache settings |
| `firewall.sh` | Firewall rule management |
| `ip-access.sh` | IP access block/allow/challenge rules |
| `page-rules.sh` | Page Rules management |
| `workers.sh` | Worker listing, deployment, retrieval, deletion, and subdomain state |
| `analytics.sh` | Zone analytics and DNS analytics |
| `zone-settings.sh` | Zone-level settings |

Read `reference.md` when endpoint details, response shapes, or argument examples are needed.

## Common Commands

List zones:

```bash
./scripts/zones.sh list
```

Find a zone ID by name:

```bash
./scripts/zones.sh get-by-name example.com --id-only
```

List DNS records:

```bash
./scripts/dns.sh list <zone_id>
```

Create a proxied A record:

```bash
./scripts/dns.sh create <zone_id> --type A --name api --content 192.0.2.1 --ttl 3600 --proxied true
```

Set strict SSL:

```bash
./scripts/ssl.sh set-mode <zone_id> strict
```

Purge all cache:

```bash
./scripts/cache.sh purge-all <zone_id>
```

Deploy a Worker:

```bash
./scripts/workers.sh deploy <script_name> <script_file>
```

## Templates

Use `templates/` for starter payloads and examples:

- `dns-records.json` - common DNS record patterns
- `firewall-rules.json` - firewall expression examples
- `page-rules.json` - Page Rule examples
- `worker-examples.js` - Worker script examples

## Safety

- Treat DNS, SSL/TLS, firewall, cache purge, and Worker deployment operations as production-impacting.
- Prefer API tokens with only the required Cloudflare permissions.
- Do not commit or print credentials.
- For ambiguous requests that could affect multiple zones or records, resolve ambiguity before writing.
