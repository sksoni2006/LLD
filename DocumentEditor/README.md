#  Document Editor - LLD Implementation

A modular, extensible **Low-Level Design (LLD)** of a Document Editor built using C++. This project demonstrates how to handle various document elements (Text, Images, Formatting) while maintaining a decoupled storage system (File, DB).

##  Features

* **Polymorphic Rendering:** Supports multiple elements like `Text`, `Images`, `New Lines`, and `Tabs` using a common interface.
* **Pluggable Persistence:** Easily switch between `FileStorage` and `DBStorage` without modifying the core editor logic.
* **Lazy Rendering:** Implements basic caching in the editor to avoid re-rendering unless necessary.
* **Clean Architecture:** Strictly follows SOLID principles for maintainability.

---

##  System Architecture (UML)

The system is designed using a **Composition-based Architecture**.

* **DocumentElement (Interface):** The base for all components.
* **Document (Container):** Uses the **Composite Pattern** logic to manage a collection of elements.
* **Persistence (Interface):** Follows the **Strategy Pattern** to allow different saving mechanisms.

---

##  Design Principles Applied

### 1. Single Responsibility Principle (SRP)

* `Document` is only responsible for managing elements.
* `Persistence` is only responsible for saving data.
* `DocumentEditor` acts as the orchestrator.

### 2. Open/Closed Principle (OCP)

You can add new elements (e.g., `TableElement`, `VideoElement`) by simply inheriting from `DocumentElement` without changing the `Document` or `DocumentEditor` classes.

### 3. Dependency Inversion Principle (DIP)

`DocumentEditor` does not depend on `FileStorage`. It depends on the `Persistence` abstraction. This allows us to swap storage types at runtime.

---

##  Code Explanation

### Core Components

| Class | Description |
| --- | --- |
| `DocumentElement` | Abstract Base Class with a pure virtual `render()` function. |
| `TextElement` | Handles raw string data. |
| `ImageElement` | Handles image paths and renders them in a specific format. |
| `Document` | Holds a `std::vector<DocumentElement*>`. Iterates through them to build the final string. |
| `Persistence` | Abstract interface for saving logic (`save` method). |
| `DocumentEditor` | The high-level API used by the client to interact with the system. |

---

##  How to Run

1. **Prerequisites:** Ensure you have a C++ compiler (GCC/Clang) installed.
2. **Compilation:**
```bash
g++ -o editor DocumentEditor.cpp

```


3. **Execution:**
```bash
./editor

```

---
