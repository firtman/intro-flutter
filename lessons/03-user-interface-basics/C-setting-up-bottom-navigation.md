## Setting the Theme

Open the file at `main.dart` and let's update the app's name, and also the theme's color. We will use `Colors.brown`. To see all the colors available in Material, check the [Material Color website](https://material.io/resources/color/) or [Material Palette](https://www.materialpalette.com/).

Replace the title in the `Scaffold` widget with 

```dart
AppBar(
    title: Image.asset('images/logo.png'),
    ),
```

## Creating the Bottom Bar

In the HomePage widget, add a `bottomNavigationBar` to the `Scaffold` widget and define the following code:

```dart
BottomNavigationBar(
    backgroundColor: Theme.of(context).primaryColor,
    elevation: 24,
    selectedItemColor: Colors.yellow.shade400,
    unselectedItemColor: Colors.brown.shade50,
    items: const <BottomNavigationBarItem>[
        BottomNavigationBarItem(
            icon: Icon(Icons.coffee),
            label: 'Menu',
        ),
        BottomNavigationBarItem(
            icon: Icon(Icons.local_offer),
            label: 'Offers',
        ),
        BottomNavigationBarItem(
            icon: Icon(Icons.shopping_cart_outlined), 
            label: 'Order'
        ),
    ],
),
```

Now we need to save the state in a state variable at HomePage

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

    return Scaffold(
      appBar: AppBar(
        title: Image.asset('images/logo.png'),
      ),
      bottomNavigationBar: BottomNavigationBar(
        backgroundColor: Theme.of(context).primaryColor,
        elevation: 24,
        selectedItemColor: Colors.yellow.shade400,
        unselectedItemColor: Colors.brown.shade50,
        items: const <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            icon: Icon(Icons.coffee),
            label: 'Menu',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.local_offer),
            label: 'Offers',
          ),
          BottomNavigationBarItem(
              icon: Icon(Icons.shopping_cart_outlined), label: 'Order'),
        ],
        currentIndex: _currentIndex,
        onTap: (index) {
          setState(() {
            _currentIndex = index;
          });
        },
      ),
      body: currentPage,
    );
  }
}

```

Now create a `pages/` folder, move `OffersPage.dart` there and create two empty Widgets in new files for `MenuPage` and `OrderPage`.