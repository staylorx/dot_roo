# Clean Architecture

When it doubt always assume a clean architectural style, i.e., domain, data, and presentation layers at a minimum.
Domain and data layers should be in a seperate package folder to ensure crisp separation.
Usecases must always use dependency injection.
No riverpod, getit, or any other state or DI mechanisms in the domain and data layers.
