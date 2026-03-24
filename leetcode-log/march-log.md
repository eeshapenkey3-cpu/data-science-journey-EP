# March LeetCode Log 2026  

## *02-03-2026*  

**Problem 1: Two Sum**:  

**problem:** Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.  

**solution:**
``` java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++){
            for (int j = i + 1; j < nums.length; j++ ){
                if(nums[i] + nums[j] == target){
                    return new int[] {i, j};
                }
            }
        }
        return new int[]{};
    }
}
```
## *04-03-2026*  

**Problem 175: Combine Two Tables**  

**problem:**
Write a solution to report the first name, last name, city, and state of each person in the Person table. If the address of a personId is not present in the Address table, report null instead.  

**solution:** 
```
sql
SELECT firstName, lastName, city, state FROM Person
LEFT JOIN Address 
ON Person.personID = Address.personID

```
## *06-03-2026*  

**Problem 182: Duplicate Emails**  

**problem:** Write a solution to report all the duplicate emails. Note that it's guaranteed that the email field is not NULL.  

**solution**:
```
sql
SELECT email AS Email FROM Person 
GROUP BY email
HAVING COUNT(email) > 1
```
## *08-03-2026*  

**Problem 627: Swap Sex of Employees**  

**problem:** Write a solution to swap all 'f' and 'm' values (i.e., change all 'f' values to 'm' and vice versa) with a single update statement and no intermediate temporary tables.  

**solution**: 
```
UPDATE Salary set sex = if( sex = 'f', 'm', 'f'); 
```
## *09-03-2026*  

**Problem 1667: Fix Names in a Table**

**problem**:
Write a solution to fix the names so that only the first character is uppercase and the rest are lowercase. Return the result table ordered by `user_id`.

**solution**:
```sql
SELECT user_id,
CONCAT(UPPER(SUBSTRING(name, 1, 1)), LOWER(SUBSTRING(name, 2))) AS name
FROM Users
ORDER BY user_id
```
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
## *12-03-2026*  

**Problem 584: Find Customer Referee**  

**problem:** Find the names of the customer that are not referred by the customer with id = 2.  
**solution**:
```
# Write your MySQL query statement below
SELECT name FROM Customer
WHERE referee_id IS NULL
OR referee_id != 2;
```
## *16-03-2026*  

**Problem 181: Employees Earning More Than Their Managers**  

**problem**: Write a solution to find the employees who earn more than their managers.  

**solution**:
```
SELECT 
    e.name AS Employee
FROM 
    Employee AS e
JOIN 
    Employee AS m 
    ON e.managerId = m.id
WHERE 
    e.salary > m.salary;
```  

## *17-03-2026*

**Problem 197: Rising Temperature**

**problem**:
Write a solution to find all dates' Id with higher temperatures compared to its previous dates (yesterday).

**solution**:
```sql
# Write your MySQL query statement below
SELECT 
    w.id 
FROM Weather AS e
INNER JOIN Weather AS w
    ON DATEDIFF(w.recordDate, e.recordDate) = 1
WHERE w.temperature > e.temperature;
```
## *18-03-2026*  

**Problem 196: Delete Duplicate Emails**  

**problem**:  
Write a solution to delete all duplicate email entries in a table named Person, keeping only unique emails based on its smallest id. (Note: write a DELETE statement and not a SELECT one.)  

**solution**:  
```
DELETE FROM Person 
WHERE id NOT IN (
    SELECT * FROM (
        SELECT MIN(id) FROM Person GROUP BY email
    ) AS temp
);
```

## *20-03-2026*  

**Problem 183: Customers Who Never Order**  

**problem**:  
Suppose that a website contains two tables, the Customers table and the Orders table. Write a solution to find all customers who never order anything.  

**solution**:  
```
SELECT c.name AS Customers
FROM Customers AS c
LEFT JOIN Orders AS o
ON c.id = o.customerId
WHERE o.id IS NULL;
```

## *22-03-2026*  

**Problem 185: Department Top Three Salaries**  

**problem:**  
A company's executives are interested in seeing who earns the most money in each of the company's departments. A high earner in a department is an employee who has a salary in the top three unique salaries for that department. Write a solution to find the employees who are high earners in each of the departments. Return the result table in any order.  

**solution**:  
```
SELECT Department, Employee, Salary
FROM (
    SELECT 
        d.name AS Department, 
        e.name AS Employee, 
        e.salary AS Salary,
        DENSE_RANK() OVER (PARTITION BY d.name ORDER BY e.salary DESC) AS rnk
    FROM Employee e
    JOIN Department d ON e.departmentId = d.id
) as temp_table
WHERE rnk <= 3;
```
## *23-03-2026*  

**Problem 577: Employee Bonus**  

**problem**: Write a solution to report the name and bonus amount of each employee with a bonus less than 1000. If an employee does not have a bonus, their name should still be reported, but with a null or empty bonus value. Return the result table in any order.  

**solution**: 
```
SELECT name, bonus FROM Employee AS e
LEFT JOIN BONUS AS b 
ON b.empId = e.empId
WHERE bonus < 1000 OR
bonus IS null;
```
## *24-03-2026*  

**Problem 595: Big Countries**  

**problem**: A country is big if it has an area of at least three million (i.e., 3,000,000), or it has a population of at least twenty-five million (i.e., 25,000,000). Write a solution to find the name, population, and area of the big countries.  

**solution**: 
```
SELECT name, population, area FROM World
WHERE area >= 3000000 OR population >= 25000000;
```
