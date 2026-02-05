---
description: "Clean Architecture Review"
argument-hint: <file or directory to review>
---

Code review for strict adherence to clean architecture principles.

# Clean Architecture Knowledge Base

This document describes the comprehensive knowledge base that powers the Clean Architecture MCP server. The knowledge base is designed to be language-agnostic, focusing on first principles that apply across all programming paradigms.

## Knowledge Base Organization

The knowledge base is organized into five main categories:

1. **Principles**: Core Clean Architecture principles
2. **Rules**: Specific, checkable rules derived from principles
3. **Violations**: Common violation patterns with explanations
4. **Patterns**: Good architectural patterns and examples
5. **Prompts**: Templates for AI-assisted reviews

## 1. Principles

### Core Principles Covered

#### The Dependency Rule

**URI**: `ca://principles/dependency-rule`

The fundamental rule of Clean Architecture: source code dependencies must point only inward, toward higher-level policies.

**Key Concepts**:

- Dependencies flow inward only
- Inner layers are unaware of outer layers
- Outer layers depend on inner abstractions
- Use dependency inversion at boundaries

**Why It Matters**:

- Business logic remains independent of frameworks
- System becomes testable without external dependencies
- Flexibility to change implementations without affecting core
- Clear separation of concerns

#### Layering

**URI**: `ca://principles/layering`

Clean Architecture organizes code into concentric layers with specific responsibilities.

**The Four Layers**:

1. **Entities (Core)**
   - Pure business objects and rules
   - Framework-agnostic
   - Most stable, least likely to change
   - No dependencies on outer layers

2. **Use Cases (Application Business Rules)**
   - Application-specific logic
   - Orchestrates entities
   - Defines interfaces for data access
   - No knowledge of frameworks or UI

3. **Adapters (Interface Adapters)**
   - Converts data between use cases and external systems
   - Controllers, presenters, gateways
   - Implements interfaces defined by use cases
   - Knows about both inner and outer layers

4. **Frameworks (Frameworks & Drivers)**
   - UI, database, web frameworks
   - External tools and libraries
   - Most volatile, most likely to change
   - Depends on everything inward

**Layer Responsibilities**:

- Each layer has a single, well-defined purpose
- Layers communicate through interfaces
- Data crosses boundaries in appropriate forms
- No layer skipping (must go through adjacent layers)

#### SOLID Principles

**URI**: `ca://principles/solid`

SOLID principles are fundamental to Clean Architecture implementation.

**Single Responsibility Principle (SRP)**:

- A class should have one reason to change
- Each class serves a single purpose
- Separates concerns effectively

**Open-Closed Principle (OCP)**:

- Open for extension, closed for modification
- Extend behavior through interfaces and inheritance
- Don't modify existing code to add features

**Liskov Substitution Principle (LSP)**:

- Subtypes must be substitutable for base types
- Derived classes must honor base class contracts
- Ensures polymorphism works correctly

**Interface Segregation Principle (ISP)**:

- Many specific interfaces better than one general interface
- Clients shouldn't depend on methods they don't use
- Creates focused, role-specific interfaces

**Dependency Inversion Principle (DIP)**:

- Depend on abstractions, not concretions
- High-level modules don't depend on low-level modules
- Both depend on abstractions
- Critical for implementing the Dependency Rule

#### Package Principles

**URI**: `ca://principles/packages`

Principles for organizing code into packages/modules.

**Acyclic Dependencies Principle (ADP)**:

- No cycles in package dependency graph
- Break cycles with interfaces or new packages
- Enables independent development and testing

**Stable Dependencies Principle (SDP)**:

- Depend in direction of stability
- Volatile packages depend on stable packages
- Stable packages are harder to change

**Stable Abstractions Principle (SAP)**:

- Stable packages should be abstract
- Unstable packages should be concrete
- Stability correlates with abstraction level

## 2. Rules

Rules are specific, checkable criteria derived from principles.

### Layering Rules

#### Rule: No Outward Dependencies

**ID**: `no-outward-dependencies`
**Severity**: Critical

**Description**: Code in inner layers must never import or depend on code from outer layers.

