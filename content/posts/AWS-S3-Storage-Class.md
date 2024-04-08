---
title: AWS S3 Storage Class
date: 2024-04-08
tags: 
cover:
  image: img/aws-s3.svg
---
> Bucket Bucket Bucket

# Standard Classes

## S3 Standard - General Purpose
- 99.99% avaliability
- Used for frequent accessed data
- Low latency and high throughput
> Usage: Big data analytics, mobile & gaming applications, content distribution...

## Standard - Infrequent Access
- For data that is less frequently accessed, but requires rapud acess when needed
- Lower cost than S3 standard 

## Intelligent Tiering
- Moves objects automatically between Access Tiers based on usage
> Usage: Unknown or changing access

## One-Zone IA
- Work only in single AZ; data lost when AZ is destroyed 
- 99.5% avaliabity
> Usage: Storing secondary backup copies of on-premise data, or data you can recreate

--------

# Glacier Storage Classes 
- Low-cost object storage meant for archiving / backup
-  Pricing: price for storage + object retrieval cost


## Glacier Instant Retrieval
- Millisecond retrieval, great for data accessed once a quarter
- Minimunm storage duration of 90 days
## Glacier Flexible Retrieval
- Expedited (1 to 5 minutes) , Standar (3 to 5 hours), Bulk( 5 to 12 hours) -free
- Minimum storage duration of 90 days 
## Glacier Deep Archive
- Standard(12 hours), Bulk(48 hours)
- Minimum storage duration of 180 days



> All bucket have 99.99999999999% durability
