# Structured SQL Queries & Test Results

This document contains 5 representative SQL queries run against the local SQLite database (`coverage.db`) for the Enterprise Healthcare Coverage Assistant, along with their sample outputs.

---

## Query 1: Deductible for Gold PPO Plan
**Member Question:** *"What's the deductible on the Gold PPO plan?"*

### SQL Query
```sql
SELECT plan_name, annual_deductible 
FROM plans 
WHERE plan_name = 'Gold PPO';


plan_name,annual_deductible
Gold PPO,2000



SELECT COUNT(*) AS pending_claims_count 
FROM claims 
WHERE member_id = 'M1001' AND status = 'Pending';

pending_claims_count
1



SELECT plan_id, plan_name, monthly_premium 
FROM plans 
WHERE monthly_premium < 400;

plan_id,plan_name,monthly_premium
P102,Silver HMO,300
P103,Bronze HMO,150





SELECT c.claim_id, c.member_id, p.plan_name, c.procedure, c.claim_amount, c.status
FROM claims c
JOIN plans p ON c.plan_id = p.plan_id;

claim_id,member_id,plan_name,procedure,claim_amount,status
C1001,M1001,Gold PPO,X-ray,250,Pending
C1002,M1001,Gold PPO,Surgery,1200,Approved
C1003,M1002,Silver HMO,X-ray,150,Denied
C1004,M1002,Silver HMO,Surgery,900,Approved
C1005,M1003,Bronze HMO,X-ray,50,Pending





SELECT procedure, COUNT(*) AS claim_count, SUM(claim_amount) AS total_amount
FROM claims
GROUP BY procedure
ORDER BY claim_count DESC
LIMIT 5;

Here is a clear visual representation of what your VS Code window will look like once you create and paste into **`structured_queries.md`**:

```text
┌─────────────────────────────────────────────────────────────────────────┐
│  VS Code - COVERAGE-CHATBOT-API                                         │
├─────────────────┬───────────────────────────────────────────────────────┤
│ EXPLORER        │  structured_queries.md                                │
│                 │ ───────────────────────────────────────────────────── │
│ 📁 coverage-..  │  1  # Structured SQL Queries & Test Results          │
│   📁 .venv      │  2                                                    │
│   📁 data       │  3  ## Query 1: Deductible for Gold PPO Plan          │
│      claims.csv │  4  **Member Question:** *"What's the deductible..."*  │
│      plans.csv  │  5                                                    │
│      coverage.db│  6  ```sql                                            │
│   📄 main.py    │  7  SELECT plan_name, annual_deductible                │
│   📄 test_..py  │  8  FROM plans WHERE plan_name = 'Gold PPO';          │
│   📝 structured_│  9  ```                                             │
│      queries.md │ 10                                                    │
│                 │ 11  ### Output Result                                 │
│                 │ 12  | plan_name | annual_deductible |                 │
│                 │ 13  | Gold PPO  | 2000              |                 │
│                 │ 14                                                    │
│                 │ 15  ... (Query 2, 3, 4, and 5 follow below)          │
└─────────────────┴───────────────────────────────────────────────────────┘

```

---

### Key Things to Notice:

1. **Left Side (File Explorer):** `structured_queries.md` is listed as a file in your main project folder.
2. **Right Side (Editor):** All 5 questions, SQL queries, and table results live together inside this single file, stacked vertically from line 1 down to the end.

---

### Complete Text to Paste:

Copy everything inside this box in one go and paste it into the editor window:

```markdown
# Structured SQL Queries & Test Results

This document contains 5 representative SQL queries run against the local SQLite database (`coverage.db`) for the Enterprise Healthcare Coverage Assistant, along with their sample outputs.

---

## Query 1: Deductible for Gold PPO Plan
**Member Question:** *"What's the deductible on the Gold PPO plan?"*

### SQL Query
```sql
SELECT plan_name, annual_deductible 
FROM plans 
WHERE plan_name = 'Gold PPO';

```

### Output Result

| plan_name | annual_deductible |
| --- | --- |
| Gold PPO | 2000 |

---

## Query 2: Pending Claims Count for Member

**Member Question:** *"How many claims are pending for member M1001?"*

### SQL Query

```sql
SELECT COUNT(*) AS pending_claims_count 
FROM claims 
WHERE member_id = 'M1001' AND status = 'Pending';

```

### Output Result

| pending_claims_count |
| --- |
| 1 |

---

## Query 3: Affordable Plans Under Threshold

**Member Question:** *"Which plans have a monthly premium under $400?"*

### SQL Query

```sql
SELECT plan_id, plan_name, monthly_premium 
FROM plans 
WHERE monthly_premium < 400;

```

### Output Result

| plan_id | plan_name | monthly_premium |
| --- | --- | --- |
| P102 | Silver HMO | 300 |
| P103 | Bronze HMO | 150 |

---

## Query 4: Member Claims Joined with Plan Details

**Member Question:** *"Show me claims details along with the name of the health plan."*

### SQL Query

```sql
SELECT c.claim_id, c.member_id, p.plan_name, c.procedure, c.claim_amount, c.status
FROM claims c
JOIN plans p ON c.plan_id = p.plan_id;

```

### Output Result

| claim_id | member_id | plan_name | procedure | claim_amount | status |
| --- | --- | --- | --- | --- | --- |
| C1001 | M1001 | Gold PPO | X-ray | 250 | Pending |
| C1002 | M1001 | Gold PPO | Surgery | 1200 | Approved |
| C1003 | M1002 | Silver HMO | X-ray | 150 | Denied |
| C1004 | M1002 | Silver HMO | Surgery | 900 | Approved |
| C1005 | M1003 | Bronze HMO | X-ray | 50 | Pending |

---

## Query 5: Most Frequent Procedures (Top-N)

**Member Question:** *"What are the most commonly claimed medical procedures?"*

### SQL Query

```sql
SELECT procedure, COUNT(*) AS claim_count, SUM(claim_amount) AS total_amount
FROM claims
GROUP BY procedure
ORDER BY claim_count DESC
LIMIT 5;

```

### Output Result

| procedure | claim_count | total_amount |
| --- | --- | --- |
| X-ray | 3 | 450 |
| Surgery | 2 | 2100 |

```

```