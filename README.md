# Customer Orders Insights – Oracle SQL & PL/SQL

**Author:** Sudipta Gouda  
**Location:** Berhampur, Odisha, India  
**Timeline:** 2023–2024  
**Project Type:** Self-Initiated Portfolio Project  
**Status:** Completed  

---

## Tools & Technologies

- **Database:** Oracle SQL, PL/SQL  
- **Techniques:** Joins, Indexing, Stored Procedures, Functions, Analytical Functions  
- **Platform:** Oracle SQL Developer  

---

## Objective

To analyze customer order patterns and product demand by leveraging Oracle SQL and PL/SQL, simulating real-world business analytics for large datasets.

---

## Implementation Details

 **1. Table Creation:**

-- CUSTOMERS TABLE

    CREATE TABLE CUSTOMERS (
    CUSTOMER_ID NUMBER PRIMARY KEY,
    NAME VARCHAR2(100),
    CITY VARCHAR2(50) 
    );

-- PRODUCTS TABLE

    CREATE TABLE PRODUCTS (
    PRODUCT_ID NUMBER PRIMARY KEY,
    PRODUCT_NAME VARCHAR2(100),
    CATEGORY VARCHAR2(50),
    PRICE NUMBER
    );

-- ORDERS TABLE

    CREATE TABLE ORDERS (
    ORDER_ID NUMBER PRIMARY KEY,
    CUSTOMER_ID NUMBER,
    PRODUCT_ID NUMBER,
    QUANTITY NUMBER,
    ORDER_DATE DATE,
    FOREIGN KEY (CUSTOMER_ID) REFERENCES CUSTOMERS(CUSTOMER_ID),
    FOREIGN KEY (PRODUCT_ID) REFERENCES PRODUCTS(PRODUCT_ID)
    );

---

**2. Inserting Sample Data:**

-- CUSTOMERS TABLE

	INSERT INTO CUSTOMERS VALUES (1, 'AMIT SHARMA', 'DELHI');
	INSERT INTO CUSTOMERS VALUES (2, 'SNEHA PATIL', 'MUMBAI');
	INSERT INTO CUSTOMERS VALUES (3, 'RAVI VERMA', 'BANGALORE');
	INSERT INTO CUSTOMERS VALUES (4, 'NISHA REDDY', 'HYDERABAD');
	INSERT INTO CUSTOMERS VALUES (5, 'ARJUN DAS', 'KOLKATA');

-- PRODUCTS TABLE

	INSERT INTO PRODUCTS VALUES (101, 'LAPTOP', 'ELECTRONICS', 55000);
	INSERT INTO PRODUCTS VALUES (102, 'SMARTPHONE', 'ELECTRONICS', 30000);
	INSERT INTO PRODUCTS VALUES (103, 'BOOK - SQL GUIDE', 'BOOKS', 500);
	INSERT INTO PRODUCTS VALUES (104, 'WASHING MACHINE', 'APPLIANCES', 18000);
	INSERT INTO PRODUCTS VALUES (105, 'HEADPHONES', 'ELECTRONICS', 1500);

-- ORDERS TABLE

	INSERT INTO ORDERS VALUES (1001, 1, 101, 1, TO_DATE('2023-11-01', 'YYYY-MM-DD'));
	INSERT INTO ORDERS VALUES (1002, 2, 103, 3, TO_DATE('2023-11-05', 'YYYY-MM-DD'));
	INSERT INTO ORDERS VALUES (1003, 3, 102, 2, TO_DATE('2023-12-15', 'YYYY-MM-DD'));
	INSERT INTO ORDERS VALUES (1004, 1, 105, 1, TO_DATE('2024-01-10', 'YYYY-MM-DD'));
	INSERT INTO ORDERS VALUES (1005, 4, 104, 1, TO_DATE('2024-02-20', 'YYYY-MM-DD'));

---

**3. Identifying Top-Selling Products and Customer Trends Using Oracle Ranking Techniques:**

-- TOP 3 PRODUCTS BASED ON SALES QUANTITY

	SELECT * FROM (
	    SELECT PRODUCT_ID, SUM(QUANTITY) AS TOTAL_SOLD
	    FROM ORDERS
	    GROUP BY PRODUCT_ID
	    ORDER BY TOTAL_SOLD DESC
	)
	WHERE ROWNUM <= 3;

