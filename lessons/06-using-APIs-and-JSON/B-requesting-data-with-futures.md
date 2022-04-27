Dart doesn't map automatically JSON values into classes, so we have to do it manually. We will add some factory methods in `DataModel.dart` for our Product and Category classes as:

##Data Model to the rescue
```dart

  // Add this in class Product
  factory Product.fromJson(Map<String, dynamic> json) {
    return Product(
        id: json['id'] as int,
        name: json['name'] as String,
        price: json['price'] as double,
        image: json['image'] as String);
  }

  // Add this in class Category
  factory Category.fromJson(Map<String, dynamic> json) {
    var productsJson = json['products'] as Iterable<dynamic>;
    var products = productsJson.map((p) => Product.fromJson(p)).toList();
    return Category(name: json['name'] as String, products: products);
  }

  
```

##Using Futures to get the network response and parse JSON

In DataManager.dart add the following methods

```dart
fetchMenu() async {
    try {
      const url = 'https://firtman.github.io/coffeemasters/api/menu.json';
      var response = await http.get(Uri.parse(url));

      if (response.statusCode == 200) {
        _menu = [];
        var decodedData = jsonDecode(response.body) as List<dynamic>;
        for (var json in decodedData) {
          _menu?.add(Category.fromJson(json));
        }
      } else {
        throw Exception("Error loading data");
      }
    } catch (e) {
      throw Exception("Error loading data");
    }
  }

    Future<List<Category>> getMenu() async {
    if (_menu == null) {
      await fetchMenu();
    }
    return _menu!;
  }
```

