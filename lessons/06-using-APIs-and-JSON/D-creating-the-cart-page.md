Finally, we have to update our `OrderPage` so it can render its content. We will start by creating a simple view for when the cart is empty, then the CartItem that we will repeat for every item, and the `ListView` that will render all its contents.


## OrderItem

```dart
class OrderItem extends StatelessWidget {
  final ItemInCart item;
  final Function onRemove;
  const OrderItem({Key? key, required this.item, required this.onRemove})
      : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Card(
      elevation: 4,
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Row(
          mainAxisAlignment: MainAxisAlignment.start,
          children: [
            Expanded(
                flex: 1,
                child: Padding(
                  padding: const EdgeInsets.only(left: 8.0),
                  child: Text("${item.quantity}x"),
                )),
            Expanded(
                flex: 6,
                child: Text(
                  item.product.name,
                  style: const TextStyle(fontWeight: FontWeight.bold),
                )),
            Expanded(
                flex: 2,
                child: Text("\$" +
                    (item.product.price * item.quantity).toStringAsFixed(2))),
            Expanded(
                flex: 1,
                child: IconButton(
                    color: Theme.of(context).primaryColor,
                    onPressed: () {
                      onRemove(item.product);
                    },
                    icon: const Icon(Icons.delete)))
          ],
        ),
      ),
    );
  }
}
```

## OrderPage

We will need to convert the Stateless widget into a Stateful widget because the list will be updated every time we delete one item

```dart

class OrderPage extends StatefulWidget {
  final DataManager dataManager;
  const OrderPage({Key? key, required this.dataManager}) : super(key: key);

  @override
  State<OrderPage> createState() => _OrderPageState();
}

class _OrderPageState extends State<OrderPage> {
  @override
  Widget build(BuildContext context) {
    if (widget.dataManager.cart.isEmpty) {
      return const Padding(
        padding: EdgeInsets.all(16.0),
        child: Text("Your order is empty"),
      );
    } else {
      return Padding(
        padding: const EdgeInsets.all(8.0),
        child: Column(
          children: [
            ListView.builder(
                shrinkWrap: true,
                physics: const ClampingScrollPhysics(),
                itemCount: widget.dataManager.cart.length,
                itemBuilder: (context, index) {
                  var item = widget.dataManager.cart[index];
                  return OrderItem(
                      item: item,
                      onRemove: (product) {
                        setState(() {
                          widget.dataManager.cartDelete(product);
                        });
                      });
                }),
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: Text(
                  "Total: \$${widget.dataManager.cartTotal().toStringAsFixed(2)}"),
            ),
            Padding(
              padding: const EdgeInsets.only(top: 28.0),
              child: SizedBox(
                width: 200,
                child: ElevatedButton(
                    style: ElevatedButton.styleFrom(
                        primary: Colors.green.shade900),
                    onPressed: () {
                      //TODO:
                    },
                    child: const Text("Send Order")),
              ),
            )
          ],
        ),
      );
    }
  }
}
```

Now we need to finish the Send Order button by adding some behaviour and creating an `AlertDialog` widget to show to the user

```dart
// this code goes in the TODO: in the previous widget
showDialog(
    context: context,
    builder: (context) => const OrderAlert());
setState(() {
    // we update the cart within setState so the current widget will get re-rendered
    widget.dataManager.cartClear();
});
```

The `OrderAlert` widget looks like:

```dart
class OrderAlert extends StatelessWidget {
  const OrderAlert({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return AlertDialog(
      title: const Text("Your Order"),
      content: const Text("Your order is being prepared. Thanks!"),
      actions: [
        TextButton(
            onPressed: () => Navigator.pop(context, 'OK'),
            child: const Text('OK'))
      ],
    );
  }
}
```