# aws-ip-ranges

Automated tracking of AWS public IP address ranges with version-controlled history.

## Overview

This repository automatically fetches and commits daily snapshots of AWS's official IP address ranges from [ip-ranges.amazonaws.com](https://ip-ranges.amazonaws.com/ip-ranges.json). Each update is tagged, creating a full audit trail of AWS infrastructure changes over time.

## What's Tracked

The `ip-ranges.json` file contains:

- **IPv4 and IPv6 prefixes** — All public IP ranges used by AWS
- **Regions** — Geographic region for each prefix (e.g., `us-east-1`, `eu-west-1`)
- **Services** — AWS service using the range (e.g., `EC2`, `S3`, `CLOUDFRONT`, `AMAZON`)
- **Network border groups** — Logical groupings for network traffic routing

## Use Cases

- **Firewall rules** — Allowlist AWS services by IP range
- **Security auditing** — Track when new IP ranges are added or removed
- **Network planning** — Monitor AWS infrastructure expansion
- **Compliance** — Maintain historical records of AWS IP allocations

## How It Works

1. **GitHub Actions** runs daily at 12:12 AM UTC (`.github/workflows/scrape.yaml`)
2. **scrape.sh** downloads the latest `ip-ranges.json` from AWS
3. If changes are detected, a new commit and tag are created automatically

## Manual Update

To fetch the latest IP ranges manually:

```bash
./scrape.sh
```

## References

- [AWS IP address ranges documentation](https://docs.aws.amazon.com/vpc/latest/userguide/aws-ip-ranges.html)
- [IP ranges JSON syntax](https://docs.aws.amazon.com/vpc/latest/userguide/aws-ip-syntax.html)
