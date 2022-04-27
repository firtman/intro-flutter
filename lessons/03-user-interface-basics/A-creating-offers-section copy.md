## Assets

We are going to use several images from the assets.zip file you downloaded from assets. Create an `images` subfolder in your project and copy all the files within assets.

## OfferPage

Create the OffersPage as a new Dart file, and create a Stateless Widget. 

In the same file, create the Offer Stateless widget with the following code:


```dart
class Offer extends StatelessWidget {
  final String title;
  final String description;

  const Offer({Key? key, required this.title, required this.description})
      : super(key: key);

  @override
  Widget build(BuildContext context) {
    return SizedBox(
      width: 320,
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Card(
          elevation: 2,
          color: Colors.amber.shade50,
          child: Padding(
            padding: const EdgeInsets.all(8.0),
            child: Container(
              decoration: const BoxDecoration(
                image: DecorationImage(
                  image: AssetImage("images/background.png"),
                  fit: BoxFit.cover,
                ),
              ),
              child: Padding(
                padding: const EdgeInsets.only(top: 20, bottom: 20),
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.stretch,
                  children: [
                    Center(
                        child: Container(
                      color: Colors.amber.shade50,
                      child: Padding(
                        padding: const EdgeInsets.all(8.0),
                        child: Text(title,
                            style: Theme.of(context).textTheme.headline5),
                      ),
                    )),
                    Center(
                        child: Padding(
                      padding: const EdgeInsets.only(top: 8.0),
                      child: Container(
                        color: Colors.amber.shade50,
                        child: Padding(
                          padding: const EdgeInsets.all(8.0),
                          child: Text(description,
                              style: Theme.of(context).textTheme.bodyLarge),
                        ),
                      ),
                    ))
                  ],
                ),
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

Now use this widget rendering it in OffersPage; then remove the default template code (the counter and the FloatingActionButton) and render `OffersPage` from within App or HomePage.

Now, let's render some Offers:

```dart
class OffersPage extends StatelessWidget {
  const OffersPage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return SizedBox(
      width: double.infinity,
      child: Column(children: const [
        Offer(
            title: "Early Coffee",
            description: "10% off. Offer valid from 6am to 9am."),
        Offer(title: "Welcome Gift", description: "25% off on your first order")
      ]),
    );
  }
}
```