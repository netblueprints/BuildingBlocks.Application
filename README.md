# BuildingBlocks.Application

A set of reusable building blocks for implementing the Application layer in .NET solutions, following Clean Architecture and CQRS principles.

## Features

- **Pipeline Behaviours**: Common MediatR pipeline behaviors such as validation and unhandled exception handling.
- **Custom Exceptions**: Application-specific exceptions like `ValidationException` and `ForbiddenAccessException`.
- **Mapping Extensions**: Utilities for mapping between domain and application models.
- **Result & Pagination Models**: Standardized result and paginated list models for consistent API responses.
- **Security**: Attributes and helpers for authorization in the application layer.

## Usage Example

### Using Pipeline Behaviours with MediatR

```csharp
services.AddMediatR(cfg => {
    cfg.AddBehavior(typeof(IPipelineBehavior<,>), typeof(ValidationBehaviour<,>));
    cfg.AddBehavior(typeof(IPipelineBehavior<,>), typeof(UnhandledExceptionBehaviour<,>));
});
```

### Returning a Paginated List

```csharp
var paginatedList = await PaginatedList<T>.CreateAsync(query, pageIndex, pageSize);
return Result<PaginatedList<T>>.Success(paginatedList);
```

### Throwing a Custom Exception

```csharp
if (!user.HasAccess)
    throw new ForbiddenAccessException();
```

## Testing

Unit tests are provided in the NetBlueprints.BuildingBlocks.Application.tests project, demonstrating usage and best practices for the application layer components.

## Getting Started

1. Reference the `NetBlueprints.BuildingBlocks.Application` project in your solution.
2. Register the provided pipeline behaviors and use the models and exceptions in your application services and handlers.
3. Refer to the test project for practical examples.

## License

This project is licensed under the MIT License. See the LICENSE file for details.