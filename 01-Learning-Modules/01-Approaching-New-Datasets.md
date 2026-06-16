# Module 1: Approaching a New Dataset

## 🎯 Your First Day as a BA: The Framework

When you receive a new dataset, **most interns panic and jump into dashboards**. Senior analysts do something completely different—they ask questions, understand context, and build a mental map *before* touching any tool.

---

## 📋 The BA's First 24 Hours Framework

### **Phase 1: Business Context (Before Opening the Data)**

Before you look at a single row, answer these questions:

#### **1. The Business Context Questions**

```
🔍 CONTEXT DISCOVERY CHECKLIST

□ What business problem are we solving?
  Example: "We're losing money on low-value suppliers" 
  NOT: "Just analyze the data"

□ Who is asking for this analysis?
  Example: "CFO wants to reduce procurement costs by 20%"
  Context: This means you need financial impact, not just insights

□ What decision will this data inform?
  Example: "Should we consolidate suppliers or renegotiate rates?"
  Context: This shapes which KPIs matter most

□ What's the business outcome?
  Example: "Reduce annual spend by $5M in 6 months"
  Context: This tells you if you're analyzing quarterly or annual trends

□ What metrics does the business already track?
  Example: "They monitor supplier cost variance and delivery time"
  Context: You should include these in your analysis

□ What's the time sensitivity?
  Example: "Decision needed in 2 weeks"
  Context: This affects your analysis depth and priorities

□ Who will use the insights?
  Example: "Finance director, procurement manager, category heads"
  Context: Different stakeholders need different depths of analysis
```

#### **2. The Data Context Questions**

```
🔍 DATA DISCOVERY CHECKLIST

□ What does this data represent?
  Example: "All purchase transactions for FY 2022-2025"
  
□ How was it collected?
  Example: "From SAP ERP system, monthly extracts"
  Context: Tells you about potential data quality issues

□ What's the data source and frequency?
  Example: "Real-time procurement system, updated daily"
  Context: If it's manual, data quality is likely lower

□ How old is this data?
  Example: "Last updated yesterday"
  Context: Is it current enough for decision-making?

□ What's the granularity?
  Example: "Individual transactions, not aggregated"
  Context: High granularity = more flexibility for analysis

□ What period does it cover?
  Example: "Jan 2022 - Jun 2025 (3.5 years)"
  Context: Enough for trend analysis? Seasonal patterns?

□ Are there known data quality issues?
  Example: "Some entries have missing supplier names from 2022"
  Context: Plan for data cleaning
```

---

### **Phase 2: The Data Dictionary Deep Dive**

**BEGINNER MISTAKE:** Opening Excel and scrolling randomly.
**EXPERT APPROACH:** Understand every column *before* analysis.

#### **Your Procurement Dataset Headers Explained**

