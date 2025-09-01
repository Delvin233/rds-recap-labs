# RDS Read Replica Testing

## 1. Replication Lag

- Observed replication lag between the primary (master) and read replica was typically **a few milliseconds to a couple of seconds**, depending on workload.  
- Heavy write operations can temporarily increase lag.  
- PostgreSQL lag tended to be slightly higher than MySQL under intense writes.

---

## 2. Writing to a Read Replica

- **Not allowed.** Read replicas are **read-only** by default.  
- Attempting to write results in an error (e.g., `ERROR: cannot execute INSERT in a read-only transaction`).  
- Writes must go to the primary; replicas are meant for offloading read traffic and analytics.

---

## 3. Cross-Region Replication & Data Transfer Costs

- Cross-region replication **incurs additional data transfer charges** because data is sent across AWS regions.  
- Intra-region replication is free.  
- Use cross-region replication primarily for **disaster recovery, geo-distribution, or global read performance**—not just for load balancing.

---

## 4. Use Cases for Promoting a Read Replica

- **Failover / High Availability:** If the primary fails, you can promote the replica to primary.  
- **Scaling Write Workloads:** In emergencies or migrations, replicas can temporarily become writable.  
- **Disaster Recovery:** Maintain a standby copy in another region.  
- **Testing / Analytics:** Promote a replica for reporting or testing without affecting production writes.

---

## 5. Personal Notes / Lab Insights

- Replicas are excellent for **read-heavy workloads** and reducing load on the primary.  
- Cross-region replicas are powerful for **DR setups**, but cost planning is essential.  
- Always monitor replication lag to avoid serving stale data in applications.  
- Promoting a replica should be a **controlled operation**, ideally part of a failover plan.

