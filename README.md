# 📚 Library Management System (OOP Edition)

A feature-rich **console-based Library Management System** built with **C++** using **Object-Oriented Programming** principles. This system manages books, magazines, DVDs, and library members with borrowing/return functionality and late fee calculation.

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

## 🏗️ Class Hierarchy
LibraryResource (Base Class)
├── Book (Rs. 5/day late fee)
├── Magazine (Rs. 3/day late fee)
└── DVD (Rs. 10/day late fee)

Library (Manages all resources)
LibraryMember (Manages members and borrowed items)

##🧠 What I Learned

Inheritance – Creating specialized classes from a base class
Function Hiding – Redefining base class functions in derived classes
this Pointer – Using it for method chaining and clarity
Composition – Storing objects inside other objects
Friend Functions – Granting access to private members
Menu-Driven Systems – Using do-while + switch patterns
Resource Management – Tracking availability and borrowing

