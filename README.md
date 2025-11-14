# 📚 Library Management System using HBase & Python (HappyBase)

A scalable and distributed Library Management System built using **HBase**, **HDFS**, **Python**, and **HappyBase (Thrift API)**.  
This project demonstrates how Big Data technologies can efficiently manage library operations such as storing book details, borrowing, and returning books — all in real-time.

---

# 🖼️ System Architecture


+-------------------+ Thrift API +-------------------------+
| Python App | <---------------------> | HBase Server |
| (HappyBase Client)| | (HDFS + ZooKeeper) |
+-------------------+ +-------------------------+
| |
| |
+------------------ User Inputs -----------------+


📌 **Placeholder for architecture image:**  
`![Architecture](images/architecture.png)`

---

# 🧠 Features Demonstrated
- Real-time borrowing & returning  
- Search by ID, name, or author  
- Two-table architecture:  
  - `library_books`  
  - `borrowed_books`  
- Fault-tolerant and scalable NoSQL design  
- Python-driven backend logic  

---

# 🧩 Code Snippets

## **1️⃣ Connecting to HBase using HappyBase**
```python
import happybase

connection = happybase.Connection('localhost', port=9090)
connection.open()
print("Connected to HBase!")

Inserting Books into library_books Table

table = connection.table('library_books')

table.put(
    b'101',
    {
        b'details:book_name': b'The Great Gatsby',
        b'details:author': b'F. Scott Fitzgerald'
    }
)

print("Book inserted successfully!")

Searching for a Book

def search_book(book_id):
    table = connection.table('library_books')
    row = table.row(str(book_id).encode())
    return row

result = search_book(101)
print(result)

Borrowing a Book (Move from library_books → borrowed_books)

library = connection.table('library_books')
borrowed = connection.table('borrowed_books')

def borrow_book(book_id, borrower_name):
    book = library.row(str(book_id).encode())
    
    if not book:
        print("Book not found!")
        return
    
    # Insert into borrowed_books
    borrowed.put(
        str(book_id).encode(),
        {
            b'details:book_name': book[b'details:book_name'],
            b'details:author': book[b'details:author'],
            b'details:borrowed_by': borrower_name.encode()
        }
    )

    # Delete from library_books
    library.delete(str(book_id).encode())
    print("Book borrowed successfully!")

Returning a Book

def return_book(book_id):
    book = borrowed.row(str(book_id).encode())
    
    if not book:
        print("You do not have any borrowed books.")
        return

    library.put(
        str(book_id).encode(),
        {
            b'details:book_name': book[b'details:book_name'],
            b'details:author': book[b'details:author']
        }
    )

    borrowed.delete(str(book_id).encode())
    print("Book returned successfully!")


Sample Input / Output
Borrow Book – Example
Enter Book ID to search: 101

Book Found:
Name: The Great Gatsby
Author: F. Scott Fitzgerald

Borrow this book? (y/n): y
Enter your name: Rohan

Book borrowed successfully!

Return Book – Example
Enter your borrowed book ID: 101

Book found in your borrowed list.
Returning the book...

Book returned successfully!
