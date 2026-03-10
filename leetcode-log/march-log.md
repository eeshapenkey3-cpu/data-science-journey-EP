# March LeetCode Log 2026

## *10-03-2026*

**Problem 1068: Product Sales Analysis I**  

**problem**:  
combine the Sales table and the Product table to show the product_name, year, and price for every sale.  

**solution**:  
```sql
SELECT 
    p.product_name, 
    s.year, 
    s.price
FROM Sales AS s
JOIN Product AS p 
  ON s.product_id = p.product_id;
