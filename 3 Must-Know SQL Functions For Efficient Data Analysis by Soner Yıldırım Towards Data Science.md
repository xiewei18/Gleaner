# 3 Must-Know SQL Functions For Efficient Data Analysis | by Soner Yıldırım | Towards Data Science
Save From : [3 Must-Know SQL Functions For Efficient Data Analysis | by Soner Yıldırım | Towards Data Science](https://towardsdatascience.com/3-must-know-sql-functions-for-efficient-data-analysis-b7e4ee820faf) 

## Content
3 Must-Know SQL Functions For Efficient Data Analysis
=====================================================

Explained with practical examples

![](https://miro.medium.com/max/1400/1*mhW-IR7S3z9xkTWPHbY0cg.jpeg)

Photo by [Carl Heyerdahl](https://unsplash.com/@carlheyerdahl?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/efficient?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

SQL is a programming language used by relational database management systems. It provides numerous functions and methods that operate on the data stored in relational databases.

SQL is not just a query language. We can use it to filter, manipulate, and analyze data as well. In this article, we will go over 3 SQL functions that are quite useful for efficient data analysis.

The functions we will cover are:

*   Coalesce
*   Case when
*   Row_number

I have created two sample tables and filled them with mock data. Let’s first take a look at these tables.

![](https://miro.medium.com/max/1400/1*G59vFzIwMbm4teSnJcA1SA.png)

products table (image by author)

![](https://miro.medium.com/max/1400/1*C0_wb1rZyMsbAas0rvYKBw.png)

sales table (image by author)

The tables contain sales and product data from two different stores.

1\. Coalesce
------------

Consider a case where we need to left join the sales table to the products table. They are related by the product codes so we join the tables based on this column.

```
SELECT P.*, S.storecode, s.date, s.salesqty, s.salesrevenue                                                                      FROM products P                                                                                                                             LEFT JOIN sales S                                                                                                                           ON P.productcode = S.productcode;
```

![](https://miro.medium.com/max/1400/1*4AbekGnOabOltfcETEIwJg.png)

(image by author)

Not every product has sales on the given date. For these products, the columns from the sales table contain null values (empty in the screenshot above).

We can use the coalesce function to handle null values as a result of joining tables. In our case, we can fill the sales quantity and sales revenue columns with zeroes. The date column can be filled with the date in the other rows.

```
SELECT   
   P.*,   
   S.storecode,   
   coalesce(s.date, '2021-05-10') as date,    
   coalesce(s.salesqty,0) as salesqty,   
   coalesce(s.salesrevenue, 0)as salesrevenue                                                                                                                             FROM Products P                                                                                                                             LEFT JOIN Sales S                                                                                                                           ON P.productcode = S.productcode;
```

![](https://miro.medium.com/max/1400/1*UnM6FnbFe0u6fvnXdd2Paw.png)

(image by authot)

The empty cells are filled with the specified values in the coalesce function. I have left the store code as empty.

2\. Case when
-------------

The case when function allows for updating values based on given conditions. It is similar to the if-else statement in Python.

Let’s say we want to select all the columns from the sales table and create an additional column based on the sales revenue. If the revenue is higher than 5, this column takes the value “high”. Otherwise, it is filled with “regular”.

We can accomplish this operation with the case when function as follows:

```
SELECT   
   *,  
   CASE WHEN salesrevenue > 5 THEN 'high' ELSE 'regular' END AS  
   salesgroup  
FROM Sales;
```

![](https://miro.medium.com/max/1400/1*088eP6cW9tlGl67Y4PK98A.png)

(image by author)

The case when statement in the above query performs the following steps:

*   Create a column named “salesgroup”
*   When the value in the sales revenue column is more than 5, assign “high” to this column
*   Otherwise (i.e. else) assign “regular”

3\. Row_number
--------------

The row_number function allows for assigning a rank to the rows based on the values in a particular column. We can make it more flexible or useful by combining with a partition.

Recall the sales table:

![](https://miro.medium.com/max/1400/1*C0_wb1rZyMsbAas0rvYKBw.png)

sales table (image by author)

Let’s assume we need to assign a rank based on the sales revenue. We want to have separate ranks for different product groups. Thus, fruits and vegetables will be ranked within themselves.

The first step is to take the product group column from the products table. Then, we will use the row_number function.

```
SELECT  
   S.*,   
   P.productgroup,   
   ROW_NUMBER() OVER(PARTITION BY P.productgroup ORDER BY    
   salesrevenue DESC) AS salesrank  
FROM sales S   
LEFT JOIN products P   
ON S.productcode = P.productcode;
```

![](https://miro.medium.com/max/1400/1*q7aSlNQHHLdXM7xcEitW-g.png)

(image by author)

In each group, first rank is assigned to the row with the highest sales revenue. Then, it increases accordingly.

Conclusion
----------

SQL is a powerful tool in the data science ecosystem. It is definitely a must-have skill for data scientists. We should use SQL not only for retrieving data from a database but also for data analysis and manipulation.

SQL is able to perform almost all the operations that can be done with popular data analysis libraries such as Python pandas and R data table.

Thank you for reading. Please let me know if you have any feedback.
## Note