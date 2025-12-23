# Installation Guide

## Prerequisites

- [Claude Code](https://claude.com/claude-code) installed and configured
- Cloudflare account with API access
- Bash 4.0+, curl, and jq installed

## Step 1: Clone or Copy the Skill

### Option A: Clone Repository
```bash
git clone https://github.com/YOUR_USERNAME/claude-cloudflare-skill.git
cd claude-cloudflare-skill
```

### Option B: Copy to Existing Project
```bash
cp -r .claude/skills/cloudflare /path/to/your/project/.claude/skills/
```

### Option C: Install Globally (All Projects)
```bash
cp -r .claude/skills/cloudflare ~/.claude/skills/
```

## Step 2: Configure Cloudflare Credentials

Create a credentials file at `~/cloudflare_global_key`:

```bash
touch ~/cloudflare_global_key
chmod 600 ~/cloudflare_global_key
```

Add your Cloudflare API Token:

```
Bearer YOUR_API_TOKEN_HERE
```

Or use Global API Key (legacy):

```
YOUR_GLOBAL_API_KEY
```

### Creating an API Token

1. Log in to Cloudflare Dashboard
2. Go to **My Profile** > **API Tokens**
3. Click **Create Token**
4. Use the **Edit zone DNS** template or create a custom token
5. Add permissions as needed:
   - Zone:DNS:Edit (for DNS management)
   - Zone:Zone:Read (for zone listing)
   - Zone:Zone Settings:Edit (for settings)
   - Zone:Firewall Services:Edit (for firewall)
   - Zone:Cache Purge:Purge (for cache)
   - Account:Workers Scripts:Edit (for Workers)

## Step 3: Make Scripts Executable

```bash
chmod +x .claude/skills/cloudflare/scripts/*.sh
```

## Step 4: Verify Installation

Test that the skill is working:

```bash
# Verify API token
.claude/skills/cloudflare/scripts/cf-api.sh verify-token

# List zones
.claude/skills/cloudflare/scripts/zones.sh list
```

## Step 5: Start Using

Open Claude Code and start asking about Cloudflare. The skill will activate automatically:

```
You: Show me my Cloudflare zones
You: Add an A record for www.example.com
You: What's the SSL mode for example.com?
```

## Troubleshooting

### "Command not found" Error
Make sure scripts are executable:
```bash
chmod +x .claude/skills/cloudflare/scripts/*.sh
```

### Authentication Errors
1. Verify your token is valid:
   ```bash
   curl "https://api.cloudflare.com/client/v4/user/tokens/verify" \
     -H "Authorization: Bearer YOUR_TOKEN"
   ```
2. Check file permissions: `chmod 600 ~/cloudflare_global_key`
3. Ensure the token has required permissions

### jq Not Found
Install jq:
- macOS: `brew install jq`
- Ubuntu/Debian: `sudo apt install jq`
- RHEL/CentOS: `sudo yum install jq`

### Skill Not Activating
1. Verify the skill is in the correct location:
   - Project: `.claude/skills/cloudflare/SKILL.md`
   - Global: `~/.claude/skills/cloudflare/SKILL.md`
2. Check SKILL.md has valid YAML frontmatter
3. Restart Claude Code

## Directory Structure

```
.claude/skills/cloudflare/
├── SKILL.md              # Skill manifest
├── reference.md          # API reference
├── scripts/
│   ├── cf-api.sh        # Core API client
│   ├── zones.sh         # Zone management
│   ├── dns.sh           # DNS records
│   ├── ssl.sh           # SSL/TLS
│   ├── cache.sh         # Cache management
│   ├── firewall.sh      # Firewall rules
│   ├── ip-access.sh     # IP access rules
│   ├── page-rules.sh    # Page rules
│   ├── workers.sh       # Workers
│   ├── analytics.sh     # Analytics
│   └── zone-settings.sh # Zone settings
└── templates/
    ├── dns-records.json
    ├── firewall-rules.json
    ├── page-rules.json
    └── worker-examples.js
```

## Updating

To update the skill:

```bash
cd claude-cloudflare-skill
git pull origin main
```

## Uninstalling

Remove the skill directory:

```bash
# Project installation
rm -rf .claude/skills/cloudflare

# Global installation
rm -rf ~/.claude/skills/cloudflare
```
