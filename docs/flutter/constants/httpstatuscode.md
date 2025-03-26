---
title: HttpStatusCode
sidebar_position: 2
---

# HttpStatusCode

The `HttpStatusCode` class provides a centralized collection of commonly used **HTTP status codes**, grouped by their respective categories: success, redirection, client error, and server error.

This makes it easier to avoid magic numbers, improve code readability, and reduce typos when working with HTTP responses.

---

## ✅ Usage Example

```dart
if (response.statusCode == HttpStatusCode.ok) {
  print('Request succeeded!');
} else if (response.statusCode == HttpStatusCode.notFound) {
  print('Resource not found.');
}
```

---

## 📚 Available Constants

### ✅ 2xx — Success

| Name         | Code | Description                  |
|--------------|------|------------------------------|
| `ok`         | 200  | Standard success response    |
| `created`    | 201  | Resource successfully created|
| `accepted`   | 202  | Request accepted for processing |
| `noContent`  | 204  | Success with no response body|

---

### 🔁 3xx — Redirection

| Name                 | Code |
|----------------------|------|
| `movedPermanently`   | 301  |
| `found`              | 302  |
| `seeOther`           | 303  |
| `notModified`        | 304  |
| `temporaryRedirect`  | 307  |
| `permanentRedirect`  | 308  |

---

### 🚫 4xx — Client Errors

| Name                 | Code |
|----------------------|------|
| `badRequest`         | 400  |
| `unauthorized`       | 401  |
| `paymentRequired`    | 402  |
| `forbidden`          | 403  |
| `notFound`           | 404  |
| `methodNotAllowed`   | 405  |
| `notAcceptable`      | 406  |
| `requestTimeout`     | 408  |
| `conflict`           | 409  |
| `gone`               | 410  |
| `unprocessableEntity`| 422  |
| `tooManyRequests`    | 429  |

---

### 💥 5xx — Server Errors

| Name                 | Code |
|----------------------|------|
| `internalServerError`| 500  |
| `notImplemented`     | 501  |
| `badGateway`         | 502  |
| `serviceUnavailable` | 503  |
| `gatewayTimeout`     | 504  |

---

## 🛠 Best Practices

- Use these constants in your API clients and error handlers to **improve clarity**.
- Map status codes to custom exceptions or UI messages for better UX.

---

## 📂 Location

Defined in:  
`lib/constants/constants.dart`

Make sure it's properly referenced via:

```dart
part 'http_status_code.dart';
```
