---
title: LoginForm
sidebar_position: 1
---

# LoginForm

`LoginForm` is a custom form class that encapsulates user login data using the [reactive_forms](https://pub.dev/packages/reactive_forms) package. It provides typed access to the `username` and `password` fields with built-in validation logic.

---

## 📌 Purpose

The `LoginForm` class is designed to streamline user authentication by:

- Providing a reusable and type-safe structure for login forms.
- Encapsulating validation logic directly within the form group.
- Enabling reactive UI updates based on form state.

---

## 🚀 Usage

### ✅ Creating the form

```dart
final form = LoginForm('', '');
```

You can provide initial values for both fields:

```dart
final form = LoginForm('user@example.com', '');
```

### 🧩 Accessing form controls

```dart
form.username.value; // current username
form.password.value; // current password

form.username.valid; // validation state
form.password.errors; // validation errors if any
```

### 🔄 Listening to changes

```dart
form.username.valueChanges.listen((value) {
  print('Username updated: $value');
});
```

---

## 🧠 Validators

Both `username` and `password` are marked as **required**:

```dart
Validators.required
```

You can extend this class with more validators if needed (e.g., email format, password strength).

---

## 🛠 Best Practices

- Prefer using this form class over manually constructing a `FormGroup` in UI layers.
- Bind the form directly to UI widgets using `ReactiveForm` and `ReactiveTextField` for optimal reactivity.
- Centralize business logic in a bloc or controller, keeping the UI clean and declarative.

---

## 📎 Example with UI

```dart
ReactiveForm(
  formGroup: LoginForm('', ''),
  child: Column(
    children: [
      ReactiveTextField<String>(
        formControlName: 'username',
        decoration: InputDecoration(labelText: 'Username'),
      ),
      ReactiveTextField<String>(
        formControlName: 'password',
        obscureText: true,
        decoration: InputDecoration(labelText: 'Password'),
      ),
    ],
  ),
)
```

---

## 🧱 Extension Ideas

- Add `Validators.email` to the `username` field if used as email.
- Add a `rememberMe` checkbox as a `FormControl<bool>`.
- Add password visibility toggle via UI logic.

---

## 📂 Location

This class is defined in:  
`lib/forms/login_form.dart` (recommended convention)
