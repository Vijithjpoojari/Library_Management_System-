# 📚 Library Management System using HBase & Python (HappyBase)

## 🧾 Project Overview
This project implements a **scalable and distributed Library Management System** using **HBase**, a NoSQL database built on HDFS, with a Python backend integrated via **HappyBase (Thrift API)**.  
It manages book records, user transactions, and real-time updates while demonstrating how Big Data technologies can be applied in real-world systems.

---

## 📝 Abstract
This project presents the development of a distributed **Library Management System** using **HBase** integrated with Python's HappyBase client. The system stores book details, manages borrow/return operations, and tracks user activity using two HBase tables.  
It highlights the scalability and performance of HBase while showcasing how Big Data tools can support efficient data management at scale.  

**Key Highlights:**
- Two HBase tables:
  - `library_books` → stores book details  
  - `borrowed_books` → tracks borrowed books and user info  
- Real-time read/write operations  
- Python + HBase integration using Thrift server  
- Scalability, high performance & fault tolerance  
- Supports search, borrow, and return functionalities  

---

## 📑 Table of Contents
- Introduction  
- Literature Review  
- Problem Statement  
- Methodology  
- Results & Discussion  
- Conclusion  

---

# 🏗️ 1. Introduction
Managing large volumes of library records requires a system that can scale, support distributed storage, and process updates in real time. Traditional relational databases struggle with these demands.

**HBase** offers:
- Horizontal scalability  
- High performance and low latency  
- Distributed architecture  
- Efficient column-family storage  

Python’s **HappyBase** provides simple APIs to perform CRUD operations using the Thrift server.

---

# 📚 2. Literature Review
Research identifies HBase as a robust NoSQL solution capable of managing massive datasets with real-time access. Studies show its use in:
- Social media messaging systems  
- Large medical databases  
- Cloud-scale storage systems  
- Highly elastic data infrastructures  

These findings support the selection of HBase for scalable library management.

---

# ❗ 3. Problem Statement
Traditional library systems face challenges such as:
- Poor scalability  
- Slow real-time updates  
- Complex data management  
- Limited user experience  

**Objective:**  
Design a scalable library management system using **HBase** to efficiently store, retrieve, and update book and user transaction data.

**Key Features Required:**
- Book insertion  
- Search by ID, name, or author  
- Borrow & return actions  
- Real-time tracking  
- Distributed handling of large datasets  

---

# ⚙️ 4. Methodology

### **System Setup**
- Install & configure HBase, HDFS, and ZooKeeper  
- Configure Thrift server for Python connectivity  
- Set up Python environment with HappyBase  

### **Database Design**
Two main HBase tables:

| Table Name        | Column Families         | Purpose |
|------------------|-------------------------|----------|
| `library_books`  | `details:` (name, author) | Stores available books |
| `borrowed_books` | `details:` (name, author, borrowed_by) | Tracks borrowed books |

### **Workflow**
#### **Borrowing Books**
- User searches by ID/name/author  
- If available → book moves from `library_books` → `borrowed_books`  

#### **Returning Books**
- User identifies borrowed book  
- Book moves back to `library_books`  

### **Real-Time Updates**
HBase writes through:
- WAL (Write-Ahead Log)  
- MemStore  
- HFiles  
Ensuring **fault tolerance** and **real-time consistency**.

### **Optimization**
- Bloom filters for fast reads  
- Block caching  
- Region splitting for scalability  

---

# 📊 5. Results & Discussion

### ✔️ Key Results
- **Horizontal Scalability:** Handles large datasets smoothly  
- **Real-Time Processing:** Immediate borrow/return updates  
- **Fast Queries:** Efficient search using row keys  
- **User-Friendly Workflow:** Clear interactions for borrowing and returning  

### 🔍 Discussion
The system performs significantly better than relational DBMS for large data volumes.  
It ensures:
- Fast access  
- Consistency  
- Flexibility  

**Areas for Improvement:**
- Add authentication security  
- Implement due dates & penalties  
- Include book categorization  
- Improve UI/UX  

---

# 🏁 6. Conclusion
This project demonstrates that **HBase** is a powerful solution for large-scale library systems.  
It provides:
- High scalability  
- Real-time performance  
- Efficient data management  

Future extensions may include:  
✔️ Encryption & access control  
✔️ Advanced search engine  
✔️ Integration with cloud Big Data tools  
✔️ Recommendation system for books  

---

## 📂 Project Structure