<img width="630" height="200" alt="Screenshot 2025-07-24 175805" src="https://github.com/user-attachments/assets/f2c32f57-d91c-481b-88bf-af00fbae84a5" />


-- TOP PRODUCT PER CUSTOMER USING ROW_NUMBER()

	SELECT *
	FROM (
	    SELECT CUSTOMER_ID, PRODUCT_ID, QUANTITY,
	           ROW_NUMBER() OVER (PARTITION BY CUSTOMER_ID ORDER BY QUANTITY DESC) AS RN
	    FROM ORDERS
	)
	WHERE RN = 1;

<img width="861" height="307" alt="Screenshot 2025-07-24 175855" src="https://github.com/user-attachments/assets/f7494659-b0d0-44df-91fd-3a1a959da954" />


---

**4. Automating Monthly Sales Insights Using PL/SQL Procedure:**

This procedure calculates and displays monthly total sales for a specified year. It aggregates order quantities and prices, helping simulate real-world business reporting and automation using Oracle PL/SQL and DBMS_OUTPUT.

SET SERVEROUTPUT ON;

-- PROCEDURE CREATION

	  CREATE OR REPLACE PROCEDURE MONTHLY_SALES_SUMMARY (
	    YEAR_INPUT IN NUMBER
	)
	AS
	BEGIN
	    FOR REC IN (
	        SELECT 
	            TO_CHAR(ORDER_DATE, 'MM') AS MONTH,
	            SUM(P.PRICE * O.QUANTITY) AS TOTAL_SALES
	        FROM ORDERS O
	        JOIN PRODUCTS P ON O.PRODUCT_ID = P.PRODUCT_ID
	        WHERE EXTRACT(YEAR FROM O.ORDER_DATE) = YEAR_INPUT
	        GROUP BY TO_CHAR(ORDER_DATE, 'MM')
	    )
	    LOOP
	        DBMS_OUTPUT.PUT_LINE('MONTH: ' || REC.MONTH || ' | TOTAL SALES: ' || REC.TOTAL_SALES);
	    END LOOP;
	END;

-- EXECUTE PROCEDURE

	EXEC MONTHLY_SALES_SUMMARY(2024);

<img width="780" height="318" alt="Screenshot 2025-07-24 180113" src="https://github.com/user-attachments/assets/5a3bb6bd-1975-4dd3-8140-9880659ec227" />


---

**5. Calculating Average Customer Spend Using PL/SQL Function:**

This user-defined function returns the average amount spent by a specific customer. It uses joins between orders and products to compute the total value of purchases, providing a modular and reusable analytics logic in Oracle PL/SQL.

--CREATING FUNCTION

	CREATE OR REPLACE FUNCTION AVG_CUSTOMER_SPEND(CUST_ID IN NUMBER)
	RETURN NUMBER
	AS
	    AVG_SPEND NUMBER;
	BEGIN
	    SELECT AVG(P.PRICE * O.QUANTITY)
	    INTO AVG_SPEND
	    FROM ORDERS O
	    JOIN PRODUCTS P ON O.PRODUCT_ID = P.PRODUCT_ID
	    WHERE O.CUSTOMER_ID = CUST_ID;
	
	    RETURN AVG_SPEND;
	END;

-- CALL FUNCTION

	SELECT AVG_CUSTOMER_SPEND(1) AS AVG_CUSTOMER_TOTAL_SPENT FROM DUAL;

<img width="1172" height="234" alt="Screenshot 2025-07-24 180320" src="https://github.com/user-attachments/assets/590fab1d-1537-41b4-b808-8bb4e46214a8" />

---

**6. Ranking Customer Purchase Activity Using Analytical Functions**
This query uses Oracle’s RANK() and ROW_NUMBER() functions to rank product quantities ordered by each customer. Analytical functions help in generating business insights like top purchases, trends, and comparisons without collapsing grouped data.

	SELECT 
	    CUSTOMER_ID,
	    PRODUCT_ID,
	    QUANTITY,
	    RANK() OVER (PARTITION BY CUSTOMER_ID ORDER BY QUANTITY DESC) AS QUANTITY_RANK
	FROM ORDERS;

<img width="1167" height="305" alt="Screenshot 2025-07-24 180414" src="https://github.com/user-attachments/assets/9d3a9c48-6dfe-4bff-8462-9e2f60845700" />





