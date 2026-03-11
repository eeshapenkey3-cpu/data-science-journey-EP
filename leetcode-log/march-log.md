# March LeetCode Log 2026

## *10-03-2026*

**Problem 1068: Product Sales Analysis I**  

**problem**:  
combine the Sales table and the Product table to show the product_name, year, and price for every sale.  

**solution**:  
```
sql
SELECT 
    p.product_name, 
    s.year, 
    s.price
FROM Sales AS s
JOIN Product AS p 
  ON s.product_id = p.product_id;
```  

## *11-03-2026*

**Problem 13: Roman to Integer**

**problem**:
Given a roman numeral, convert it to an integer. Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M. The logic must account for instances where a smaller value appears before a larger value (e.g., IV = 4), requiring subtraction rather than addition.

**solution**:
```
java
class Solution {
    public int romanToInt(String s) {
        int total = 0;
        int i = 0;
        
        // Using a while loop to align with current class modules
        while (i < s.length()) {
            int current = getValue(s.charAt(i));
            
            // Subtraction Rule: Look ahead to see if the next value is greater
            if (i + 1 < s.length() && current < getValue(s.charAt(i + 1))) {
                total -= current;
            } else {
                total += current;
            }
            i++;
        }
        return total;
    }

    private int getValue(char c) {
        switch (c) {
            case 'I': return 1;
            case 'V': return 5;
            case 'X': return 10;
            case 'L': return 50;
            case 'C': return 100;
            case 'D': return 500;
            case 'M': return 1000;
            default: return 0;
        }
    }
}
```
