# Submission Template: Module 4 Lab 1: pandas on a Real Dataset

Name: Khandker Ehmar Reza    Date: 11/09/2026

Fill this in as you work. Sections marked PREDICT must be written before you run the step.

---

### Step 1: Load the file and profile it

> So after running the template code, I've noticed 3 issues with the columns. The data type for the dates ended up being read as strings, there's 21 missing prices for the unit_price column, and there are negative shipping costs in the shipping_cost column. A negative shipping cost would mean the customer is being PAID for shipping.

### Step 2: Sort the problems into two kinds

> Wrote a check for negative shipping prices

### Step 3: Fix two problems and say what each fix costs

#### Problem 1: unit_prices

> WHAT: 21 blank unit prices
DID: Dropped those 21 rows
COSTS: Lost actual customer details for that order, like payment, date, category, etc.

#### Problem 2: shipping_costs
> WHAT: 13 Negative shipping costs
DID: Got rid of the rows with negative shipping costs
COSTS: This also lost 13 real order details

## 4. Reflection

Your own words. No AI assistance. Graders check these against the outputs in your notebook.

### 1. Quote your own two numbers from Step 3, the average quantity before and after deleting the rows where unit_price is missing. Say what the size of that difference tells you about whether the missing values are random, and what it means for your decision.

> The changes in the averages kinda only showed me how little they missing unit_prices mattered even though I got rid of 21. It was a very minor change in the mean (about .01). The means before and after were ${5.088}$ and ${5.079331941544885}$ respectively

### 2. Someone will use your cleaned file without reading your notebook. Write the three sentences you would put at the top of it so they do not misuse it.

>  "Title: Ecommerce Orders. This notebook is for cleaning up the list of orders. Only alter df_clean, and run every cell in order. The rows have already been dropped from 500 to 466 due to missing unit_prices and impossible shipping_costs.". 

## 5. AI use disclosure

Required by the course AI Use Policy. Write none if you used no AI.

- **Tool used:** Gemini
- **What I asked for:** 

> How to profile m4_ecommerce_orders.csv; why Excel shows "#######" for dates while preserving underlying values; how Step 2 categorizes data defects into missing values versus impossible values; whether a custom check was needed for the date column; what the "before" and "after" mean quantity checks verify in Step 3; how to structure the three-line WHAT/DID/COSTS blocks for missing unit prices and negative shipping costs; why the date string format appeared to shift from M/D/YYYY to YYYY-MM-DD; code review and validation for the combined pandas pipeline; what Step 4 requires for grouped aggregations (highest average quantity by category and highest average shipping cost by region); and whether lecture transcripts instruct leaving notes/documentation for collaborators using cleaned files.

- **What I used from it:** 

> Some generated code, as I was confused as to what we needed to do and what it meant. Asked it to elaborate the syntax on "df.dropna" and how to clear rows with values. Also used explanations for the gaps formed by the assignment.

- **How I verified it:** 

> By using it and altering the usage myself to see how it works. Also had to go back and forth between a wrong markdown template and the assignment page, confused as to what we needed to do. So, I changed the entire to fit the assignment.


## 6. Checklist

- [ ] Predictions written before running
- [ ] Actual results recorded, including the ones I got wrong
- [ ] Exact error text captured for every break it item
- [ ] Notebook runs top to bottom with outputs visible
- [ ] PDF exported after the full run
- [ ] Reflection written by me
- [ ] Files uploaded individually, no archive