**Check Criteria**:

- Entities don't import use cases, adapters, or frameworks
- Use cases don't import adapters or frameworks
- Adapters don't import frameworks (except as needed for implementation)

**Violation Examples**:

**Correct Example**:

#### Rule: Entities Must Be Framework-Agnostic

**ID**: `entities-framework-agnostic`
**Severity**: Critical

**Description**: Domain entities must contain only business logic, no framework dependencies.

**Check Criteria**:

- No framework imports
- No database annotations
- No serialization concerns
- No UI dependencies

**Common Violations**:

- `@Entity`, `@Table`, `@Column` annotations
- `@JsonSerializable` decorators
- Database ID fields (unless business requirement)
- HTTP/REST concerns

#### Rule: Use Cases Define Interfaces

**ID**: `use-cases-define-interfaces`
**Severity**: Major

**Description**: Use cases should define repository and gateway interfaces, not depend on concrete implementations.

**Check Criteria**:

- Repository interfaces in domain/use case layer
- Concrete implementations in infrastructure layer
- Use cases depend on abstractions only
- Dependency injection used

**Pattern**:

### Dependency Rules

#### Rule: Dependency Inversion at Boundaries

**ID**: `dependency-inversion-boundaries`
**Severity**: Major

**Description**: At layer boundaries, use dependency inversion to maintain inward-pointing dependencies.

**Check Criteria**:

- Interfaces defined in inner layer
- Implementations in outer layer
- Outer layer depends on inner interfaces
- No concrete class references crossing boundaries

#### Rule: No Business Logic in Outer Layers

**ID**: `no-business-logic-outer`
**Severity**: Major

**Description**: Business rules belong in entities and use cases, not in adapters or frameworks.

**Violations**:

- Business calculations in controllers
- Validation logic in UI
- Business rules in database queries
- Domain logic in API handlers

### SOLID Rules

#### Rule: Single Responsibility Per Class

**ID**: `single-responsibility`
**Severity**: Minor

**Description**: Each class should have one reason to change.

**Indicators of Violation**:

- Class name contains "And" or "Manager"
- Multiple unrelated methods
- Many dependencies
- Large class (>300 lines often indicates multiple responsibilities)

#### Rule: Depend on Abstractions

**ID**: `depend-on-abstractions`
**Severity**: Major

**Description**: Classes should depend on interfaces/abstract classes, not concrete implementations.

**Check Criteria**:

- Constructor parameters are interfaces
- No `new` keyword for dependencies (use factories/DI)
- Concrete classes only in composition root

## 3. Violation Patterns

Common violations with detailed explanations and fixes.

### Entity-Framework Coupling

#### Violation: Entity with Database ID

**Pattern**: Entity contains `id`, `ID`, or `_id` field

**Why It's Wrong**:
Database IDs are infrastructure concerns. Unless the ID is a business concept (like a product SKU), it couples the domain to persistence implementation.

**Fix**:
Use domain handles instead:

**Repository Mapping**:

#### Violation: Entity with Serialization Annotations

**Pattern**: `@JsonSerializable`, `@JsonKey`, etc. in entity

**Why It's Wrong**:
Serialization is an infrastructure concern. Entities should be pure business objects.

**Fix**:
Create DTOs in infrastructure layer:

### Outward Dependencies

#### Violation: Use Case Depends on Framework

**Pattern**: Use case imports HTTP, database, or UI framework

**Why It's Wrong**:
Use cases should be framework-agnostic, testable without external dependencies.

**Fix**:
Define interfaces in use case layer, implement in infrastructure:

#### Violation: Business Logic in Controller

**Pattern**: Calculations, validations, or rules in presentation layer

**Why It's Wrong**:
Business logic should be in domain/use case layers for reusability and testability.

**Fix**:
Move logic to use case:

### Missing Abstractions

#### Violation: Concrete Class Crossing Boundary

**Pattern**: Use case depends on concrete repository class

**Why It's Wrong**:
Violates dependency inversion, makes testing difficult, couples layers.

**Fix**:
Always use interfaces at boundaries:

