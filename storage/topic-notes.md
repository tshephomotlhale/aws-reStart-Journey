# Storage Notes

## Types of Storage
- S3: Object storage
- EBS: Block storage for EC2
- EFS: Network file system

## Use Cases
- S3 for static websites and file backups
- EBS for app data (like databases)
- EFS for shared file access across instances

## Reflection
Understanding the difference between object and block storage helped me figure out when to use each service.

## Storage Lab: Amazon S3

### Objective
Learn how to create, upload, and manage objects in Amazon S3.

### Steps Taken
1. Logged into AWS Console
2. Navigated to **Amazon S3**
3. Created an **S3 bucket** with unique global name
4. Uploaded files (objects) into the bucket
5. Configured bucket permissions and object access

### Challenges
- Bucket naming rules (must be globally unique)
- Public access blocked by default, had to configure permissions for testing

### Screenshot
_(Optional – paste image if available)_

### Takeaways
- **Buckets** are global namespaces; names must be unique.
- **Objects** are files stored in S3.
- S3 provides durability and scalability but requires proper permission setup.

---