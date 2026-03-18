CREATE DATABASE retail_portfolio;
USE retail_portfolio;

CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    city VARCHAR(50),
    country VARCHAR(50),
    signup_date DATE
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10,2)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    status VARCHAR(20),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

CREATE TABLE order_items (
    order_item_id INT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT,
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);


INSERT INTO customers VALUES
(1,'John','Smith','john@email.com','New York','USA','2023-01-10'),
(2,'Emma','Brown','emma@email.com','Los Angeles','USA','2023-02-15'),
(3,'Liam','Wilson','liam@email.com','London','UK','2023-03-20'),
(4,'Olivia','Taylor','olivia@email.com','Manchester','UK','2023-04-12'),
(5,'Noah','Davis','noah@email.com','Toronto','Canada','2023-05-05');

INSERT INTO products VALUES
(1,'Laptop','Electronics',1200),
(2,'Phone','Electronics',800),
(3,'Headphones','Electronics',150),
(4,'Desk Chair','Furniture',300),
(5,'Coffee Table','Furniture',250);

INSERT INTO orders VALUES
(101,1,'2024-01-10','Completed'),
(102,2,'2024-01-12','Completed'),
(103,1,'2024-02-05','Completed'),
(104,3,'2024-02-20','Completed'),
(105,4,'2024-03-15','Completed'),
(106,5,'2024-03-18','Completed'),
(107,2,'2024-04-10','Completed');

INSERT INTO order_items VALUES
(1,101,1,1),
(2,101,3,2),
(3,102,2,1),
(4,103,4,1),
(5,104,1,1),
(6,104,5,1),
(7,105,3,3),
(8,106,2,1),
(9,107,1,1);


-- total revenue
SELECT 
    SUM(p.price * oi.quantity) AS total_revenue
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id;


-- revenue by country
SELECT 
    c.country,
    SUM(p.price * oi.quantity) AS revenue
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN order_items oi ON o.order_id = oi.order_id
JOIN products p ON oi.product_id = p.product_id
GROUP BY c.country
ORDER BY revenue DESC;


-- top Selling Products
SELECT 
    p.product_name,
    SUM(oi.quantity) AS total_quantity_sold,
    SUM(p.price * oi.quantity) AS total_sales
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_sales DESC;



-- Monthly Revenue Trend
SELECT 
    DATE_FORMAT(o.order_date, '%Y-%m') AS month,
    SUM(p.price * oi.quantity) AS monthly_revenue
FROM orders o
JOIN order_items oi ON o.order_id = oi.order_id
JOIN products p ON oi.product_id = p.product_id
GROUP BY month
ORDER BY month;

-- Customer Lifetime Value (CLV)
SELECT 
    c.customer_id,
    CONCAT(c.first_name,' ',c.last_name) AS customer_name,
    SUM(p.price * oi.quantity) AS lifetime_value
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN order_items oi ON o.order_id = oi.order_id
JOIN products p ON oi.product_id = p.product_id
GROUP BY c.customer_id, customer_name
ORDER BY lifetime_value DESC;



