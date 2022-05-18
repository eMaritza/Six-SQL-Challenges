/*Description
These exercises utilize the sample database from MySqlTutorial.org. You will need to have downloaded and run the installation script before attempting these exercises.
Data URL: http://www.mysqltutorial.org/mysql-sample-database.aspx


1. Write a query to display each customer’s name (as “Customer Name”) alongside the name of the employee who is responsible for that customer’s orders. The employee name should be in a single “Sales Rep” column formatted as “lastName, firstName”. The output should be sorted alphabetically by customer name.
*/

SELECT 
	customers.customerName AS 'Customer Name', 
	CONCAT(lastName,', ', firstName) AS 'Sales Rep'
FROM customers
INNER JOIN employees ON customers.salesRepEmployeeNumber = employees.employeeNumber 
ORDER BY customerName ASC;


/*2. Determine which products are most popular with our customers. For each product, list the total quantity ordered along with the total sale generated (total quantity ordered * buyPrice) for that product. The column headers should be “Product Name”, “Total # Ordered” and “Total Sale”. List the products by Total Sale descending.
*/
/*
A. For each product list the total quantity order & total sale generated (total quantity order*buyPrice)
*/
-- Get product name via productcode from the orderdetails & products tables using an INNER JOIN
SELECT 
   products.productName AS 'Product Name',
COUNT(orderdetails.quantityOrdered) AS 'Total # Ordered', (orderdetails.quantityOrdered * buyPrice) AS 'Total Sale'
FROM products
INNER JOIN orderdetails ON products.productCode = orderdetails.productCode
GROUP BY orderdetails.productCode
ORDER BY (orderdetails.quantityOrdered * buyPrice) DESC;

/*3. Write a query which lists order status and the # of orders with that status. Column headers should be “Order Status” and “# Orders”. Sort alphabetically by status.*/
SELECT 
   status AS 'Order Status',
COUNT(status) AS '# Orders'
FROM  orders 
GROUP BY status
ORDER BY status ASC;

/*4. Write a query to list, for each product line, the total # of products sold from that product line. The first column should be “Product Line” and the second should be “# Sold”. Order by the second column descending.
*/
SELECT 
  	products.productLine AS 'Product Line',
SUM(orderdetails.quantityOrdered) AS '# Sold'
FROM products
INNER JOIN orderdetails ON products.productCode = orderdetails.productCode
GROUP BY productLine
ORDER BY sum(orderdetails.quantityOrdered ) DESC;

/*5. For each employee who represents customers, output the total # of orders that employee’s customers have placed alongside the total sale amount of those orders. The employee name should be output as a single column named “Sales Rep” formatted as “lastName, firstName”. The second column should be titled “# Orders” and the third should be “Total Sales”. Sort the output by Total Sales descending. Only (and all) employees with the job title ‘Sales Rep’ should be included in the output, and if the employee made no sales the Total Sales should display as “0.00”.
*/

SELECT 
  CONCAT(lastName,', ', firstName) AS 'Sales Rep',
COUNT(orders.customerNumber) AS '# Orders',
SUM(payments.amount) AS 'Total Sales'
FROM employees
LEFT JOIN customers ON employees.employeeNumber = customers.salesRepEmployeeNumber
INNER JOIN orders ON customers.customerNumber = orders.customerNumber
INNER JOIN payments ON payments.customerNumber = orders.customerNumber
WHERE jobTitle = 'Sales Rep'
GROUP BY employees.employeeNumber
ORDER BY SUM(payments.amount) DESC;

/*6. Your product team is requesting data to help them create a bar-chart of monthly sales since the company’s inception. Write a query to output the month (January, February, etc.), 4-digit year, and total sales for that month. The first column should be labeled ‘Month’, the second ‘Year’, and the third should be ‘Payments Received’. Values in the third column should be form EXTRpaymentsACTatted as numbers with two decimals – for example: 694,292.68.
*/
SELECT 
  monthname(paymentDate) AS 'Month',
  year(paymentDate) AS 'Year',
  sum(amount) AS 'Total Payment'
FROM payments
GROUP BY month(paymentDate), year(paymentDate);