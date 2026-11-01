# Problem Set 3 — The Number Nobody Can Reproduce

**ECON 3916 · Applied Data Analytics** · Role: Analyst, Business Intelligence

## Objective
Two queries on the same customer data gave two different "average West revenue" figures. I worked out which one is right, why they differ, what missing data does to regional comparisons, and whether the West account-management programme actually works.

## What's in the notebook
`Econ_3916_PS3.ipynb`, organised in four phases:

**Phase 1: Reproduce both numbers**
- Built a DuckDB warehouse: 3,000 customers (2,097 in the West) and 20,584 orders, with order counts drawn from a long-tailed negative binomial and revenue driven by order count.
- Wrote the two queries: averaging revenue over customers gives USD 814.43 on 2,097 rows; averaging after joining orders gives USD 1,250.67 on 14,191 rows (ratio 1.54).
- Wrote `join_check`, which compares row counts before and after a join; it fires on the fanned-out query and stays silent on a query that aggregates orders before joining.

**Phase 2: The rows that disappear**
- Set 450 customers' region (15%) to NULL.
- `WHERE region != 'West'` returned 760 rows; `WHERE region IS DISTINCT FROM 'West'` returned 1,210. The 450 missing rows are dropped by SQL's three-valued logic without any error.
- Used `AVG(revenue) OVER (PARTITION BY region)` to put each customer's revenue next to their region's average without collapsing rows (3,000 in, 3,000 out).

**Phase 3: The causal question**
- Simulated 5,000 customers where account size drives both West assignment and revenue, and the programme's true effect is USD 25.
- Naive West-vs-rest gap: USD 250.49. Controlling for account size: USD 25.43.
- Adding support tickets (caused by both the programme and revenue) as a control flipped the estimate to −USD 28.84.

**Phase 4: AI-assisted query reviewer**
- Used Claude to write `review_query(con, sql)`, then fixed a crash (some parse-tree fields are not strings) and lowered false alarms on equality filters.
- Ran it on my own Phase 1 and 2 queries. It caught the fan-out, flagged `!= 'West'`, and stayed quiet on the corrected queries, but missed the inflated average when it was computed in an outer query, and reported whole-table row counts instead of the filtered ones.

## Key findings
1. **USD 814 is the right number.** Revenue is measured per customer, so each customer must count once. The join counted customers once per order and inflated the average by about 54%.
2. **A row-count check catches this.** Neither query errors; only the row count shows that the unit of observation changed.
3. **Missing values change who is in the comparison.** A plain `!=` filter silently excluded 15% of customers.
4. **"West earns more" is not evidence that the programme works.** The West got larger accounts to begin with. Controlling for what existed before assignment recovers the true effect; controlling for something the programme changes makes the answer worse.
