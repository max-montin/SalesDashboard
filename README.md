# Pizzeria Sales Dashboard
In this project, I analyzed a fictional dataset containing a year's worth of sales data that was gathered from a Pizzeria.
The original data included four separate tables containing columns such as order IDs, pizza IDs, ingredients, dates and times, prices, and quantities. All other columns have been added by me.

The dashboard can be seen below, and under it you can find a step-by-step description of how this project was completed.

<img src="https://github.com/max-montin/SalesDashboard/blob/main/Files/PizzaSales.png">

[Link to Power BI file](https://github.com/max-montin/SalesDashboard/blob/main/Files/PizzaSales.pbix)

After loading and modeling the data, the tables needed transforming in Power Query.
- First, I changed some data types to better match the fields.
- In the original file, all ingredients of an item were listed in one column. Some items contained more ingredients than others, so as a solution I separated the ingredient lists into columns and made redundant columns null.
- To find the totals of each order, I grouped the orders by order IDs and calculated the sums of each order by fetching the prices from the pizza detail table.
- The original files contained just plain dates, so I added a column to show which day of the week each date was. Because Power BI sorts day names alphabetically and not in their usual order and Power Query starts the week from Sunday, I needed to create a function that moves the order number of each day by one:

  ```
  if Date.DayOfWeek([date]) < 7 then Date.DayOfWeek([date])+1 else 0
  ```
- After creating the new column to assign correct order numbers to each day of the week, I added a conditional sort to sort the day names by the newly created column. This made it possible to visualize weekly data while keeping the days in correct order and representing them in their written formats.
- In order to find out how frequently each ingredient was used, I needed to merge the tables. First, I merged the pizza IDs to the pizza types, and then I merged that table to the ingredients table. After merging the tables, I unpivoted all of the ingredient columns and grouped the data by ingredient. This allowed me to calculate the sum of ordered quantities by ingredient and find the popularity of each ingredient.
- Lastly, to visualize daily traffic, I created a data group that assigns the order times into 15-minute bins and gives a better representation of the busiest and quietest timeframes.

The data used in this project was downloaded from [Maven Analytics](https://www.mavenanalytics.io/data-playground).

[CSV files](https://github.com/max-montin/SalesDashboard/tree/main/Files)
