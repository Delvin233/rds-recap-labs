# RDS Backup and Point-in-Time Recovery (PITR) Testing

## 1. Backup Retention Period & Storage Costs

- **Longer retention periods increase storage costs** because AWS keeps more backup data over time.
- Example: Retaining automated backups for 7 days costs less than retaining them for 35 days.
- Storage cost grows linearly with retention and the size of the database.

---

## 2. Manual Snapshots vs Automated Backups

| Feature          | Manual Snapshot                           | Automated Backup                                        |
| ---------------- | ----------------------------------------- | ------------------------------------------------------- |
| **Creation**     | User-initiated                            | Automatically created by RDS                            |
| **Retention**    | Until explicitly deleted                  | Based on backup retention period                        |
| **PITR Support** | Can restore from the snapshot only        | Supports point-in-time recovery within retention window |
| **Use Case**     | Long-term archiving, before major changes | Daily backups, automatic recovery from failures         |

> Observation: Manual snapshots are ideal for before upgrades or schema changes, while automated backups handle daily disaster recovery.

---

## 3. Point-in-Time Recovery Duration

- In our lab testing, **PITR took ~5–10 minutes** to restore a small database (~1–2 GB).
- Duration increases with database size and complexity.
- AWS restores to the exact second within the retention window.

---

## 4. Limitations of Point-in-Time Recovery

- Can only restore to a **new database instance**; you cannot overwrite the existing instance.
- Restoration time depends on **database size and I/O activity**.
- PITR is limited to the **backup retention window** (e.g., 7–35 days).
- Cannot restore cross-region unless using cross-region automated backups or manual snapshots.

---

## 5. Personal Notes / Lab Insights

- Longer retention gives more flexibility but increases cost—balance based on business needs.
- Manual snapshots are great before risky operations or migrations.
- PITR is a **powerful safety net**, but for large production databases, expect longer recovery times.
- Always test PITR as part of a disaster recovery plan to understand real restore durations.

---

Try these labs here: **https://claude.ai/public/artifacts/0c0d2edd-8fb8-4be2-8db6-b86d722bed27**
