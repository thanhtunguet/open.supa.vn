---
title: CookieManager
sidebar_position: 4
---

# CookieManager

The `CookieManager` system provides an abstraction layer for managing HTTP cookies in Flutter applications. It enables **platform-aware cookie storage and retrieval**—supporting both **Hive-based local persistence** for mobile and desktop, and **browser cookies** for web apps.

This design allows consistent and secure cookie handling across platforms when working with `Dio` HTTP requests.

---

## 🧩 Interface Overview

```dart
abstract class CookieManager {
  Interceptor get interceptor;

  List<Cookie> loadCookies(Uri uri);
  Cookie getSingleCookie(Uri uri, String name);
  void saveCookies(Uri uri, List<Cookie> cookies);
  void deleteCookies(Uri uri);
  void deleteAllCookies();
  String buildUrlWithToken(String url);
}
```

This interface defines the contract for:

- Attaching cookies to outgoing requests.
- Extracting and saving cookies from responses.
- Deleting cookies by URI or globally.
- Constructing URLs with access tokens for platforms that require query-based auth.

---

## 🛠 Common Use Case with Dio

```dart
final dio = Dio();
dio.interceptors.add(GetIt.I<CookieManager>().interceptor);
```

---

## 🗃 Platform Implementations

### 🐝 HiveCookieManager

Used for **mobile and desktop**. Stores cookies using the [Hive](https://pub.dev/packages/hive) database.

#### 🔧 Behavior

- Intercepts outgoing requests to inject cookies into headers.
- Saves cookies returned in the `set-cookie` response headers.
- Cookies are stored per host in a `Map<String, String>` format.
- Uses `Hive.openBox('supa_cookies')`.

#### 🔒 Token Injection

```dart
final url = manager.buildUrlWithToken(apiUrl);
// Appends token as query parameter if found in cookie storage.
```

#### 🧠 Notes

- Persistent between app launches.
- Manual initialization recommended:
  
```dart
await HiveCookieManager.create();
```

---

### 🌐 WebCookieManager

Used for **Flutter Web**. Relies on the native `document.cookie` API.

#### 🔧 Behavior

- On request: adds cookies to headers.
- On response: parses and saves cookies using `document.cookie`.
- Stores and deletes cookies using domain-based paths and expiration.

#### 🔥 Limitations

- Browser-managed, scoped by domain and path.
- No serialization beyond string pairs.
- `buildUrlWithToken()` is a no-op—authentication is cookie-based.

---

## 💡 Methods Summary

| Method               | Description                                                  |
|----------------------|--------------------------------------------------------------|
| `interceptor`        | Intercepts requests/responses to manage cookies via Dio.     |
| `loadCookies(uri)`   | Loads cookies for a given URI.                               |
| `saveCookies(uri)`   | Saves cookies to storage (Hive or browser).                  |
| `getSingleCookie()`  | Fetches a cookie by name.                                    |
| `deleteCookies(uri)` | Removes all cookies for the specified URI.                   |
| `deleteAllCookies()` | Removes all stored cookies.                                  |
| `buildUrlWithToken()`| Appends auth token as query parameter (Hive only).           |

---

## 🔒 Security Considerations

- Always validate and sanitize cookies before usage.
- Avoid exposing sensitive tokens via `buildUrlWithToken()` unless required by backend APIs.
- For secure apps, consider encrypting cookies on Hive (if needed).

---

## 📂 Location

```txt
lib/core/cookie_manager/cookie_manager.dart
lib/core/cookie_manager/hive_cookie_manager.dart
lib/core/cookie_manager/web_cookie_manager.dart
```
