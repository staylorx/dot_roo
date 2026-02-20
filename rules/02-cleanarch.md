# Clean Architecture

When it doubt always assume a clean architectural style, i.e., domain, data, and presentation layers at a minimum.

Map your components to Clean Architecture's four layers using separate packages/modules/projects (e.g., Domain, Application, Infrastructure, Presentation), ordered inward for dependencies: Presentation → Application → Domain ← Infrastructure (arrows show allowed flows). Top-level folders scream business domain (e.g., src/Ordering or src/Cart), with layers nested below; each layer is a distinct project to enforce rules via compiler.

Exact Layer Mapping & Dependencies
Your items fit precisely:

Layer (Package/Project) Your Components Dependencies
Domain (innermost) entities, value_objects None (pure)
​
Application usecases, repository_contracts (interfaces) → Domain only
​
Infrastructure (outer) repository_implementation, low-level API/database stuff (DbContext, EF configs, external libs) → Application + Domain
​
Presentation (outermost) app/facade (controllers, UI, entry points) → Application
​
Recommended Folder Layout
Use one project per layer for strict enforcement; inside, group by feature/use case:

text
Solution/
├── src/
│ ├── Domain/ # Entities, ValueObjects
│ │ ├── Entities/
│ │ └── ValueObjects/
│ ├── Application/ # UseCases, Contracts
│ │ ├── UseCases/ # Or Features/Ordering/Commands
│ │ │ └── Ordering/
│ │ └── Contracts/ # IRepository, etc.
│ ├── Infrastructure/ # Impls + low-level
│ │ ├── Persistence/ # Repos impls, DbContext
│ │ └── External/ # APIs, services
│ └── Presentation.Web/ # Or .Api, .App (Facade)
│ ├── Controllers/ # Or Pages/
│ └── Facades/ # App entry
└── tests/ # Unit per layer
Dependency Rule: Use DI to inject; Application references Domain project only, Infrastructure references Application+Domain, Presentation references Application. No reverse refs.
