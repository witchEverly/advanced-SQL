


### Table 1: Students

| StudentID | Name      | Subjects                |
|-----------|-----------|-------------------------|
| 1         | Alice     | Math, Science           |
| 2         | Bob       | History                 |
| 3         | Carol     | Math, Science, History  |


> Not in any of the normal forms because it is not atomic in Subjects column.

---


### Table 2: Orders

| OrderID | ProductID | Quantity | PricePerUnit |
|---------|-----------|----------|--------------|
| 1       | A         | 2        | 10           |
| 2       | A         | 1        | 10           |
| 3       | B         | 3        | 20           |



> In 1NF, but not in 2NF because ProductID is not fully dependent on OrderID.
If the primary key was a composite key (OrderID , ProductID) would it be in 2NF? 
Yes, because even though price per unit is not unique 
it **_depends on the composite key to exist_**. So does Quantity. 



---

### Table 3: CustomerOrders

| CustomerID | OrderID | ProductName | Quantity |
|------------|---------|-------------|----------|
| 1          | 1       | Apple       | 2        |
| 1          | 2       | Banana      | 3        |
| 2          | 3       | Apple       | 1        |




If orderID is primary then it is in 1NF, and this should not matter for order of columns correct?
In this case, the table would not be 2NF because CustomerID is not needed for Customer Orders. 
This one is more confusing. 



---


### Table 4: Employees

| EmployeeID | Name  | Department  | Salary |
|------------|-------|-------------|--------|
| 1          | Eve   | Sales       | 5000   |
| 2          | Dave  | Engineering | 6000   |
| 3          | Frank | Sales       | 5000   |


> 1NF no repeating groups and has primary key, 2NF ,  ~~but the columns are not transitive, so it's not 3NF~~ (See GPT answer).

---


## GPT Solutions: 

<summary>

<details>

### Table 1
You're absolutely correct. The "Subjects" column contains a list of subjects, making the table not atomic and therefore not in 1NF.

### Table 2
You pointed out that this table is in 1NF but not in 2NF, citing that `ProductID` is not fully dependent on `OrderID`. That's correct. If the primary key were a composite of `OrderID` and `ProductID`, then all attributes would indeed be fully functionally dependent on the entire composite key, making it in 2NF.

### Table 3
This table can be a bit confusing. If `OrderID` is the primary key, then it's in 1NF. But you correctly noted that it wouldn't be in 2NF because `ProductName` and `Quantity` could be considered dependent on `CustomerID` as well, which is not part of the primary key. If the primary key were a composite (`CustomerID`, `OrderID`), then the table would be in 2NF since all non-key attributes are fully functionally dependent on the composite key.

### Table 4
You got it right again: it's in 1NF and 2NF. However, you mentioned it's not in 3NF because it's "not transitive." Just to clarify, 3NF requires that there are no transitive dependencies of non-key attributes on the primary key. In this case, all non-key attributes (`Name`, `Department`, `Salary`) are directly dependent on the primary key (`EmployeeID`) and not on other non-key attributes. So actually, this table would be in 3NF.



</details>

</summary>


