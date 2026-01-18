# riverpod

## FutureProvider

Stick to FutureProvider mostly for:

- Data fetching (your repos/usecases return Future)
- Handles loading/error states automatically
- Built-in caching/refresh

## Provider

Use Provider only for:

- Pure computation from other providers
- Factory objects (usecases, repositories)
- Static config values
