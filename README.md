# 🌏 AWS Multi-Region Architecture — CVL Cloud

> 8-phase migration to dual-region AWS infrastructure
> Mumbai (ap-south-1) + Hyderabad (ap-south-2)
> Zero data loss | RPO: 15 min | RTO: 1 hour

## 🏗️ Architecture
On-Premises DC
Palo Alto Firewall
↓
Site-to-Site VPN
↓
┌──────┴──────────────┐
│                     │
AWS ap-south-1        AWS ap-south-2
Mumbai (Primary)      Hyderabad (DR)
Application         - AWS DRS Replica
RDS Primary         - RDS Read Replica
S3 Versioned        - S3 Replication

## 🗓️ Migration Phases

| Phase | Activity | Timeline |
|---|---|---|
| 1 | Assessment + dependency mapping | Week 1-2 |
| 2 | VPC, subnets, security groups | Week 2-3 |
| 3 | Site-to-Site VPN + Palo Alto | Week 3-4 |
| 4 | Data migration (replication first) | Week 4-6 |
| 5 | Application migration | Week 6-9 |
| 6 | AWS DRS setup + DR testing | Week 9-10 |
| 7 | Cutover (4-hour window) | Week 11 |
| 8 | Decommission + 30-day hypercare | Week 12-16 |

## ⚙️ Tech Stack

| Component | Technology |
|---|---|
| Cloud | AWS (ap-south-1, ap-south-2) |
| Firewall | Palo Alto |
| Connectivity | Site-to-Site VPN |
| Disaster Recovery | AWS DRS |
| Database | Amazon RDS (Multi-region) |
| Storage | Amazon S3 (Cross-region replication) |

## 📊 Results

- ✅ Zero data loss during migration
- ✅ RPO: 15 minutes
- ✅ RTO: 1 hour
- ✅ DR tested and verified pre-cutover
- ✅ Palo Alto east-west traffic policies enforced

## 🔑 Key Design Decisions

- **Replication before cutover** — data synced first, cutover last
- **Phase-wise approach** — rollback plan for every phase
- **DR tested before go-live** — not after
- **4-hour maintenance window** — minimal business disruption
