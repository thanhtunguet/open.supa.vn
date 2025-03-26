---
title: PersistentStorage
sidebar_position: 3
---

# PersistentStorage

`PersistentStorage` is an abstract class that defines a **platform-agnostic contract** for storing key-value data, API configuration, and authentication state. It enables **clean separation of concerns** between business logic and storage backend, making it easier to support multiple platforms like **Web** and **Mobile/Desktop**.

---

## 🧩 Interface Overview

```dart
abstract class PersistentStorage {
  Future<void> initialize();
  void setValue(String key, String value);
  String? getValue(String key);
  void removeValue(String key);
  void clear();

  String get baseApiUrl;
  set baseApiUrl(String baseApiUrl);

  Tenant? get tenant;
  set tenant(Tenant? tenant);
  void removeTenant();

  AppUser? get appUser;
  set appUser(AppUser? appUser);
  void removeAppUser();
}
```

---

## 🌐 WebPersistentStorage

An implementation of `PersistentStorage` that uses **`window.localStorage`** for data persistence.

### 🔧 Behavior

- `baseApiUrl` is fetched from `SupaArchitecturePlatform` (read-only).
- `tenant` and `appUser` are serialized to JSON and stored as strings.
- Initialization registers itself with `GetIt`.

### ⚙️ Storage Medium

- Uses the browser’s `localStorage` API.
- All data is stringified and stored under their respective keys.

### ⚠️ Notes

- Data is not encrypted; avoid storing sensitive data.
- localStorage has limited space (~5MB depending on browser).

---

## 📱 HivePersistentStorage

An implementation that uses the **[Hive](https://pub.dev/packages/hive)** local database, optimized for mobile and desktop.

### 🔧 Boxes Used

- `_boxName = 'supa_architecture'`: General settings and API base URL.
- `_authBoxName = 'supa_auth'`: Authentication-specific data like `Tenant` and `AppUser`.

### 🛡 Reliability

- Uses structured storage (`Map<String, dynamic>`) with support for object serialization.
- Handles Hive initialization exceptions via a custom `HiveInitializationException`.

### ⚠️ Notes

- Hive is fast and offline-friendly but should be properly initialized before use.
- Be sure to call `await initialize()` before accessing storage.

---

## 🚀 Usage Example

```dart
final storage = GetIt.instance<PersistentStorage>();

await storage.initialize();

storage.setValue('theme', 'dark');

final token = storage.getValue('auth_token');

storage.tenant = Tenant(id: 'abc'); // Save tenant
final tenant = storage.tenant;      // Load tenant
```

---

## 🧠 Best Practices

- Always access the singleton instance via `GetIt` to ensure platform abstraction.
- Call `.initialize()` before usage (especially for Hive).
- Clear sensitive data (like `appUser` and `tenant`) on logout.
- Avoid storing large payloads or deeply nested structures in Web localStorage.

---

## 🗃 Key Responsibilities

| Method           | Purpose                                   |
|------------------|-------------------------------------------|
| `setValue()`     | Store a simple key-value pair             |
| `getValue()`     | Retrieve stored value                     |
| `clear()`        | Wipe all session/authentication data      |
| `tenant`         | Save and load `Tenant` from storage       |
| `appUser`        | Save and load `AppUser` from storage      |
| `baseApiUrl`     | Store or resolve base URL for API client  |

---

## 🧩 Storage Decision Table

| Platform | Implementation         | Storage Backend     |
|----------|------------------------|---------------------|
| Web      | `WebPersistentStorage` | `window.localStorage` |
| Mobile   | `HivePersistentStorage`| `Hive` boxes        |

---

## 📂 Location

```txt
lib/core/persistent_storage/persistent_storage.dart
lib/core/persistent_storage/web_persistent_storage.dart
lib/core/persistent_storage/hive_persistent_storage.dart
```
