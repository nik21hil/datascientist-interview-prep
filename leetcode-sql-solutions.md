<h1 align="center">🧮 LeetCode SQL Solutions</h1> 

### EASY

#### 175. Combine Two Tables

```sql
SELECT p.firstName, p.lastName, a.city, a.state
FROM Person p
LEFT JOIN Address a 
ON p.personId = a.personId;
```

#### 181. Employees Earning More Than Their Managers
```sql
SELECT e1.name AS Employee
FROM Employee e1
JOIN Employee e2
ON e1.managerId = e2.id
WHERE e1.salary > e2.salary;
```

#### 182. Duplicate Emails
```sql
SELECT email
FROM Person
GROUP BY 1
HAVING COUNT(id)>1;
```

#### 183. Customers Who Never Order
```sql
SELECT name AS Customers
FROM Customers
WHERE id NOT IN 
(
SELECT customerId 
FROM Orders
GROUP BY 1
);
```
