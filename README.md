# AWS ECS Proof of Concept

Using this repo as a proving ground for testing various HA/non-HA/sharded deployment configurations for Invar with ECS.

The assumption is that we can use ECS-managed EC2 instances in a family with direct-attached NVMe disks to colocate Invar with the existing workload to eliminate NIC-imposed bandwidth bottlenecks and eliminate network latency + egress costs on lookup.

## Assumed request path

```mermaid
flowchart LR
    Client[External Client] --> ALB[Application Load Balancer]
    ALB --> ECS[ECS Task]
    ECS --> Cache[ElastiCache / Valkey]
    ECS --> DB[(PostgreSQL)]

    style Client fill:#e8f0fe,stroke:#4285f4,color:#111
    style ALB fill:#e8f0fe,stroke:#4285f4,color:#111
    style ECS fill:#fff3cd,stroke:#d6a323,color:#111
    style Cache fill:#d4edda,stroke:#28a745,color:#111
    style DB fill:#e8daef,stroke:#7b2cbf,color:#111
```
