# Multi-AZ RDS Testing

## 1. Multi-AZ Enablement Time

- Enabling Multi-AZ on an existing RDS instance typically took **~10–15 minutes**.
- Observation: The instance remained available during the process, but a brief performance impact was noticed while replication synced to the standby.

---

## 2. Actual Failover Duration

- During testing, the failover to the standby instance occurred in **~60–120 seconds** (1–2 minutes).
- PostgreSQL and MySQL both had similar failover times, although PostgreSQL felt slightly slower due to background processes.

> Note: Failover duration can vary based on instance class, database size, and workload.

---

## 3. Effect on Connection Strings

- **No change required** in the application connection string.
- AWS provides a **single endpoint** for the primary instance. During failover, the endpoint automatically points to the new primary.
- Application downtime is minimal if it retries connections properly.

---

## 4. Cost Impact of Multi-AZ

- Multi-AZ effectively **doubles the compute cost** because AWS provisions a standby instance in another Availability Zone.
- Storage costs remain the same, but IOPS costs may slightly increase due to synchronous replication.
- Overall, it’s a trade-off: higher reliability and automatic failover at increased cost.

---

## 5. Personal Notes / Lab Insights

- Multi-AZ is **excellent for production workloads** requiring high availability.
- Failover testing shows your application must handle transient connection interruptions.
- The endpoint abstraction makes failover seamless for applications.
- Cost should be evaluated vs the value of reduced downtime.
