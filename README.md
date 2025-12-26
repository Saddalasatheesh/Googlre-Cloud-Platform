GCP Training Summary (Day 1 – Day 10)
Overview of Work Completed

This training covered core and advanced Google Cloud Platform (GCP) services including Compute, Networking, Storage, Databases, Messaging, Data Integration, and Serverless Architectures. Hands-on labs were performed using CLI tools, Cloud SQL, Firestore, Pub/Sub, BigQuery, and Cloud Functions.

Module-wise Topics Covered
Module	Key Topics & Activities
Compute	• GCP Compute Infrastructure (Regions & Zones)
• Virtual Machines using Compute Engine
• SSH Keys and OS Login
• Customer Identity using Identity Platform
• Images, Instance Templates & Shared Image Families
• RAID Configuration with Persistent Disks
• Startup Scripts & Metadata
• Load Balancing & Health Checks
• Managed Instance Groups (MIGs) & Autoscaling
• Cloud Monitoring, Logging & Alerting Policies
• App Engine & Cloud Run Monitoring
Networking	• VPC Networking Basics
• External (Public) IP Addresses
• Network Interfaces (NICs)
• VPC Firewall Rules
• Network Tags & Service Accounts
• VPC Flow Logs
• Bastion Host & IAP TCP Forwarding
• VPC Routes & Cloud Router (BGP)
Storage	• Cloud Storage (Object Storage)
• Persistent Disk & Hyperdisk (Block Storage)
• Pub/Sub & Firestore (Queue & Table Storage)
• Cloud Tasks
• Storage Buckets & IAM Policies
• Filestore (Managed NFS)
• Partner Storage Services
• Disk Access Control
• Disk Encryption using CMEK
• Cloud Storage Browser & gsutil
Database (Firestore & NoSQL)	• SQL vs NoSQL Comparison
• Introduction to Firestore
• Firestore Setup & Execution
• Benefits and Use Cases of Firestore
• Serverless Integration (Cloud Functions & Cloud Run)
• Firestore Integration with GCP Services
• Why Firestore is Ideal for Serverless
• Managed Bigtable & Cassandra
• Limitations / Drawbacks of Firestore
GCP Service Mapping / Data Integration	• Cloud Data Integration Overview
• Importance of Data Integration in GCP
• Dataplex (Crawler & Metadata Discovery)
• Data Ingestion using Data Fusion & Dataflow
• Creating Control Flow & Data Flow
• Scheduling Pipelines with Cloud Scheduler
• Pipeline Monitoring using Cloud Monitoring & Logging
• Integration with GCP Data Services
RDS (Cloud SQL)	• Relational Database Concepts
• Relational Databases in GCP
• Cloud SQL Setup
• MySQL & PostgreSQL Interfaces
• DB Instances, Storage & Monitoring
• Event Notifications
• Database Access Control
• MySQL Features
• Creating Databases & Tables
• Database Connectivity
• Data Export & Import
Messaging in GCP	• Messaging Concepts & Benefits
• Messaging Options: Pub/Sub, Cloud Tasks, Eventarc
• Messaging Service Design Patterns
• Pub/Sub Basics & Architecture
• Eventarc Integration
• Streaming with Pub/Sub & Dataflow
• Real-time Messaging
• Publisher & Subscriber Model
• Queue vs Pub/Sub Comparison
• Message Attributes & Filtering
• Raw Message Delivery
• System-to-System Messaging
Command Line (CLI) Usage – GCP
Authentication & Configuration
gcloud auth login
gcloud config set project satheesh26
gcloud config set compute/region asia-south1

Enable Required Services
gcloud services enable pubsub.googleapis.com
gcloud services enable cloudfunctions.googleapis.com
gcloud services enable eventarc.googleapis.com
gcloud services enable run.googleapis.com
gcloud services enable bigquery.googleapis.com

Cloud SQL (MySQL)
cloud-sql-proxy.x64.exe satheesh26:asia-south1:satheeshdb --port 3307

mysql -h 127.0.0.1 -P 3307 -u satheeshdemo -p

USE management_system;

Pub/Sub
gcloud pubsub topics create satheesh26-events
gcloud pubsub topics list
gcloud pubsub subscriptions create satheesh26-events-sub --topic=satheesh26-events

BigQuery
bq mk --dataset --location=asia-south1 satheesh26events
bq ls
bq mk --table satheesh26events.user_events event:STRING,user:STRING,ts:TIMESTAMP
bq ls satheesh26events

Cloud Functions (Gen 2 Deployment)
gcloud functions deploy satheesh26-fn \
  --gen2 \
  --region=asia-south1 \
  --runtime=python310 \
  --source=. \
  --entry-point=on_user_create \
  --trigger-event-filters="type=google.cloud.firestore.document.v1.created" \
  --trigger-event-filters="database=satheesh26" \
  --trigger-event-filters-path-pattern="document=users/{docId}"
