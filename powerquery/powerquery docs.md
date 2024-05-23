# Power Query

## Extract Transform Load (ETL) 
![alt](/powerquery/images/image.png)

## Extract 
1. Load Datasets into Power Query Editor
2. (optional) Remove/Keep relevant rows and/or columns
3. (optional) Transform first row into header
4. (optional) Reorder Columns/rows 
5. (optional) Rename Query, or column names 
   
## Transform
Under View, check "Column Quality", "Column Distribution" and "Column Profile", this allows for clearer analysis of anomalous data.

![alt text](/powerquery/images/image-3.png)

> Take note that column profiling and distribution often times default to analysing first 1000 rows if dataset is large, to switch to whole dataset for accurate analysis:
> ![alt text](/powerquery/images/image-21.png)

**Column Distribution and Column Profile not showing for a column** 

- Select `keep errors` to investigate
- An error message will appear:
![alt text](/powerquery/images/image-1.png)
- Right click column to `Replace errors` 
- Remove `Kept Errors` in Applied Steps
  
## Error Handling
### Missing Data
- Null/Blank data can be replaced in `Replace Values` with whatever needed
- errors in entries that are numerical are likely to affect data visualisation more. 
  - Depending on data and context, blanks can be replaced with average values retreived from column statistics.
  - ![alt](/powerquery/images/image-4.png)
- For insignificant data, under the arrow of the column, `Remove Empty`
  
### Outliers, entry errors




### Duplicate Data
- Check unique values vs total values in Column Distribution
- If unequal, investigate duplicates under `Keep Rows` > `Keep Duplicates`
- If duplicates are unwanted, `Remove Duplicates`

## Column Transformations

`Transform` tab vs `Add Column` tab must be taken note of
  

### 1. Numeric
- Rounding Values
- Extract numeric information (e.g. even vs odd, sign)
- Calculate statistics (e.g. sum, count)
- Perform artihmetic operations

#### *Numeric Arithmetic*

e.g. Add column that calculates discharges minus admissions

1. select discharges column then admissions column
2. `Add Column` > `Standard`, `Subtract`
3. rename the column net_difference
   
----------

#### *Extracting Signs/even/odd*

Select Column> `Add Column`> `Information`> `Sign`

----------

### 2. Date/Time 
- Combine date/time fields
- extract date or time component
- round to start of the month, hour etc
- date arithmetic (age, duration)

#### *Transform Date*
`Date` > 

----------


#### *Date Arithmetic*

e.g. Subtract birth_date from survey_date

- select survey_date column then birth_date column
- under `Add Column`>`Date`>`Subtract Days`
- Transform into years by dividing by 365: `Standard`>`Divide`
- `Rounding`> Input 0 d.p
- Rename new column

----------

### 3. text
- splitting column contents
- case conversion
- concat 
- text length

#### *Extracting first or last characters of a column*
`Transform` > `Extract` 

----------

## Reshaping data & Aggregations

![alt text](/powerquery/images/image-8.png)

### 1. Transposing
Reshape rows to columns, columns to rows
![alt text](/powerquery/images/image-6.png)

### 2. Group By 
- Aggregare data into groups based on specific values (e.g. sum)
- Retains row and column orientation
![alt text](/powerquery/images/image-7.png)

example: performing group by transformation on hospital_site and Start of month on median question 3 score 
![alt text](/powerquery/images/image-14.png)

### 3. Pivoting Tables
![alt text](/powerquery/images/image-5.png)
- Reshape data and create a cross-tab by rotating rows into columns
- AND group/aggregate data based on specific columns (e.g. sum)

e.g. pivoting hosputal_site to show average of total_score for each hospital based on total_score as value
![alt text](/powerquery/images/image-10.png)
In advanced settings, change the aggregation to average:
![alt text](/powerquery/images/image-13.png)
![alt text](/powerquery/images/image-11.png)

Create a clustered column chart by going into excel, right clicking the sheet and creating a chart:
![alt text](/powerquery/images/image-12.png)

----------

### Difference between Reference and Duplicate Queries
Duplicate - Creates a copy and any changes made will not make any changes to the original/source query duplicated from

Reference - Is a continuation of the referenced source query. Any changes to the source query will affect the reference query

`View` > `Query Dependencies` to check out!


## Appending and Merging Queries
- Consolidates data from multiple sources
- Saves time by reducing manual manipulation (VLOOKUP etc.)
- Enriches larger datasets by including addition columns from related tables

**Append** - union - stack datasets of shared columns vertically
**Merge** - joins - combine datasets horizontally based on common column(s)

Join Types
![join types](/powerquery/images/image-15.png)

### Append
1. Open Queries that you want to append
2. Two type of append options:
![alt text](/powerquery/images/image-16.png)
  a. (default) Append Queries - will append onto hence edit file selected
  b. Append Queries *as New* - will append queries into a newly created query
  
  For 2 tables:
  ![alt text](/powerquery/images/image-17.png)
  
  For 3 or more tables:
  ![alt text](/powerquery/images/image-18.png)

### Merging
1. Open Queries you want to append
2. Select Query to merge on:
   a. (default) Merge Queries - will merge to selected query
   b. Merge queries *as New* - will merge queries into a newly created query

![alt text](/powerquery/images/image-19.png)

3. Fields of newly merged will only appear if selected and *expanded*
   ![alt text](/powerquery/images/image-20.png)

