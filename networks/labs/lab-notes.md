# AWS Labs Notes

## Networking Lab: Internet Protocols - Public and Private IP addresses

### Objective
- Investigate why one EC2 instance cannot reach the internet while another can.
- Test connectivity using SSH.
- Provide guidance on using public vs. private CIDR ranges when creating a VPC.

---

### Steps Taken
1. Logged into the **AWS Console** → navigated to **EC2 service**.
2. Viewed **Instance A** and **Instance B** details:
    - Instance A → only had a **private IP address**.
    - Instance B → had both a **private** and a **public IP address**.
3. Compared the networking settings → confirmed architecture (VPC, subnet, IGW, route tables) was correct.
4. Downloaded the **labsuser.pem** key pair.
5. Attempted SSH connection:
   ```bash
   ssh -i labsuser.pem ec2-user@<public-ip>
   ```
   - Could connect to Instance B (because it had a public IP).
   - Could not connect to Instance A (private IP only).
6. Reviewed customer’s question on using 12.0.0.0/16 as a VPC CIDR.
