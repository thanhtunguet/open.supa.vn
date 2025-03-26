---
title: DateTimeFormatsVN
sidebar_position: 1
---

# DateTimeFormatsVN

The `DateTimeFormatsVN` class defines a set of standardized date and time formats tailored for the **Vietnamese locale** (`vi_VN`). These constants are designed to work seamlessly with the [`intl`](https://pub.dev/packages/intl) package and ensure consistent formatting across your app.

---

## 🧠 Why use this?

- Enforces **locale-specific** formatting.
- Centralizes all date/time format strings in one place.
- Improves consistency, reusability, and maintainability.

---

## 📦 Usage

```dart
import 'package:intl/intl.dart';

final formatted = DateFormat(DateTimeFormatsVN.dateOnly, 'vi_VN').format(DateTime.now());
print(formatted); // e.g., 26/03/2025
```

---

## 📋 Available Formats

| Constant                     | Format String             | Example                          |
|-----------------------------|---------------------------|----------------------------------|
| `dateTime`                  | `dd/MM/yyyy HH:mm:ss`     | `01/01/2024 14:30:45`            |
| `dateTimeWithoutSeconds`    | `dd/MM/yyyy HH:mm`        | `01/01/2024 14:30`               |
| `dateOnly`                  | `dd/MM/yyyy`              | `01/01/2024`                     |
| `timeOnly`                  | `HH:mm:ss`                | `14:30:45`                       |
| `timeOnlyWithoutSeconds`    | `HH:mm`                   | `14:30`                          |
| `dateWithDayAndMonthOnly`   | `dd/MM`                   | `01/01`                          |
| `yearOnly`                  | `yyyy`                    | `2024`                           |
| `dateWithDayName`           | `EEEE, dd/MM/yyyy`        | `Thứ Hai, 01/01/2024`            |
| `dateWithMonthName`         | `dd MMMM yyyy`            | `01 Tháng Một 2024`              |
| `shortDateWithMonthName`    | `dd MMM`                  | `01 Tháng Một`                   |

---

## ✅ Best Practices

- Use these constants throughout your app to avoid hardcoding format strings.
- Always pass `"vi_VN"` explicitly to the `DateFormat` constructor to ensure proper localization.
- Use `DateFormat(...).format(...)` instead of `.toString()` for user-facing strings.

---

## 📂 Location

This class is defined in:  
`lib/constants/constants.dart`

It is marked with `part of "constants.dart";`, so ensure your `constants.dart` file includes:

```dart
part 'date_time_formats_vn.dart';
```
