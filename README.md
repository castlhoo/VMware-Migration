# VMware Migration Guide

## Table of Contents
1. [vMotion Overview](#vmotion-overview)
2. [vMotion Features](#vmotion-features)
3. [How vMotion Works](#how-vmotion-works)
4. [Requirements for vMotion](#requirements-for-vmotion)
5. [vMotion Setup Guide](#vmotion-setup-guide)
6. [vMotion EVC (Enhanced vMotion Compatibility)](#vmotion-evc)
7. [Conclusion](#conclusion)

## vMotion Overview

vMotion is a powerful feature provided by VMware that enables live migration of virtual machines (VMs) from one physical host to another without any downtime. This seamless migration ensures that business-critical applications remain available without interruption during maintenance or resource balancing.

![vMotion Overview](https://github.com/user-attachments/assets/de5965b5-1a57-4c1f-96de-ee893bd35b7f)

## vMotion Features

- **Zero Downtime**: Migrates VMs without service interruption, ideal for routine server maintenance.
- **Resource Optimization**: Enables dynamic balancing of resources across servers by moving VMs between hosts to avoid performance bottlenecks.
- **Flexibility**: Supports both intra-cluster and cross-cluster migrations.

## How vMotion Works

![vMotion Process Step 1](https://github.com/user-attachments/assets/f10986d7-d9bc-4a00-a3a6-cfac912eb0e4)
![vMotion Process Step 2](https://github.com/user-attachments/assets/5b948895-7fc0-4257-9365-a516b9036213)

1. **Shadow VM Creation**: A Shadow VM is created on the target host with the same configuration as the source VM.

2. **Pre-copy Phase**: The memory and running state of the source VM are copied in real-time to the Shadow VM.

3. **Memory Synchronization**: As copying nears completion, the source VM continues to run until there are very few changed memory pages.

4. **Final Copy**: The source VM is briefly paused, and remaining memory pages are copied to the target host.

5. **VM Restart and Network Connection**: The VM is restarted on the target host, and network connections are established.

6. **Minimal Ping Loss**: The VM's downtime is extremely short, resulting in ping loss of about 1–2 ms, which is almost imperceptible to clients.

## Requirements for vMotion

1. **Shared Storage**
   ![Shared Storage](https://github.com/user-attachments/assets/2fc25992-5ff8-4c9f-bd8c-c41702b47114)

2. **vMotion Network**
   ![vMotion Network](https://github.com/user-attachments/assets/90347402-24ad-4880-8f0f-7c0a087f70a6)

3. **CPU Compatibility**

## vMotion Setup Guide

### 1. Add Port Group in Distributed Switch for vMotion Network

![Add Port Group](https://github.com/user-attachments/assets/6306f9e4-7d7a-4ff7-84e0-2f3f92063396)

Complete setting for vMotion network:
![vMotion Network Setting](https://github.com/user-attachments/assets/cda3a7af-00af-45cf-b8d9-d9eeacd519d8)

Two hosts connected to vMotion Network:
![Hosts Connected](https://github.com/user-attachments/assets/8a486a03-04b9-464e-a47d-20b7ae5e8534)

### 2. Switch Setting for Host

![Switch Setting 1](https://github.com/user-attachments/assets/653368f7-f771-4ed8-a2ad-3349e709493c)
![Switch Setting 2](https://github.com/user-attachments/assets/b2540ce5-0cbc-4ed3-9430-616f9da49021)

Configure VMkernel and IP settings:
![VMkernel Config](https://github.com/user-attachments/assets/ebd98deb-41fe-4156-bff6-8998049f6911)
![IP Config](https://github.com/user-attachments/assets/3d9ca4e3-4c7b-45fb-a88a-ed86a084ab0a)

### 3. Setting vMotion Network in VM

![VM Network Setting 1](https://github.com/user-attachments/assets/5f4c5f16-c9f5-4167-ac4f-61abe65ca5f0)
![VM Network Setting 2](https://github.com/user-attachments/assets/647d56a9-438d-4d69-962f-073460dac587)

### 4. Migration

![Migration Types](https://github.com/user-attachments/assets/d825a87d-69ef-4997-a62e-ea818152dfb3)
![Migration Process](https://github.com/user-attachments/assets/bdcaf736-f6ca-40d1-99a7-2710bf01727c)

Four types of migration:
1. Compute resource (basic live migration)
2. Change storage only
3. Combined compute resource and storage migration
4. Migration between vCenter servers

![Migration Network](https://github.com/user-attachments/assets/43c0aa02-ffec-42fe-ab28-afb8a8ace99c)

## vMotion EVC

Enhanced vMotion Compatibility (EVC) allows vMotion between hosts with different CPU generations.

![EVC Concept](https://github.com/user-attachments/assets/b346d2e6-0296-4bf6-b8d8-3ecfe1f54186)

### Advantages and Disadvantages of EVC

**Advantages:**
- Supports various CPU types
- Allows gradual upgrades without purchasing all CPUs at once

**Disadvantages:**
- Limited to CPUs that pass the compatibility check
- Cannot fully utilize the newest CPU features on hosts with the latest CPUs

### EVC Setup

1. Check Compatibility Guide
   ![Compatibility Guide](https://github.com/user-attachments/assets/9c6db450-d2cc-4c9f-8fe8-61cd05477031)

2. Set CPU mode
   ![CPU Mode Setting](https://github.com/user-attachments/assets/79a4798c-901b-4030-a088-db30bbf7054c)

3. Complete Setup
   ![EVC Setup Complete](https://github.com/user-attachments/assets/f192b94b-ff96-4372-9d6a-82ac0bf5d26c)

## Conclusion

In this guide, we've explored vMotion and EVC, crucial features for VMware environments. We've learned how to:

- Perform live migration using vMotion
- Set up vMotion networks and configurations
- Understand and implement EVC for CPU compatibility

These technologies enable flexible and efficient management of virtual environments, allowing for seamless maintenance and resource optimization.
