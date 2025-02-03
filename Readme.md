### **Full-Stack Developer Assignment: Optimized Payments Querying & Listing**  

## **Task**  
You will build a **Payment Records Management System** that efficiently lists and queries millions of payment transactions.  

### **Scenario:**  
A fintech company maintains **millions of payment transactions**. Admins need a dashboard to:  
1. **List & paginate** through millions of records.  
2. **Search & filter** payments by amount, date range, and status.  
3. **Optimize queries** for fast response times.  
4. **Handle large datasets** efficiently on the frontend.  

---

## **Requirements**  

### **1. Backend** (Node.js + Express / Python + FastAPI / any framework of your choice)  
- Implement an **API to fetch payments** with pagination and filtering.  
- Optimize queries to handle millions of records efficiently.  
- Implement **indexing strategies** for fast lookups.  
- Ensure proper error handling and logging.  

#### **Example API Endpoints:**  
```http
GET /payments?page=1&limit=50  
GET /payments?search=John&page=1&limit=50  
GET /payments?minAmount=100&maxAmount=5000&status=success&page=1&limit=50  
```

---

### **2. Frontend** (React / Vue / any framework of your choice)  
- Render **millions of records efficiently** using **virtualized scrolling**.  
- Implement **search, filtering, and sorting**.  
- Optimize API calls to prevent unnecessary re-fetching.  

---

### **3. Debugging Challenge**  
Fix and optimize the following inefficient SQL query:  

```sql
SELECT * FROM payments WHERE status = 'success' ORDER BY created_at DESC;
```

**Hint:** Consider indexing and pagination strategies.  

---

### **4. Architectural Thinking**  
- How would you **scale** this system to handle **real-time payments**?  
- What **database optimizations** would you apply to prevent slow queries?  
- How would you **implement caching** for frequently accessed queries?  

---

### **Evaluation Criteria**  
- **Code Quality**: Clean, modular, and follows best practices.  
- **Performance Optimization**: Efficient SQL queries, indexing, and frontend performance.  
- **Debugging & Problem-Solving**: Ability to identify and fix performance bottlenecks.  
- **Architecture & Scalability Thinking**: Handling large datasets efficiently.  
- **Time Efficiency**: The ability to implement a solution within a few hours.  

---

### **SQL Schema for Sample Payments Data**  
Here’s an SQL file (`payments.sql`) that generates a **large dataset of payment records** with indexes for optimized querying.  

```sql
CREATE TABLE payments (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    user_id BIGINT NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    currency VARCHAR(3) NOT NULL DEFAULT 'USD',
    status ENUM('pending', 'success', 'failed') NOT NULL,
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_status (status),
    INDEX idx_created_at (created_at),
    INDEX idx_user_id (user_id)
);

-- Generate 1 million sample records
INSERT INTO payments (user_id, amount, currency, status, created_at)
SELECT 
    FLOOR(RAND() * 1000000), 
    ROUND(RAND() * 10000, 2), 
    'USD', 
    ELT(FLOOR(1 + (RAND() * 3)), 'pending', 'success', 'failed'), 
    NOW() - INTERVAL FLOOR(RAND() * 365) DAY
FROM 
    (SELECT 1 UNION SELECT 2 UNION SELECT 3 UNION SELECT 4 UNION SELECT 5) t1,
    (SELECT 1 UNION SELECT 2 UNION SELECT 3 UNION SELECT 4 UNION SELECT 5) t2,
    (SELECT 1 UNION SELECT 2 UNION SELECT 3 UNION SELECT 4 UNION SELECT 5) t3,
    (SELECT 1 UNION SELECT 2 UNION SELECT 3 UNION SELECT 4 UNION SELECT 5) t4;
```

---

### **Submission**  
- Provide a **GitHub repository** with your solution.  
- Include a **README** with setup steps and architectural decisions.  
- Mention **optimizations** or improvements you made.  

---
