# enhanced-http

[![Pub](https://img.shields.io/pub/v/enhanced_http.svg)](https://pub.dartlang.org/packages/enhanced_http)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/andresaraujo/enhanced_http/master/LICENSE)

## IMPORTANT !!!
## This project has been migrated to the following [monorepo](https://github.com/sliit-foss/dart-cookbook) and will no longer be maintained here.

A wrapper around the dart http package provided by Google (https://pub.dev/packages/http) which is inspired by axios

## Getting started

Create an instance of enhanced http as follows :

```dart
EnhancedHttp http = EnhancedHttp(baseURL: "https://dog.ceo/api");
```

Custom headers can be provided through the name parameter 'headers' ( Default content type is specified as application/json ) :

```dart
EnhancedHttp http = EnhancedHttp(
  baseURL: "https://dog.ceo/api",
  headers: {'Authorization': "Bearer $token"}
);
```

Provide optional interceptors as follows :

```dart
EnhancedHttp http = EnhancedHttp(
    baseURL: "https://dog.ceo/api",
    interceptors: InterceptorOptions(
      response: (dynamic res) {
        print("Status ${res["status"]}");
        print("Headers ${res["headers"]}");
        print("Data ${res["data"]}");
        return res["data"];
      },
      error: (dynamic e) {
        print(e);
        return "An error has occurred please try again later";
      }
    )
);
```

## Usage

Fetch data from an api endpoint - GET

```dart
final res = await http.get("/path");
```

Send data to an api endpoint - POST

```dart
final res = await http.post("/path", payload: {
    "data": "This is some sample data to send to a server"
});
```

Update data at an api endpoint - PUT

```dart
final res = await http.put("/path", payload: {
    "data": "This is some sample data to update at a server"
});
```

Partially update data at an api endpoint - PATCH

```dart
final res = await http.put("/path", payload: {
    "data": "This is some sample data to update at a server"
});
```

Delete data at an api endpoint - DELETE

```dart
final res = await http.delete("/path");
```

Request headers at an api endpoint - HEAD

```dart
final res = await http.head("/path");
```

## Additional Parameters

The files attribute on the http post, http put and http patch methods can be used to send files to the server

```dart
final res = await http.post("/path",
    payload: {
        "data": "This is some sample data to update at a server"
    },
    headers: {
      "Content-Type": "multipart/form-data"
    },
    files: [
        {
            "array_key": "file",
            "file": File("path_to_file")
        }
    ],
);
```

## Access to the underlying http package

The underlying http package can be accessed as follows bypassing the transitive dependency import warning:

```dart
import 'package:enhanced_http/enhanced_http.dart' as http;

final res = await http.get("/path");
```
