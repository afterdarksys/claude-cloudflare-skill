# Cloudflare Skill for Claude Code

**Created by After Dark Systems, LLC**

A comprehensive Claude Code skill for managing Cloudflare infrastructure. This skill provides full control over DNS, zones, SSL/TLS, caching, firewall rules, Workers, and analytics through the Cloudflare API v4.

## Features

- **Zone Management** - Create, list, and manage Cloudflare zones (domains)
- **DNS Management** - Full CRUD operations for all DNS record types
- **SSL/TLS Configuration** - Manage encryption modes, TLS versions, HSTS
- **Cache Control** - Purge cache by URL, tags, prefixes, or completely
- **Firewall Rules** - Create and manage firewall expressions
- **IP Access Rules** - Block, allow, or challenge IPs, ranges, ASNs, countries
- **Page Rules** - Configure URL-based behavior rules
- **Workers** - Deploy and manage Cloudflare Workers
- **Analytics** - View traffic, bandwidth, threats, and DNS analytics
- **Zone Settings** - Configure all zone-level settings

## Quick Start

1. Install the skill (see [INSTALL.md](INSTALL.md))
2. Configure your Cloudflare API credentials
3. Use Claude Code naturally - the skill activates automatically when you ask about Cloudflare

### Example Conversations

```
You: List all my Cloudflare zones
You: Add an A record for api.example.com pointing to 192.0.2.1
You: Enable strict SSL mode for my domain
You: Purge the cache for example.com
You: Block IP 192.0.2.100 on my zone
You: Show me traffic analytics for the last 24 hours
```

## Available Scripts

| Script | Description |
|--------|-------------|
| `cf-api.sh` | Core API client with authentication |
| `zones.sh` | Zone management operations |
| `dns.sh` | DNS record management |
| `ssl.sh` | SSL/TLS settings |
| `cache.sh` | Cache purging and settings |
| `firewall.sh` | Firewall rules |
| `ip-access.sh` | IP access rules |
| `page-rules.sh` | Page rules management |
| `workers.sh` | Workers deployment |
| `analytics.sh` | Traffic and security analytics |
| `zone-settings.sh` | Zone settings management |

## API Coverage

This skill covers the major Cloudflare API v4 endpoints:

- `/zones` - Zone management
- `/zones/{id}/dns_records` - DNS records
- `/zones/{id}/settings/*` - Zone settings
- `/zones/{id}/purge_cache` - Cache purging
- `/zones/{id}/firewall/rules` - Firewall rules
- `/zones/{id}/firewall/access_rules` - IP access rules
- `/zones/{id}/pagerules` - Page rules
- `/zones/{id}/ssl/*` - SSL/TLS settings
- `/zones/{id}/analytics/*` - Analytics
- `/accounts/{id}/workers/*` - Workers

## Templates

The `templates/` directory includes ready-to-use configurations:

- `dns-records.json` - Common DNS record patterns (MX, SPF, DKIM, etc.)
- `firewall-rules.json` - Security rule templates
- `page-rules.json` - Common page rule configurations
- `worker-examples.js` - Example Worker scripts

## Requirements

- Bash 4.0+
- curl
- jq
- Cloudflare API Token or Global API Key

## Security

- Store API credentials securely
- Use API Tokens with minimal required permissions
- Never commit credentials to version control

## Documentation

- [INSTALL.md](INSTALL.md) - Installation instructions
- [.claude/skills/cloudflare/reference.md](.claude/skills/cloudflare/reference.md) - Full API reference

## License

MIT License - See LICENSE file

## Support

For issues with this skill, contact After Dark Systems, LLC.

For Cloudflare API documentation: https://developers.cloudflare.com/api/
