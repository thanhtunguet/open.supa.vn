---
title: FileService
sidebar_position: 2
---

# FileService

`FileService` is a utility class that provides **common file operations** and **metadata extraction** used throughout the Supa Flutter application. It encapsulates logic for detecting file types, generating viewer URLs, launching external links, and resolving appropriate icons for various file extensions.

---

## 📦 Features

- File type detection (Office, PDF, Image, etc.)
- Viewer URL generation for Microsoft Office and Google Docs
- Launch external file URLs in browser
- Icon mapping for file extensions using Carbon Icons
- Supported file type validation

---

## 🧠 Use Cases

- Detecting file type from filename or extension.
- Displaying appropriate icon in the UI.
- Opening files in web viewers like Office Online or Google Docs.
- Validating whether a file can be processed.

---

## 🚀 File Type Detection

### Example:

```dart
FileService.isPDFFile("invoice.pdf"); // true
FileService.isImageFile("profile.jpg"); // true
FileService.isOfficeFile("report.docx"); // true
```

### Available Detectors

| Method                      | File Types                      |
|----------------------------|----------------------------------|
| `isOfficeFile`             | `.doc`, `.docx`, `.xls`, `.xlsx`, `.ppt`, `.pptx` |
| `isDocFile`                | `.doc`, `.docx`                 |
| `isSpreadSheetFile`        | `.xls`, `.xlsx`                 |
| `isPresentationFile`       | `.ppt`, `.pptx`                 |
| `isImageFile`              | `.jpg`, `.jpeg`, `.png`         |
| `isPDFFile`                | `.pdf`                          |
| `isSupportedFile`          | All supported file types listed below |

---

## 🌐 Viewer URL Utilities

```dart
final officeUrl = FileService.createOfficeViewerUrl(fileUrl);
final googleUrl = FileService.createGoogleDocsViewerUrl(fileUrl);
```

### Format

- Office Viewer:  
  `https://view.officeapps.live.com/op/view.aspx?src=<encoded_url>`

- Google Docs Viewer:  
  `https://docs.google.com/gview?embedded=true&url=<encoded_url>`

---

## 🖼 Icon Mapping

```dart
final icon = FileService.iconData("document.pdf");
```

### Icon Mapping Table

| Extension Types              | Icon                      |
|-----------------------------|---------------------------|
| `.pdf`                      | `CarbonIcons.pdf`         |
| `.doc`, `.docx`             | `CarbonIcons.doc`         |
| `.ppt`, `.pptx`             | `CarbonIcons.ppt`         |
| `.xls`, `.xlsx`             | `CarbonIcons.xls`         |
| `.zip`                      | `CarbonIcons.zip`         |
| `.txt`                      | `CarbonIcons.txt`         |
| `.jpg`, `.jpeg`, `.png`, `.gif`, `.bmp`, `.webp` | `CarbonIcons.image` |
| Default                     | `Icons.attachment`        |

---

## 🌍 Launching URLs

```dart
await FileService.launchUrl("https://example.com/document.pdf");
```

- Checks URL validity before launching via browser.
- Uses `url_launcher_string` internally.

---

## 🧪 Supported File Types

Validated via `isSupportedFile()`:

```dart
const supportedExtensions = [
  'jpg', 'jpeg', 'png', 'gif', 'bmp', 'webp', // Images
  'doc', 'docx', 'xls', 'xlsx', 'ppt', 'pptx', // Office files
  'pdf', 'zip', 'txt'
];
```

---

## 📂 Location

```txt
lib/services/file_service.dart
```
