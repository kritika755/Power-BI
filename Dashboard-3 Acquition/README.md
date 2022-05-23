
Acquition

A company is acquiring another company and before that 
they want to perform audit of the company they are about to acquire


## Deliverables

1.What is the total Sales .

2.What about the total Quantity sold by that company(customer engagement).

3.Profit for the said period and margin on the same.

4.Details performance of last year for any selected year.

5.comparision of performance vs last year.

6.Sales 2 years ago for any Selected year.

7.Moving average in terms of Profit and sales.

8.Date table to make the analysis stable.

9.Quater wise analysis using Slicer.

10.Total Sales , Profit and %Profit can be shown as combo(Card and Line chart).

11.Show the sales comparision between cumulative performane Vs Cumulativ performance last year using area chart

12.Top performer in terms of product and customer Top 7.

13.Performance in terms of region sales -Bar Graph
## Dataset

We have five Tables:
1. Customer Data:

	1.1. Customer index

	1.2. Customer sales

2. Metric Selection: 

	2.1.Metric-There are three metrics- Revenue, Costs, Profits
	
    2.2.Metric Index
3. Product Data:
 	
    3.1. Index
	
    3.2. Product Name
4. Regions:
	
    4.1. Index
	
    4.2. Territory
	
    4.3. City 
	
    4.4. Country
	
    4.5. Full Address
5. Sales:
	
    5.1 Order Number
	
    5.2 Order Date
	
    5.3 Ship Date
	
    5.4 Customer Name Index
	
    5.5 Channel-Distributor, wholesale,Export
	
    5.6 Currency
	
    5.7 Warehouse Code
	
    5.8 Deliver Region Index
	
    5.9 Product desciption Index
	
    5.10 Order Quantity
	
    5.11 Unit Price
	
    5.12 Total Unit cost
	
    5.13 Total Revenue



## Important Measures

1. Total cost: What is the total costing of production of the products.

	Total Cost = SUMX(Sales,Sales[Order Quantity]*Sales[Total Unit Cost])

2. Total sales:What is the total sales. 
	
	Total Sales = SUMX(Sales,Sales[Order Quantity]* Sales[Unit Price])

3. Total Quantity: What is the total Quantity sold.
	
	Total Quantity = SUM(Sales[Order Quantity])

4. Profit : 
	
	Total Profit = [Total Sales]-[Total Cost]  

5. Profit Margin:
    	
	Profit margin = DIVIDE([Total Profit],[Total Sales],0)

## Specific Scenario Measures.


1. FIND OUT TOP 7 PRODUCTS
Top 7 Customers- CALCULATE([Total Sales],FILTER(VALUES('Customer Data'[Customer Names]),IF(RANKX(ALL('Customer Data'[Customer Names]),[Total Sales],,DESC)<=7,[Total Sales],BLANK())))

2. FIND OUT TOP 7 CUSTOMERS
Top 7 Products = CALCULATE([Total Sales],FILTER(VALUES('Product Data'[Product Name] ),IF(RANKX(ALL('Product Data'[Product Name]),[Total Sales],,DESC)<=7,[Total Sales],BLANK())))

## Time Intelligence Measures

1. Performance LY:

 	    Performance LY = CALCULATE([Total Profit],PREVIOUSYEAR('DimTable'[Date]))

2. Performance-LY:

 	    Performance-LY = CALCULATE([Total Profit],DATEADD('DimTable'[Date],-1,YEAR))

3.Profit Last Year:

	    Profit Last Year = CALCULATE([Total Profit],SAMEPERIODLASTYEAR(DimTable[Date]))

4. Profit Moving Average:

	    Profit Moving Average = 
		    AVERAGEX(
    			FILTER(ALLSELECTED(DimTable),
    			DimTable[Date] <=MAX(DimTable[Date])),
    			[Total Profit])
	
5.Sales Last Year
	
	sales last year = CALCULATE([Total Sales],SAMEPERIODLASTYEAR(DimTable[Date]))

6.Sales 2Yrs Ago:

	sales 2yrs Ago = CALCULATE([Total Sales],DATEADD(DimTable[Date],-2,YEAR))
    
6. Sales Moving Average

Sales Moving Average = 
		AVERAGEX(
    			FILTER(ALLSELECTED(DimTable),
    			DimTable[Date] <=MAX(DimTable[Date])),
    			[Total Sales])

## DAX Functions used

1. SUMX-Returns the sum of an expression evaluated for each row in a table.
	
	SUMX(<table>, <expression>)

2.CALCULATE-calculate an expression with a modified filter context.
	
	CALCULATE(<expression>[, <filter1> [, <filter2> [, …]]])

3.DATEADD - Returns a table that contains a column of dates, 
	shifted either forward or backward in time by the specified number of intervals from the dates in the current context.
		
	DATEADD(<dates>,<number_of_intervals>,<interval>)  
      
4.SAMEPERIODLASTYEAR:Returns a table that contains a column of dates shifted one year back in time from the dates in the specified dates column, in the current context.     

	SAMEPERIODLASTYEAR(<dates>)  

5. AVERAGEX:Calculates the average (arithmetic mean) of a set of expressions evaluated over a table.

	AVERAGEX(<table>,<expression>)  
## Other Things I have learnt in this project

1.Fact(can have duplicate value for example sales table) vs dimensions( unique columns  and have a foreign relation with fact table)	-
2.Measures( are calculated values that can be used later as well for further analysis) are always applied on Fact(sales)

3.How to create Important measure section to contain all the measures used in your analysis:
home>Enter_data>on the dialogue box name the table as important measures> click on Load( there will be blank table created )
create a simple measure
Click on that measure-->measure tools column will be activated above>Change the  home table to 	"Important measures"

4.difference betweet unit cost and unit price.
Unit cost:Cost of production of product + packaging. What it costs to business
Unit price: Price of a single item What it costs to a customer

	Cost-Price= Profit

	
Screenshot:
	
![] (https://github.com/kritika755/Power-BI/blob/main/Dashboard-3%20Acquition/Capture.PNG)
	
