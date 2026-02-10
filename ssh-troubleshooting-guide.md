# SSH Connection Troubleshooting Guide

A simple guide to quickly identify and resolve common SSH connection issues when working with your EC2 instance.

## Decision Tree

1. **Can you ping the instance?**
   - ❌ No → Make sure the instance is running and the public IP is correct.
   - ✅ Yes → Proceed to port check.

2. **Does `nc -zv IP 22` connect?**
   - ❌ No → Verify your security group allows inbound SSH (port 22) from your IP.
   - ✅ Yes → Proceed to SSH attempt.

3. **What error do you get when SSH’ing?**
   - "Permission denied" → Check that the correct key file and username are used.
   - "Connection refused" → Make sure the SSH service is running on the EC2 instance.
   - "Connection timed out" → Double-check security groups, network ACLs, and firewall rules.
   - "Host key verification failed" → Remove the old host key from `~/.ssh/known_hosts`:
     ```bash
     ssh-keygen -R <IP_ADDRESS>
     ```

## Quick Checks & Commands

```bash
# Verify key permissions
ls -l ~/.ssh/bootcamp-week2-key.pem

# Verify correct key and user
ssh -i ~/.ssh/bootcamp-week2-key.pem ec2-user@YOUR_PUBLIC_IP

# Check security group rules
aws ec2 describe-security-groups --group-ids sg-xxxxx

# Test port connectivity
nc -zv YOUR_PUBLIC_IP 22

# SSH with verbose output
ssh -vvv bootcamp-web 2>&1 | tee ssh-debug.log

