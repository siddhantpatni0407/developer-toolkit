# MongoDB Commands

This guide lists the **most commonly used MongoDB commands** for Windows (via `mongosh` or Compass), including advanced queries, aggregation, indexes, users, and database management.

---

## 1. Connect to MongoDB

```powershell
mongosh
```

- Default connection: `mongodb://localhost:27017`
- Connect to a specific database:

```powershell
mongosh "mongodb://localhost:27017/myDatabase"
```

---

## 2. Show Databases

```js
show dbs
```

- Shows databases with at least one collection with data.
- Check current database:

```js
db;
```

---

## 3. Create / Switch Database

```js
use myDatabase
```

- Creates the database if it does not exist.
- Confirm creation after adding data:

```js
show dbs
```

---

## 4. Show Collections

```js
show collections
```

- Lists collections in the current database.
- Create a collection explicitly:

```js
db.createCollection("users");
```

---

## 5. Create / Insert Documents

```js
db.users.insertOne({
  name: "Siddhant",
  email: "siddhant@example.com",
  status: "active",
});
db.users.insertMany([
  { name: "John", email: "john@example.com" },
  { name: "Jane", email: "jane@example.com" },
]);
```

- Insert with `_id` field explicitly:

```js
db.users.insertOne({ _id: 101, name: "Mike" });
```

---

## 6. Read Documents

```js
db.users.find(); // all documents
db.users.find({ name: "John" }); // filter by field
db.users.find().pretty(); // formatted output
db.users.find({}, { name: 1, email: 1 }); // project specific fields
db.users.find().sort({ name: 1 }); // ascending sort
db.users.find().limit(2); // limit results
```

---

## 7. Update Documents

```js
db.users.updateOne({ name: "John" }, { $set: { email: "john@example.com" } });
db.users.updateMany({ status: "inactive" }, { $set: { status: "active" } });
db.users.replaceOne(
  { name: "Jane" },
  { name: "Jane Doe", email: "jane.doe@example.com" }
);
```

- Upsert (insert if not exist):

```js
db.users.updateOne(
  { name: "Sam" },
  { $set: { email: "sam@example.com" } },
  { upsert: true }
);
```

---

## 8. Delete Documents

```js
db.users.deleteOne({ name: "Jane" });
db.users.deleteMany({ status: "inactive" });
```

---

## 9. Drop Collection / Database

```js
db.users.drop();
db.dropDatabase();
```

---

## 10. Indexes

```js
db.users.createIndex({ email: 1 }); // ascending
db.users.createIndex({ name: 1, email: -1 }); // compound index
db.users.getIndexes();
db.users.dropIndex("email_1");
```

- List all indexes in a database:

```js
db.getCollectionNames().forEach((c) => print(c, db[c].getIndexes()));
```

---

## 11. Aggregation Examples

```js
// Count users by status
db.users.aggregate([{ $group: { _id: "$status", count: { $sum: 1 } } }]);

// Project specific fields with computed field
db.users.aggregate([
  {
    $project: { name: 1, email: 1, domain: { $substrBytes: ["$email", 0, 5] } },
  },
]);

// Filter + Group + Sort
db.users.aggregate([
  { $match: { status: "active" } },
  { $group: { _id: "$role", total: { $sum: 1 } } },
  { $sort: { total: -1 } },
]);
```

---

## 12. User Management

```js
// Create user
db.createUser({
  user: "admin",
  pwd: "password123",
  roles: [{ role: "readWrite", db: "myDatabase" }]
});

// Show users
show users;

// Authenticate
db.auth("admin", "password123");
```

---

## 13. Backup & Restore

```powershell
# Backup database
mongodump --db myDatabase --out C:\backups\myDatabaseBackup

# Restore database
mongorestore --db myDatabase C:\backups\myDatabaseBackup\myDatabase
```

---

## 14. Miscellaneous

- Count documents:

```js
db.users.countDocuments();
```

- Show database stats:

```js
db.stats();
```

- Show collection stats:

```js
db.users.stats();
```

- Drop all indexes from a collection:

```js
db.users.dropIndexes();
```

- Rename collection:

```js
db.users.renameCollection("users_backup");
```

---

## ✅ Tips & Best Practices

- Use `mongosh` for CLI operations; Compass for GUI.
- Always add `_id` for critical collections.
- Index fields that are frequently queried to improve performance.
- Use aggregation pipelines for advanced queries instead of multiple `find` queries.
- Regularly backup your databases using `mongodump`.
- Use roles and authentication for production environments.

---
