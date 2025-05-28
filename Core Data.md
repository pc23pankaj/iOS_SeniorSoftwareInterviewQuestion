# Core Data – iOS Interview Preparation

## 🔄 Core Data Delete Rules

1. **No Action**
   - 🔹 Nothing happens when the main object is deleted. The related object stays in the database.
   - ✅ *Example:* If you delete an Employee, the linked Passport still exists.

2. **Nullify** *(Default)*
   - 🔹 The connection is set to `nil`, but the related object is not deleted.
   - ✅ *Example:* If an Employee is deleted, the `passport.employee` is set to `nil`, but the Passport remains.

3. **Cascade**
   - 🔹 Deletes all linked objects automatically.
   - ✅ *Example:* Delete an Employee → their Passport is also deleted.

4. **Deny**
   - 🔹 Prevents deletion if related objects exist.
   - ❌ *Example:* If an Employee has a Passport, you can't delete the Passport unless the Employee is removed first.
   - ⚠️ *Warning:* Use cautiously. Risk of app crashes if not handled properly.

---

## 📘 Core Data Interview Q&A

### 1. What is Core Data?
Core Data is a framework by Apple for managing model layer objects in iOS/macOS apps. It's used to save, track, modify, and filter data—but **it is not a database**.

---

### 2. What is an object graph?
An object graph is a collection of interconnected objects. Core Data manages complex object graphs and their lifecycle efficiently.

---

### 3. What is `NSManagedObjectContext`?
Manages a collection of `NSManagedObject` instances. Multiple contexts can exist, each backed by a persistent store coordinator.

---

### 4. What is the Core Data stack?
Core Data stack consists of:
- Managed Object Model
- Managed Object Context
- Persistent Store Coordinator
- Persistent Store (SQLite, XML, Binary)

---

### 5. Is Core Data the same as SQLite?
No. Core Data is not a database; it’s an object graph and persistence framework. It can use SQLite as one of its storage options.

---

### 6. What types of stores does Core Data support?
- Binary
- XML
- SQLite

---

### 7. What is Entity Inheritance?
Entities can inherit from other entities. In SQLite stores, inherited entities share the same table—may affect performance.

---

### 8. What is an Abstract Entity?
An abstract entity is never instantiated directly. Useful for common base entities like `Person` → `Employee`, `Customer`.

---

### 9. What is `NSFetchedResultsController`?
A controller for managing the results of a fetch request and integrating with `UITableView`.

---

### 10. What is `NSManagedObjectID`?
Thread-safe reference to a managed object. Use it to pass between threads safely.

---

### 11. What is a Persistent Store?
It's the physical file (SQLite/XML/Binary) used to persist managed objects.

---

### 12. What is `NSPersistentStoreCoordinator`?
Connects managed object contexts to persistent stores. Handles loading/caching data and model compatibility.

---

### 13. Can we do multithreading with Core Data?
Yes. Use multiple contexts (e.g., background context for long tasks). Always access objects from the context’s queue.

---

### 14. Minimum Required Classes and Relationships?
- `NSManagedObject`
- `NSManagedObjectContext`
- Persistent Store Coordinator
These form the foundation of Core Data operations.

---

### 15–16. Can you pass `NSManagedObject` between contexts/threads?
❌ No. Use `NSManagedObjectID` to transfer between threads or contexts safely.

---

### 17. What is Lazy Initialization?
Using `lazy` ensures Core Data stack is only initialized when accessed. Efficient for memory and performance.

---

### 18. Can `NSPersistentStoreCoordinator` have multiple stores?
Yes, but objects from different stores cannot be related directly.

---

### 19. How to fetch selected attributes?
Use `NSFetchRequest.setPropertiesToFetch` with an array of property names.

---

### 20. What is `NSAsynchronousFetchRequest`?
Fetch data without blocking the main thread. Supports cancellation and progress tracking.

---

### 21. What is Faulting?
Faulting delays the loading of object data until it's needed. Improves performance.
- Use `.isFault` to check.

---

### 22. What is `NSManagedObjectModel`?
Describes entities, attributes, and relationships. Loaded from `.xcdatamodeld` file(s).

---

### 23. What is an Attribute?
A piece of data attached to an entity (e.g., name, age, salary for `Employee`).

---

### 24. What is a Relationship?
Links between entities.
- **To-One**: e.g., Employee → Manager
- **To-Many**: e.g., Manager → Employees

---

### 25. What is `NSManagedObject`?
A dynamic, runtime representation of an entity. You can access attributes using Key-Value Coding.

---

### 26. What is Concurrency?
Allows access to Core Data on multiple queues:
- 🌲 **Main Queue Concurrency**
- 🌲 **Private Queue Concurrency**

---

### 27. What is Private Queue Concurrency?
Background queue for long-running tasks. Keeps UI responsive.

---

### 28. What is Main Queue Concurrency?
Associated with the main thread. Use for UI-bound data operations.

---

### 29. What are Wrappers?
Helper libraries to simplify Core Data API usage (e.g., syntactic sugar for inserting objects).

---

### 30. What are Synchronizers in Core Data?
Unlike adapters, synchronizers use a dedicated sync logic (not standard APIs like REST). Used for syncing across systems or stores.

---

## ✅ Summary

- Use **Cascade** for clean deletions.
- Use **Nullify** to keep related objects but remove the link.
- Avoid **Deny** unless deletion logic is well-handled.
- Always use `NSManagedObjectID` to share objects across threads.
- Use `NSAsynchronousFetchRequest` for background fetches.
