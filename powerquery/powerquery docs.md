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


## Custom Columns - using M (Data Mashup)
- Functional programming language in Power Query
- case-sensitive

### Add column from examples
1. Right click column that new column is to be based on, click "Add Column from Examples"
![alt text](/powerquery/images/image-22.png)
2. Key in some columns, the logic will automatically calculate and guess what you need
3. If logic is incorrect/inaccurate, edit it in the editor

### Add New Conditional Column
1. Under Add Column Tab > Conditional Column
2. Fill up conditional logic
![alt text](/powerquery/images/image-23.png)

### Custom Column
1. Under Add Column Tab > Custom Column
2. Key in M code needed
   ![alt text](/powerquery/images/image-24.png)
   ![alt text](/powerquery/images/image-25.png)

### Advanced indexing

#### Grouped index columns

*Case study:* The pharmacy team has sent a new data file with all the medication information collected for each patient who visited the emergency department. It includes each PatientID, the types of medications they are using, and the total medications for each.

Your task will be to enhance this dataset by adding a **grouped index medicationrankID** to count **unique medication types for each PatientID**, **sorted by top medication type by total medications**.

----------


1. Group the data by PatientID using the "All Rows" aggregation - `patientid_grouped`
   - Select PatientID then select *Group By* from the Transform Tab
   - Select *Advanced*
   - Assign "patientid_grouped" new column name with _ALL rows_ operation for aggregation
   - 
   - ![alt text](/powerquery/images/image-26.png)


2. Add a custom column `sortedgroup` to sort tables contained within the patientid_grouped column in descending order by total
   - Add a Custom Column from the Add Column section of the ribbon.
   - Recall that we want to sort the tables embedded within the patientid_grouped column.
   - The M `Table.Sort()` function syntax requires the input of the table to be sorted, followed by an optional sort argument to specify the column name and sort criteria.
   - 
   - ![alt text](/powerquery/images/image-27.png)

3. Add a custom column, `groupedindex` to add an index column (starting from 1) called medicationrankID to the tables contained within the sortedgroup column.
    - Select Custom Column from the Add Column section of the ribbon.
    - Recall that we want to add an index column to the tables embedded within the sortedgroup column.
    - The M function `Table.AddIndexColumn()` requires multiple arguments, including the column containing tables to be referenced, the name of the new index to be created, and the number to start the index from.
    - 
    - ![alt text](/powerquery/images/image-30.png)

`Patientid_grouped` column with embedded table:

![alt text](/powerquery/images/image-28.png)

`sortedgroup` column with embdded table with sorted total in descending order:

![alt text](/powerquery/images/image-29.png)

`groupedindex` column with embedded table with ranking/index of sorted total starting from 1

![alt text](/powerquery/images/image-31.png)

> Delete all columns except groupedindex and expand it 

FINAL TABLE:
![alt text](/powerquery/images/image-32.png)


## M Formula Language

- Case Sensitive
- *Let* Clause
   - Comma separated list of variable names or step identifiers
   - Each step builds upon previous step by referring to its name 
- *In* Clause
  - Step listed after the "in" clause is the visible query output

```javascript
let 
   Source = ""
in
   Source
```

### Value Types
Primitive
- single-part value (e.g. number, logical, text, or null)

Structured
- list (list = {1,2,3})
- Record (Record = [Column1=1, Column2=2])
- Table (#table({"ColumnA", "ColumnB"}, {{1,10}, {2,20}}))
- Function

### Custom Functions
```javascript
functionName = (Variable as Data Type, Variable as Data Type) => (Output Expression)
```

1. Open up query's advanced editor, add a new line after "Filtered rows" step and a single line comment to document 
2. In the Advanced Editor, define a new custom function called “convertesiscore” 
3. Add a new expression line named "Add scaled ESI score" in the Advanced Editor to add a new column to the table to invoke the new custom function, convertesiscore. Name the new column "scaledesiscore".
4. Update the "in" clause to return the expression step with the new "scaledsciscore" column, then close the Advanced Editor.

Note: you can use the Table.AddColumn() function to achieve this step.
![alt text](/powerquery/images/image-38.png)

### Built-in Functions
1. Create a blank query (New Query > Other Sources > Blank Query)
2. Into the editor: "`#shared`"
3. A list of functions will appear which you can turn into a table in the left corner
4. It is a clickable list where you can check the parameters and explanations of each function

![alt text](/powerquery/images/image-33.png)

## Query Parameters
placeholders to dynamically pass values to a query, making them more flexible and reusable (dynamic filters)
Case Study: Select a minimum score for ews score range
1. Open a blank query and create a custom list from 0 to 12
   ![alt text](/powerquery/images/image-34.png)

2. Create a new parameter called "Select EWS Minimum Score" and specify suggested values to the ews score range list query you created. Remove required option.

![alt text](/powerquery/images/image-35.png)

3. In dept_b_master query, which is the query we want to filter, set a filter on the ewsscore field to return values equal to or higher than the Parameter

![alt text](/powerquery/images/image-36.png)
![alt text](/powerquery/images/image-37.png)

4. Key in a parameter and the dept_b_master query will be filtered