```
📊 COLUMN-BY-COLUMN UNDERSTANDING

1. LL (Line Item?)
   What it is: Unique identifier for each line in a purchase order
   Why it matters: Helps you identify duplicate entries
   Analysis use: Filter, deduplicate, join operations
   
2. Tag
   What it is: Custom classification or marking system
   Why it matters: Could indicate priority, exception, or special handling
   Analysis use: Filter for specific transaction types
   
3. Date
   What it is: When the transaction occurred
   Why it matters: CRITICAL for trend analysis and time-series
   Analysis use: Group by month/quarter/year, identify seasonality
   Question to ask: Are all dates valid? Any future dates?
   
4. Particulars
   What it is: Description of what was purchased (item details)
   Why it matters: Helps understand what categories are spending on
   Analysis use: Text mining, categorization, grouping
   
5. Master Description
   What it is: Standard/standardized description of the item
   Why it matters: Cleaner version of "Particulars" for analysis
   Analysis use: Use this for grouping, not "Particulars"
   
6. Master
   What it is: Likely a master ID for the product/service
   Why it matters: Links to a product master table
   Analysis use: Aggregation, consistency checks
   
7. ICD (Inter-Company Deal? Internal Code?)
   What it is: Internal classification code
   Why it matters: May indicate internal transfers vs. external purchases
   Analysis use: Filter for true external spend
   
8. Supplier
   What it is: Name of the vendor/supplier
   Why it matters: KEY for supplier analysis and consolidation
   Analysis use: Spend by supplier, supplier concentration, performance
   Critical Question: How many unique suppliers? Any duplicates (Acme vs. ACME)?
   
9. Supplier Invoice No.
   What it is: Invoice number from supplier
   Why it matters: Helps match to payment records, audit trail
   Analysis use: Deduplicate, match with finance system
   
10. Quantity
    What it is: Number of units purchased
    Why it matters: Volume analysis, cost per unit
    Analysis use: Calculate unit rate, volume trends
    Question: Are negative quantities refunds/returns?
    
11. Value
    What it is: Total transaction value (Amount)
    Why it matters: PRIMARY metric for spend analysis
    Analysis use: Sum by category, supplier, department
    Question: Is this gross or net? Before or after discounts?
    
12. Value In Lacs
    What it is: Same as Value but in Lacs (100,000 units)
    Why it matters: Makes large numbers readable
    Analysis use: Reporting to senior management
    
13. RATE
    What it is: Unit price (Value / Quantity)
    Why it matters: Identifies pricing outliers and trends
    Analysis use: Price benchmarking, supplier comparison
    
14. UOM (Unit of Measure)
    What it is: Units being purchased (Kg, Liters, Pieces, etc.)
    Why it matters: Different items measured differently
    Analysis use: Can't compare Kg to Pieces directly
    
15. Catg. Type (Category Type)
    What it is: Broad classification of purchase type
    Why it matters: CRITICAL for spend breakdown
    Analysis use: Spend by category, category trends
    
16. New category typ (New Category Type)
    What it is: Updated/revised category classification
    Why it matters: System was likely recategorized
    Analysis use: Use this, not "Catg. Type"
    Question: Are they the same? Any mapping?
    
17. Category Head
    What it is: Head/leader of the category
    Why it matters: Identifies who's responsible
    Analysis use: Departmental accountability analysis
    
18. Deptt. (Department)
    What it is: Which department made this purchase
    Why it matters: Spend by department, cost control
    Analysis use: Department budget analysis, spending patterns
    
19. FY (Fiscal Year)
    What it is: Fiscal year when purchase was made
    Why it matters: Year-over-year comparison
    Analysis use: Annual trends, budget cycles
    
20. First Purchase Year
    What it is: When this supplier was first used
    Why it matters: Identifies new vs. established suppliers
    Analysis use: Supplier tenure, new vendor ramp-up
```

---

### **Phase 3: The 10 Questions Every BA Asks About a Dataset**

Before analysis, ask yourself:

```
✅ MANDATORY 10 QUESTIONS CHECKLIST

1. COMPLETENESS
   □ Are there missing values? Where? Why?
   → Impact: Can I analyze by department if 10% have no department?
   
2. CONSISTENCY
   □ Are dates in same format? Supplier names standardized?
   → Impact: "Acme Corp" vs "ACME CORPORATION" = different suppliers?
   
3. ACCURACY
   □ Are values reasonable? Any obvious errors?
   → Impact: One $10M transaction from a normally $10K supplier = error?
   
4. UNIQUENESS
   □ Are there duplicates? How do I identify them?
   → Impact: If same supplier invoice appears twice, analysis is inflated
   
5. OUTLIERS
   □ What's the range of values? Any extreme outliers?
   → Impact: One $100M transaction might skew all analysis
   
6. TIME COVERAGE
   □ Is the data continuous or are there gaps?
   → Impact: Missing January data affects monthly trend analysis
   
7. GRANULARITY
   □ Is this transaction-level or already aggregated?
   → Impact: Different analysis approaches for each
   
8. RELATIONSHIPS
   □ How do columns relate? Are there dependencies?
   → Impact: Value should = Quantity × Rate (verify this!)
   
9. DEFINITIONS
   □ What does each column truly represent?
   → Impact: Is "Value" gross or net? Before discount or after?
   
10. CONTEXT
    □ What changed in the business during this period?
    → Impact: Spike in June might be seasonal, not a trend
```

---

## 🧠 What Different Analysts See

### **BEGINNER ANALYST SEES:**
- "I have 20 columns and 10,000 rows"
- "Let me make charts for everything"
- "The data looks clean, let's analyze it"
- Starts building dashboard immediately

