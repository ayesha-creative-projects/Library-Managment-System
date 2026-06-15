# 📚 Library Management System 

A feature-rich **console-based Library Management System** built with **C++** using **Object-Oriented Programming** principles. This system manages books, magazines, DVDs, and library members with borrowing/return functionality and late fee calculation.

---
## ✨ Technologies

- **C++ 17**
- **OOP (Classes, Inheritance, Encapsulation)**
- **File Handling** (`<fstream>`)
- **Standard Library** (`<iostream>`, `<string>`)
- **Structures** (`struct`)

---
## ✨ Features

| Feature | Description |
|---------|-------------|
| 📖 **Add Resources** | Add Books, Magazines, or DVDs with unique IDs |
| 👤 **Register Members** | Add library members with unique IDs |
| 🤝 **Borrow Resources** | Members can borrow available resources |
| ↩️ **Return Resources** | Return borrowed resources |
| 📋 **Display Resources** | View all resources in the library |
| 📚 **Member Borrowed Items** | View what a member has borrowed |
| 💰 **Late Fee Calculation** | Calculate late fees (different rates per resource type) |
| 👑 **Admin View** | Friend function to see all private data |
| 💾 **Automatic Tracking** | Tracks availability and borrowing history |

---

## 📍 The Process

I wanted to build a complete library system that feels real and useful. Started with basic add/display functions, but realized a real library needs proper search, sorting, and borrowing features. The unique ISBN validation prevents duplicate entries, while the sort functions help organize the catalog. The borrow/return system tracks available copies in real-time. File handling ensures no data is lost between sessions. Built the whole thing with OOP principles so each component (books, members, transactions) works independently while sharing the same data structure.

---

## 🎯 Component Architecture

- **Book Structure** - Stores title, ISBN, author, publisher, copies, edition
- **addBook()** - Validates ISBN uniqueness before adding
- **deleteBook()** - Finds and removes book by ISBN
- **modifyBook()** - Updates all book fields
- **searchByISBN() / searchByTitle()** - Linear search through array
- **sortByTitle()** - Bubble sort algorithm for alphabetical order
- **sortByEdition()** - Sorts same-title books by edition
- **borrowBook() / returnBook()** - Modifies copy count with validation
- **saveToFile() / loadFromFile()** - Persistent storage using fstream

---

## 🚦 Running the Project

1. Clone the repository
2. Compile: `g++ library_system.cpp -o library`
3. Run: `./library`
4. Follow the menu-driven interface

---


## 🧠 What I Learned

| Concept | Description |
|---------|-------------|
| **Inheritance** | Creating specialized classes from a base class |
| **Function Hiding** | Redefining base class functions in derived classes |
| **`this` Pointer** | Using it for method chaining and clarity |
| **Composition** | Storing objects inside other objects |
| **Friend Functions** | Granting access to private members |
| **Menu-Driven Systems** | Using do-while + switch patterns |
| **Resource Management** | Tracking availability and borrowing |