## 4. Good Patterns

### Dependency Inversion Pattern

**Use Case**: Accessing external data from use case

**Pattern**:

### Use Case Structure Pattern

**Standard Use Case Template**:

### Repository Pattern

**Complete Repository Example**:

### Adapter Pattern

**Converting Between Layers**:

## 5. Prompts

### Code Review Prompt Template

**Purpose**: Guide AI through comprehensive CA code review

**Template**:

```
You are conducting a Clean Architecture code review. Analyze the following code for adherence to Clean Architecture principles.

CODE:
{code}

CONTEXT:
{context}

FOCUS AREAS:
{focus_areas}

Review the code for:

1. LAYERING
   - Is the code in the correct layer?
   - Does it have appropriate responsibilities for its layer?
   - Are layer boundaries respected?

2. DEPENDENCIES
   - Do dependencies point inward only?
   - Are there any outward dependencies?
   - Is dependency inversion used at boundaries?

3. SOLID PRINCIPLES
   - Single Responsibility: Does each class have one reason to change?
   - Open-Closed: Is the code open for extension, closed for modification?
   - Liskov Substitution: Are subtypes properly substitutable?
   - Interface Segregation: Are interfaces focused and role-specific?
   - Dependency Inversion: Does code depend on abstractions?

4. FRAMEWORK INDEPENDENCE
   - Are entities framework-agnostic?
   - Is business logic independent of frameworks?
   - Can the core be tested without external dependencies?

5. TESTABILITY
   - Can this code be unit tested easily?
   - Are dependencies mockable?
   - Is the code loosely coupled?

For each violation found:
- Identify the specific principle violated
- Explain why it's a problem
- Provide a concrete refactoring suggestion
- Show example code if helpful

For good practices found:
- Highlight what's done well
- Explain why it follows CA principles

Provide an overall assessment and prioritized recommendations.
```

### Architecture Review Prompt Template

**Purpose**: Review system architecture design

**Template**:

```
You are reviewing a system architecture design for Clean Architecture compliance.

ARCHITECTURE DESCRIPTION:
{architecture_description}

COMPONENTS:
{components}

Evaluate the architecture for:

1. LAYER ORGANIZATION
   - Are the four layers clearly defined?
   - Entities (Core Business Rules)
   - Use Cases (Application Business Rules)
   - Adapters (Interface Adapters)
   - Frameworks (Frameworks & Drivers)

2. DEPENDENCY FLOW
   - Do all dependencies point inward?
   - Are there any dependency cycles?
   - Is dependency inversion used at boundaries?

3. BOUNDARIES
   - Are layer boundaries well-defined?
   - How does data cross boundaries?
   - Are appropriate abstractions used?

4. STABILITY
   - Are stable components abstract?
   - Do volatile components depend on stable ones?
   - Is the core protected from change?

5. TESTABILITY
   - Can the core be tested independently?
   - Are external dependencies mockable?
   - Is the architecture test-friendly?

Provide:
- Architectural strengths
- Violations or concerns
- Refactoring recommendations
- Risk assessment
```

### Refactoring Guide Prompt Template

**Purpose**: Guide step-by-step refactoring to CA compliance

**Template**:

```
You are advising a refactoring to improve Clean Architecture compliance if one is required.

CURRENT CODE:
{current_code}

VIOLATION TYPE:
{violation_type}

GOAL:
{goal}

Provide a step-by-step refactoring guide:

1. IDENTIFY THE PROBLEM
   - What CA principle is violated?
   - Why is this a problem?
   - What are the consequences?

2. PLAN THE REFACTORING
   - What needs to change?
   - What new abstractions are needed?
   - What's the migration path?

3. STEP-BY-STEP REFACTORING
   For each step:
   - Describe what to do
   - Show the code changes
   - Explain why this step helps
   - Ensure tests still pass

4. VERIFY THE RESULT
   - Confirm CA compliance
   - Check that tests pass
   - Verify no regressions
   - Assess improvements

5. ADDITIONAL IMPROVEMENTS
   - What else could be improved?
   - Are there related issues?
   - What's the next priority?
```
