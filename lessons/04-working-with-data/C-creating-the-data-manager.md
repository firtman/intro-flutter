We will create a set of classes responsible for managing the data of our app, a DataManager class in a new file `DataManager.dart`. It will include two repositories in lists and then some functions for the cart management.


```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
import 'datamodel.dart';

class DataManager {
  List<Category>? _menu;
  List<ItemInCart> cart = [];

  cartAdd(Product p) {
    bool found = false;
    for (var item in cart) {
      if (item.product.id == p.id) {
        item.quantity++;
        found = true;
      }
    }
    if (!found) {
      cart.add(ItemInCart(product: p, quantity: 1));
    }
  }

  cartDelete(Product p) {
    cart.removeWhere((element) => element.product.id == p.id);
  }

  cartClear() {
    cart.clear();
  }

  double cartTotal() {
    var sum = 0.0;
    for (var item in cart) {
      sum += item.quantity * item.product.price;
    }
    return sum;
  }
}

```

# Using the Data Manager

We will create an instance of the DataManager at the App level in `HomePage` and pass it to final properties to the `MenuPage` and `OrderPage` that will need it.

Your HomePage widget will start with:

```dart
class _MyHomePageState extends State<MyHomePage> {
  int _currentIndex = 0;
  DataManager dataManager = DataManager();

  @override
  Widget build(BuildContext context) {
    late Widget currentPage;
    switch (_currentIndex) {
      case 0:
        currentPage = MenuPage(dataManager: dataManager);
        break;
      case 1:
        currentPage = const OffersPage();
        break;
      case 2:
        currentPage = OrderPage(dataManager: dataManager);
        break;
    }
    // continues ....
```

At `MenuPage` and `OrderPage` we will add the final variables and also receive it as a required named argument in the constructor:

```dart
class MenuPage extends StatelessWidget {
  final DataManager dataManager;

  const MenuPage({Key? key, required this.dataManager}) : super(key: key);
    // continues ....
```

Now MenuPage is ready to use the data.