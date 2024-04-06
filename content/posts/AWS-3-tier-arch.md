---
title: AWS Typical 3 Tier Solution Architecture
date: 2024-04-06
tags: 
cover:
  image: img/aws-3-tier-arch.drawio.svg

---

The above picture shows the classic 3 tier solution architecture in AWS manner.This solution well solves problems such as disaster recovery, failover, load balancing, and network domain separation.

Below is the detailed description of tools using in the solution.

- Route 53:  Amazon Route 53 is a highly available and scalable Domain Name System (DNS) web service. It has health check abilitiy and failover solution. By using Route 53, you can fine-tune the DNS route with continuously high avaliablilty. 

- ELB: Elastic load balancer, including application load balancer, network load balancer and gateway load balancer. Just like its name， load balancer mainly focus on load balancing, it will dynamically allocate the server load based on your settting. They also have health check function which will automatically failover when server down.

- Auto Scalling Group: An Auto Scaling group contains a collection of EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management. Auto scalling group can sacle in and scale out between minimum and maximum capacity based on needs. Besides, they have abilty to terminate the unheathy instance and boot a new one automatically.

- M5: One of the instance type in AWS EC2 

- Elastic Cache: An memory based database which will store the data based on  policy(TTL, write through,Lazy loading). When Cache hit, the server will retrieve data directly from cache,which greatly improving retrieval speed.

- RDS: AWS relational database service, with some cool features like read replica and multi AZ, which will maintain high speeed and avaliablity. 