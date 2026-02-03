# Testing

## Overview

- Big fan of the `shouldy` package. Use it as much as you can.
- Setup test groups with "Given" in the name, then a group with "When" in the name, and finally tests with "Then" in the names. Emulate BDD with names as much as reasonably possible.

## BDD-Style Test Structure Template

### Pattern 1: Entity/Value Object Tests

```dart
void main() {
  group('Given a ClassName', () {
    // Setup common test data at this level

    group('When constructing with valid parameters', () {
      test('Then it creates instance with all required fields', () {
        // Arrange
        // Act
        // Should
      });

      test('Then it creates instance with optional fields', () {
        // Arrange
        // Act
        // Should
      });
    });

    group('When comparing instances', () {
      test('Then two instances with same values are equal', () {
        // Arrange
        // Act
        // Should
      });

      test('Then instances with different values are not equal', () {
        // Arrange
        // Act
        // Should
      });
    });

    group('When copying with modifications', () {
      test('Then copyWith with no changes returns equivalent instance', () {
        // Arrange
        // Act
        // Should
      });

      test('Then copyWith modifies only specified fields', () {
        // Arrange
        // Act
        // Should
      });
    });

    group('When serializing to JSON', () {
      test('Then toJson returns correct map structure', () {
        // Arrange
        // Act
        // Should
      });

      test('Then fromJson creates correct instance', () {
        // Arrange
        // Act
        // Should
      });

      test('Then round trip serialization preserves all data', () {
        // Arrange
        // Act
        // Should
      });
    });
  });
}
```

### Pattern 2: Use Case Tests

```dart
void main() {
  group('Given a UseCaseName', () {
    late UseCase useCase;
    late MockRepository mockRepository;

    setUp(() {
      mockRepository = MockRepository();
      useCase = UseCase(repository: mockRepository);
    });

    group('When executing with valid input', () {
      test('Then it returns success with expected data', () {
        // Arrange
        // Act
        // Should
      });

      test('Then it calls repository exactly once', () {
        // Arrange
        // Act
        // Should
      });
    });

    group('When repository returns failure', () {
      test('Then it propagates the failure', () {
        // Arrange
        // Act
        // Should
      });
    });

    group('When handling edge cases', () {
      test('Then it handles empty results correctly', () {
        // Arrange
        // Act
        // Should
      });
    });
  });
}
```

### Pattern 3: Repository Tests

```dart
void main() {
  group('Given a RepositoryName', () {
    late Repository repository;
    late MockDataSource mockDataSource;

    setUp(() {
      mockDataSource = MockDataSource();
      repository = Repository(dataSource: mockDataSource);
    });

    group('When fetching entities', () {
      group('When data source returns success', () {
        test('Then it returns the entities', () {
          // Arrange
          // Act
          // Should
        });

        test('Then it caches the results', () {
          // Arrange
          // Act
          // Should
        });
      });

      group('When data source returns failure', () {
        test('Then it propagates the failure', () {
          // Arrange
          // Act
          // Should
        });
      });
    });

    group('When fetching by ID', () {
      group('When entity exists', () {
        test('Then it returns the entity', () {
          // Arrange
          // Act
          // Should
        });
      });

      group('When entity does not exist', () {
        test('Then it returns not found failure', () {
          // Arrange
          // Act
          // Should
        });
      });
    });
  });
}
```

### Pattern 4: Integration Tests

```dart
void main() {
  group('Given an integrated system', () {
    late SystemComponent component;

    setUp(() async {
      // Setup integration test environment
    });

    tearDown(() async {
      // Cleanup
    });

    group('When performing end-to-end operation', () {
      test('Then it completes successfully', () async {
        // Arrange
        // Act
        // Should
      });

      test('Then it produces expected side effects', () async {
        // Arrange
        // Act
        // Should
      });
    });
  });
}
```
