# Clean Architecture

When it doubt always assume a clean architectural style, i.e., domain, data, and presentation layers at a minimum.
Domain and data layers should be in a seperate package folder to ensure crisp separation.
Usecases must always use dependency injection.
No riverpod, getit, or any other state or DI mechanisms in the domain and data layers.

With dart, use melos as much as possible to monorepo a very strict chain of depdenencies:

## Domain layer

- entities (depends on nothing)

- contracts → entities (repository interfaces optionally datasource interfaces)

- use_cases → contracts, entities

## Data Layer Adapter Implentations

If our repo impls have adapter-specific language then we may need an adapter of adapters, that kind of thing. Watch out for this layer specifically, it's the pivot of the whole strategy and can get muddy fast.

- repo_impls (or similar) → contracts, entities, and the datasource packages (or just datasource interfaces if you keep it stricter)

## Data Layer Adapters

Four are given here as examples, keeping in mind that `(hive -or- sembast) -and- api --and-- yaml` is wired up later in the application or presentation layer (getit, riverpod, bloc, manually, etc.).

- datasource_hive → contracts/entities + Hive libs

- datasource_sembast → contracts/entities + Sembast libs

- datasource_duo_api → contracts/entities + HTTP/auth libs

0 adapter_yaml_io → entities (and/or contracts) + YAML libs
