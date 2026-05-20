#Nigeria 2023 Presidential Election — Data Intelligence Project

> **"Data doesn't pick a party. It just tells the truth."**

A complete SQL Server analytics project that transforms INEC's 2023 Nigerian Presidential Election results into structured, queryable intelligence — answering 10 real business-style questions about voter behaviour, party dominance, regional patterns, and competitive races.

---

## 📌 Project Context

| Detail | Info |
|--------|------|
| **Election** | 2023 Nigerian Presidential Election |
| **Data Source** | INEC Official Results (36 States + FCT) |
| **Tool** | SQL Server Management Studio (T-SQL) |
| **Author** | Oladipupo Abidemi Francis |
| **Role** | Data Analyst |

The 2023 Nigerian Presidential Election was one of the most competitive in the country's history — with four major parties (APC, PDP, LP, NNPP) contesting strongly across different geopolitical zones. This project uses relational database design and T-SQL queries to extract insights that go far beyond the headline result.

---

## 🗄️ Database Architecture

```
NigeriaElection2023
│
├── States          — 37 rows (36 states + FCT)
│   ├── StateID (PK)
│   ├── StateName
│   ├── GeoPoliticalZone
│   ├── RegisteredVoters
│   └── AccreditedVoters
│
├── Parties         — 6 rows (top competing parties)
│   ├── PartyID (PK)
│   ├── PartyCode
│   ├── PartyName
│   └── Candidate
│
└── ElectionResults — 148 rows (votes per party per state)
    ├── ResultID (PK)
    ├── StateID (FK → States)
    ├── PartyID (FK → Parties)
    └── VotesWon
```

**Design decisions:**
- Normalised into 3 tables to avoid data redundancy
- Foreign key constraints enforce referential integrity
- `UNIQUE` constraint on `(StateID, PartyID)` prevents duplicate entries
- `DEFAULT 0` on VotesWon handles states with no result for a party

---

## 🔍 The 10 Analytical Questions

| # | Question | SQL Technique Used |
|---|----------|--------------------|
| 1 | Who won the popular vote nationally? | `GROUP BY`, `SUM`, percentage calculation |
| 2 | Which geopolitical zone had highest voter turnout? | `GROUP BY`, division, `ORDER BY` |
| 3 | Which party won each state? | `RANK()` Window Function, `CTE`, `PARTITION BY` |
| 4 | How many states did each party win? | Nested `CTE`, `COUNT`, `RANK()` |
| 5 | Which party dominated each geopolitical zone? | `RANK()` with zone partition |
| 6 | Top 10 closest races (margin of victory)? | Self-JOIN on CTE, subtraction |
| 7 | Top 5 states by total votes cast? | `SUM`, `TOP 5`, percentage |
| 8 | LP vs APC head-to-head in the Southwest? | `CASE WHEN` pivot, conditional SUM |
| 9 | Which states had the most registered voters who didn't show up? | Derived column arithmetic, absentee rate |
| 10 | National election scorecard | `UNION ALL`, mixed aggregations |

---

## 💡 Key Insights Uncovered

### 🗳️ National Vote Share
| Party | Votes | Share |
|-------|-------|-------|
| **APC** | **8,794,726** | **36.6%** |
| LP | 6,101,533 | 25.4% |
| PDP | 6,984,520 | 29.1% |
| NNPP | 1,496,687 | 6.2% |

### 🗺️ Geopolitical Zone Breakdown
- **North West** delivered APC's strongest margin — over 2.4M votes
- **South East** was LP's fortress — winning all 5 states convincingly
- **South West** was the most contested zone — LP and APC within 100K votes in Lagos
- **North East** showed the lowest voter turnout nationally

### 🏆 States Won Per Party
| Party | States Won |
|-------|-----------|
| APC | 12 |
| LP | 12 |
| PDP | 12 |
| NNPP | 1 (Kano) |

### ⚡ Closest Race
- **Zamfara** — PDP beat APC by just 9,835 votes
- **Sokoto** — PDP edge of 46,715
- **Lagos** — LP vs APC difference of only ~9,848 votes

### 📉 Voter Apathy
- Over **60% of registered voters** nationwide did not accredit — a systemic participation crisis
- Kano had the highest total registered voters (5.4M) but NNPP candidate Kwankwaso pulled a massive upset there

---

## 🛠️ SQL Concepts Demonstrated

```sql
✅ Database & Table Creation (DDL)
✅ Data Insertion (DML)
✅ Foreign Keys & Constraints
✅ Window Functions: RANK() OVER (PARTITION BY ...)
✅ Common Table Expressions (CTEs)
✅ Self-JOIN for margin analysis
✅ CASE WHEN for conditional pivoting
✅ UNION ALL for scorecard aggregation
✅ FORMAT() for presentation-ready output
✅ Subqueries & nested aggregations
✅ Business-focused commentary and naming
```

---

## 🚀 How to Run This Project

1. Open **SQL Server Management Studio (SSMS)**
2. Run the full script: `nigeria_election_2023.sql`
3. The script will:
   - Create the `NigeriaElection2023` database
   - Build all 3 tables with proper constraints
   - Insert all party, state and results data
   - Execute all 10 analytical queries with formatted output

> **Note:** Requires SQL Server 2016+ for `FORMAT()` function support

---

## 📊 Sample Query Output — Q3: State Winners

```
StateName     | GeoPoliticalZone | WinningParty | WinningCandidate      | VotesWon
--------------+------------------+--------------+-----------------------+---------
Kano          | North West       | NNPP         | Rabiu Musa Kwankwaso  | 994,885
Lagos         | South West       | LP           | Peter Obi             | 582,454
Anambra       | South East       | LP           | Peter Obi             | 346,185
Rivers        | South South      | APC          | Bola Ahmed Tinubu     | 231,591
...
```

---

## 👨‍💻 About the Author

**Oladipupo Abidemi Francis** — Data Analyst & Educator based in Lagos, Nigeria.

Skilled in SQL Server, Excel, Power BI, Python, and AI automation. Passionate about using data to tell meaningful stories about real-world events — from business sales to national elections.

- 🔗 [LinkedIn](https://linkedin.com/in/fran7safe)
- 💻 [GitHub](https://github.com/fran6safe)
- 📧 abidemifrancis@gmail.com

---

> *"DATA IN THE HANDS OF A WORNG PERSON IS THE BEGINING OF CORRUPTION."*
