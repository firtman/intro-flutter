It's time to start working with data. Let's create a Model file called DataModel.dart with the following basic  classes

###DataModel

```dart
class Product {
  int id;
  String name;
  double price;
  String image;

  String get imageUrl =>
      "https://firtman.github.io/coffeemasters/api/images/$image";

  Product(
      {required this.id,
      required this.name,
      required this.price,
      required this.image});
}

class Category {
  String name;
  List<Product> products;

  Category({required this.name, required this.products});
}

class ItemInCart {
  Product product;
  int quantity;

  ItemInCart({required this.product, required this.quantity});
}

```
