
# ELK Stack Deployment Models

## Single Node Deployment

All components run on a single machine.

Suitable for:

- Learning environments
- Testing & labs
- Small workloads

Limitations:

- No fault tolerance
- Limited scalability
- Performance constraints

---

## Multi Node / Cluster Deployment

Elasticsearch nodes distributed across infrastructure.

Benefits:

- High availability
- Fault tolerance
- Horizontal scaling
- Improved performance

Used in production SOC environments.

---

## Elasticsearch Node Roles

Common node types:

- Master Node → Cluster coordination
- Data Node → Stores indexed data
- Ingest Node → Pre-processing pipelines

Separating roles improves cluster efficiency.

---

## Cloud vs On-Prem Deployment

ELK can be deployed:

- On-premises (self-managed)
- Cloud-hosted (managed services)

Trade-offs include cost, control, and maintenance complexity.

---

## Key Takeaways

- Single node deployments suit labs
- Cluster deployments suit production
- Node roles affect scalability & reliability

