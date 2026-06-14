# 📚 Library Management System

A console-based **Library Management System** built with **C++** that helps manage books efficiently.  
Perfect for small libraries or learning file handling, structures, and menu-driven programming.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| ➕ Add Book | Add new books with unique ISBN validation |
| ❌ Delete Book | Remove a book by ISBN |
| ✏️ Modify Book | Update book details (title, author, publisher, copies, edition) |
| 🔍 Search by ISBN | Find a book using its unique ISBN |
| 🔎 Search by Title | Find a book using its title |
| 📖 Sort by Title | Sort all books alphabetically by title |
| 📘 Sort by Edition | Sort books with same title by edition number |
| 🤝 Borrow Book | Decrease available copies when borrowing |
| ↩️ Return Book | Increase available copies when returning |
| 📋 Display All Books | Show all books in the library |
| 💾 Auto-Save | Automatically saves data to `library.txt` |
| 📂 Load on Start | Loads saved data when program runs |

---

## 🛠️ Technologies Used

- **C++** (Core language)
- File Handling (`<fstream>`)
- Strings (`<string>`)
- Algorithms (`<algorithm>` for `swap`)

---

## 🚀 How to Run

### 1. Compile the code
```bash
g++ library.cpp -o library
