## Database Schema Documentation

## **1. Overview**

This database manages customer information, their addresses, and the orders they place.
It consists of **three tables**:

* **ADDRESSES** – Stores location details.
* **CUSTOMERS** – Stores customer information linked to an address.
* **ORDERS** – Stores order details linked to both customers and addresses.

---

## **2. Table Structures**

### **ADDRESSES**

| Column Name | Data Type | Constraints | Description                      |
| ----------- | --------- | ----------- | -------------------------------- |
| ADDRESS_ID  | INT       | PRIMARY KEY | Unique identifier for an address |
| STREET      | VARCHAR   | NOT NULL    | Street name/number               |
| CITY        | VARCHAR   | NOT NULL    | City name                        |
| STATE       | VARCHAR   | NOT NULL    | State name                       |
| ZIP_CODE    | VARCHAR   | NOT NULL    | Postal code                      |

---

### **CUSTOMERS**

| Column Name    | Data Type | Constraints | Description                       |
| -------------- | --------- | ----------- | --------------------------------- |
| CUSTOMER_ID    | INT       | PRIMARY KEY | Unique identifier for a customer  |
| CUSTOMER_NAME  | VARCHAR   | NOT NULL    | Full name of the customer         |
| MOBILE_NO      | BIGINT    | UNIQUE      | Customer's mobile number          |
| EMAIL_ID       | VARCHAR   | UNIQUE      | Customer's email address          |
| ADDRESS_ID     | INT       | FOREIGN KEY | References ADDRESSES(ADDRESS\_ID) |

---

### **ORDERS**

| Column Name  | Data Type | Constraints | Description                                |
| ------------ | --------- | ----------- | ------------------------------------------ |
| ORDER_ID     | INT       | PRIMARY KEY | Unique identifier for an order             |
| ORDER_TYPE   | VARCHAR   | NOT NULL    | Type of the order (e.g., Online, In-Store) |
| CUSTOMER_ID  | INT       | FOREIGN KEY | References CUSTOMERS(CUSTOMER\_ID)         |
| ADDRESS_ID   | INT       | FOREIGN KEY | References ADDRESSES(ADDRESS\_ID)          |

---

## **3. Relationships**

* **CUSTOMERS → ADDRESSES**
  Each customer is linked to exactly one address.
* **ORDERS → CUSTOMERS**
  Each order belongs to a customer.
* **ORDERS → ADDRESSES**
  Each order has a delivery or billing address.

---

## **4. ER Diagram**

<img width="1303" height="930" alt="Joins" src="https://github.com/user-attachments/assets/24381265-f155-4420-afa6-f27acd29e45d" />

---

## **5. Joins Overview**

### **INNER JOIN**

Returns rows where there is a match in both tables.

-- sql
SELECT CUSTOMERS.CUSTOMER_NAME, ORDERS.ORDER_TYPE
FROM CUSTOMERS
INNER JOIN ORDERS
ON CUSTOMERS.CUSTOMER_ID = ORDERS.CUSTOMER_ID;

### **LEFT JOIN**

Returns all rows from the left table, and matching rows from the right table.

-- sql
SELECT CUSTOMERS.CUSTOMER_NAME, ORDERS.ORDER_TYPE
FROM CUSTOMERS
LEFT JOIN ORDERS
ON CUSTOMERS.CUSTOMER_ID = ORDERS.CUSTOMER_ID;

### **RIGHT JOIN**

Returns all rows from the right table, and matching rows from the left table.

-- sql
SELECT CUSTOMERS.CUSTOMER_NAME, ORDERS.ORDER_TYPE
FROM CUSTOMERS
RIGHT JOIN ORDERS
ON CUSTOMERS.CUSTOMER_ID = ORDERS.CUSTOMER_ID;

### **FULL OUTER JOIN** (MySQL Alternative: `UNION` of LEFT and RIGHT JOINs)

-- sql
SELECT CUSTOMERS.CUSTOMER_NAME, ORDERS.ORDER_TYPE
FROM CUSTOMERS
LEFT JOIN ORDERS
ON CUSTOMERS.CUSTOMER_ID = ORDERS.CUSTOMER_ID
UNION
SELECT CUSTOMERS.CUSTOMER_NAME, ORDERS.ORDER_TYPE
FROM CUSTOMERS
RIGHT JOIN ORDERS
ON CUSTOMERS.CUSTOMER_ID = ORDERS.CUSTOMER_ID;