### **EXPERIENCED ANALYST SEES:**
- "Supplier name isn't standardized (duplicates likely)"
- "Why are there two category columns? Which should I use?"
- "Value In Lacs means large transactions. Are these aggregated?"
- "Date is the key to trend analysis—must check for gaps"
- "Quantity × Rate should = Value. If not, data quality issue"

### **SENIOR ANALYST / MANAGER SEES:**
- "This data can show us supplier concentration risk"
- "First Purchase Year tells us which suppliers are replacing old ones"
- "Department spending trends could justify headcount or budget"
- "Category Head column means procurement owns this—they'll need buy-in"
- "This data could reduce spend by $5M if we consolidate suppliers"

---

## 📊 Procurement Data: 10 Initial Questions to Ask

**YOUR SPECIFIC DATASET CONTEXT:**

```
🎯 PROCUREMENT-SPECIFIC QUESTIONS

Business Questions:
1. How much are we spending overall? By category? By department?
2. Are we consolidating spend or fragmented across many suppliers?
3. Which suppliers are strategic (high spend) vs. transactional?
4. Are we paying competitive rates? How do rates vary by supplier?
5. Which categories are growing? Shrinking?

Data Quality Questions:
6. How many unique suppliers do we actually have? (Acme vs ACME issue?)
7. How clean is the data? Missing values? Outliers?
8. Can I trust the category classifications?
9. How old is this data? (Decision-making depends on freshness)
10. Are there transactions I should exclude? (Returns, internal transfers?)
```

---

## 🎬 Real Business Scenario

### **Your First Day: Email from CFO**

```
Subject: Analyze our procurement data - cost reduction opportunity

Hi Priyankshi,

We need to understand where our money is going in procurement. 
I suspect we're:
1. Paying too much to too many suppliers
2. Not leveraging category spend efficiently
3. Missing bulk discount opportunities

Can you analyze our purchase data and give me insights in 1 week?
I need to present to the board on trends, cost drivers, and 
opportunities for $5M in cost reduction.

Thanks,
CFO
```

### **What a Beginner Does:**
1. Opens data in Excel
2. Makes random charts
3. Writes: "Total spend is $50M. Attached charts."
4. CFO: "What should I DO with this?"

### **What an Experienced Analyst Does:**
1. Asks CFO: "In the $5M cost reduction, are we talking supplier consolidation, rate negotiation, or process efficiency?"
2. Understands the dataset context completely
3. Identifies that there are 500 suppliers but top 20 = 80% of spend
4. Creates analysis with actionable insights: "Consolidate 300 low-value suppliers onto top 20 platforms = $3M savings"
5. Provides specific recommendations

---

## ✅ Your Action Plan for Day 1

```
PHASE 1: BUSINESS UNDERSTANDING (30 minutes)
□ Write down: What business problem are we solving?
□ Identify: Who's the key stakeholder?
□ Understand: What decision will this influence?
□ Note: What outcome matters? (Cost reduction? Speed? Quality?)

PHASE 2: DATA DICTIONARY (45 minutes)
□ Create a document listing all 20 columns
□ For each column, write: What it means + Why it matters
□ Identify: Which columns are most important for your business question?
□ Flag: Any columns that seem suspicious or unclear

PHASE 3: DATA QUALITY CHECK (30 minutes)
□ Load data into Python/Tableau
□ Check: How many rows? Missing values? Duplicates?
□ Check: Date range? Any obvious errors?
□ Note: Data quality issues to handle in analysis

PHASE 4: INITIAL EXPLORATION (45 minutes)
□ What's the total spend?
□ How many unique suppliers?
□ What's the biggest category?
□ Which department spends most?
□ Note: Initial observations (don't analyze yet, just observe)

TOTAL TIME: 2.5 hours

OUTPUT: 
- Business Context Document
- Data Dictionary
- Initial Data Quality Report
- 10 Key Observations
```

---

## 🎓 What You'll Know After This Module

✅ How to ask the right questions *before* analyzing
✅ The complete meaning of every column in procurement data
✅ How to identify data quality issues
✅ How to think like an experienced analyst
✅ The framework for the first day with any new dataset

---

## 📚 Next Steps

→ **Move to Module 2:** `02-Exploratory-Data-Analysis.md`

Once you understand the dataset, you'll learn how to explore it professionally.

---

**Remember:** 
> **"The quality of your insights depends on the quality of your questions, not the quality of your charts."**
> 
> Spend more time understanding. Less time dashboard-building.

