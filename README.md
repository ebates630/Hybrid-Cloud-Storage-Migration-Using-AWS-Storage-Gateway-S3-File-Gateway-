# Hybrid Cloud Storage Migration Using AWS Storage Gateway (S3 File Gateway)

## Project Overview
This project demonstrates how a company can migrate file-based data from an on-premises Linux environment into AWS while maintaining existing NFS-based workflows. The goal was to create a hybrid storage solution that allows users and systems to continue interacting with files as usual, while leveraging Amazon S3 for durable, scalable cloud storage.

This type of architecture is commonly used in organizations modernizing legacy systems, building cloud-based data lakes, or centralizing data for analytics.

---

## Business Problem
The organization relied on a local Linux file server to store operational files (such as images, reports, and exports). This approach created challenges with scalability, durability, and disaster recovery. The business needed a way to move data into AWS without rewriting applications or disrupting existing file-based processes.

---

## Solution
I designed and implemented a hybrid architecture using AWS Storage Gateway (S3 File Gateway) to expose an NFS file share backed by Amazon S3. This allowed the Linux environment to mount cloud storage as if it were a local file system.

To ensure resiliency and long-term maintainability, I also implemented Amazon S3 versioning, lifecycle management, and cross-Region replication.

---

## Architecture Summary
- Linux environment mounted an NFS file share
- AWS Storage Gateway served as the hybrid bridge between on-prem systems and AWS
- Primary Amazon S3 bucket stored the migrated files
- Secondary Amazon S3 bucket replicated data automatically using Cross-Region Replication (CRR)

Data Flow:
Linux → NFS Mount → S3 File Gateway → S3 Source Bucket → CRR → S3 Replica Bucket

---

## AWS Services Used
- AWS Storage Gateway (S3 File Gateway)
- Amazon S3 (Versioning, Lifecycle Policies, Cross-Region Replication)
- AWS Identity and Access Management (IAM)
- Amazon EC2

---

## Implementation Steps

### 1. S3 Storage Foundation
- Created a primary S3 bucket with versioning enabled
- Created a secondary S3 bucket in another region with versioning enabled
- Configured Cross-Region Replication between the two buckets

### 2. Storage Gateway Deployment
- Deployed and activated an S3 File Gateway appliance
- Configured local cache storage for performance
- Attached IAM permissions to securely allow the gateway to write to S3

### 3. File Share Configuration
- Created an NFS file share mapped to the primary S3 bucket
- Configured access settings for Linux connectivity

### 4. Data Migration
- Mounted the NFS file share on the Linux server
- Migrated files into the mounted directory
- Verified that files were successfully written into Amazon S3

### 5. Validation
- Confirmed file presence in the source S3 bucket
- Verified automatic replication into the secondary S3 bucket
- Ensured expected object counts and file availability

---

## Why This Project Matters (Data + Cloud Perspective)
This project reflects a real-world pattern used before analytics work even begins. Analysts and data teams depend on reliable, centralized, and durable data storage. This solution demonstrates how raw files can be ingested into AWS, protected with replication and versioning, and prepared to support downstream analytics workflows such as ETL pipelines, dashboards, and machine learning systems.

---

## Tools & Skills Demonstrated
Hybrid Cloud Architecture, AWS Storage Gateway, Amazon S3, Cloud Data Ingestion, Data Migration, Cross-Region Replication, Lifecycle Management, IAM, Linux, Infrastructure Fundamentals

---

## Future Improvements
- Automate S3 and IAM configuration using Terraform or AWS CDK
- Enable CloudWatch monitoring and alerts
- Add encryption key management with AWS KMS
- Build a simple ingestion pipeline that loads S3 data into an analytics tool

---

## Summary
This project demonstrates my ability to design and implement a hybrid storage solution that moves operational data into AWS securely and reliably, while laying the groundwork for cloud-based analytics and data platforms.
