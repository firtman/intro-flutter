For responsive design we can use different techniques, such as:

* Flexible elements using different Widgets, including `Expanded` and `SizedBox`
* Use in a `Container` or `SizedBox` a `width` or `height` with the special value `double.infinity`
* Use `Wrap` instead of `Column` or `ListView`
* Use Media Queries to make conditional Widget rendering, using `MediaQuery.of(context)` and saving it in a variable in the `build` method