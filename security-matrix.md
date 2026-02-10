# Security Configuration Matrix

## Instance Details
- Instance ID: i-xxxxxxxxxxxxx
- Instance Type: t3.micro
- Public IP: x.x.x.x
- Private IP: x.x.x.x

## Security Group: week2-web-server-sg

### Inbound Rules
| Protocol | Port | Source | Purpose | Risk Level |
|----------|------|--------|---------|------------|
| TCP | 22 | YOUR_IP/32 | SSH admin access | Low (restricted IP) |
| TCP | 80 | 0.0.0.0/0 | Public web traffic | Low (expected) |

### Outbound Rules
| Protocol | Port | Destination | Purpose |
|----------|------|-------------|---------|
| All | All | 0.0.0.0/0 | Unrestricted egress |

## Security Assessment
- ✅ SSH restricted to specific IP
- ✅ No unnecessary ports open
- ✅ HTTP enabled for web server purpose
- ⚠️ Consider: Restrict outbound traffic

## Recommendations
1. Add monitoring alerts for SSH attempts
2. Consider using Session Manager instead of SSH
3. Enable VPC Flow Logs
