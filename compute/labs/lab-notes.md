# AWS Labs Notes

## Compute Lab: Amazon EC2

### Objective
Learn how to launch and connect to an EC2 instance.

### Steps Taken
1. Logged into AWS Console
2. Launched an **EC2 instance** (Ubuntu AMI)
3. Generated and downloaded a **key pair** (.pem file)
4. Configured **security group** with required inbound rules (port 22 for SSH)
5. SSH’d into the instance using terminal command:
   ```bash
   ssh -i "key.pem" ubuntu@<public-ip>
   ```

### Challenges
- Initially forgot to open port 22 → solved by editing inbound rules

### Screenshot
_(Optional – paste image if available)_

### Takeaways
- **Security groups** act like firewalls controlling inbound/outbound traffic.
- Always configure ports correctly before connecting (e.g., port 22 for SSH).
- EC2 provides resizable compute capacity in the cloud.
