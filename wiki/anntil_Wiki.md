# SigmaOS-anntil Component Wiki

## Overview
SigmaOS-anntil provides annulment and cancellation support for the SigmaOS operating system. It demonstrates the cancellation subsystem and task cancellation within the SigmaOS ecosystem, following the principles of clear abstraction and deterministic annulment initialization.

## Principles
- Single Responsibility
- Cancellation Abstraction
- Fail-Fast on Cancellation Initialization Errors
- Deterministic Cancellation Setup
- Clear Abstraction Over Cancellation APIs
- Composition over Inheritance for cancellation extensions

## Architecture
SigmaOS-anntil follows a cancellation pattern:
- **Cancellation Core**: Provides task cancellation, operation cancellation, and cancellation tracking
- **Task Cancellation**: Supports task cancellation, operation cancellation, and cancellation propagation
- **Cancellation Tracking**: Supports cancellation status, cancellation tracking, and cancellation lifecycle
- **Error Handling**: Fail-fast on invalid cancellation configurations or unsupported cancellation types

## API
The component provides the following public APIs:
- `cancel::task(task)` - Cancel a task by given task ID
- `cancel::operation(operation)` - Cancel an operation by given operation ID
- `cancel::status::cancellations()` - Get cancellation status and active cancellations
- `cancel::lifecycle::manage(cancellation)` - Manage cancellation lifecycle and cancellation tracking
- Error types for cancellation failure scenarios or unsupported cancellation types

## Test Structure (Arrange-Act-ASSERT)
All tests follow the AAA pattern:
1. **Arrange**: Set up test environment with specific cancellation configuration
2. **Act**: Execute the code under test (task cancellation, operation cancellation)
3. **Assert**: Verify the expected cancellation results

Example:
```rust
#[test]
fn test_cancel_task_aaa() {
    // Arrange
    let task_id = "task-1";
    
    // Act
    let result = cancel::task(task_id);
    
    // Assert
    assert!(result.is_ok());
    let cancelled = result.unwrap();
    assert!(cancelled.is_cancelled());
}
```

## Development
- Follows Rust best practices with `#![forbid(unsafe_code)]`
- Cancellation initialization is best-effort; gracefully degrades on unsupported configurations
- Comprehensive error types for all cancellation failure scenarios
- Unit tests provided for task cancellation and operation cancellation
- Integration tests for full cancellation system with actual cancellation integration

## TODO
- Add support for additional cancellation types (signal cancellation, timeout cancellation, error cancellation)
- Expand task capabilities (task priorities, task dependencies, task cancellation groups)
- Add lifecycle features (cancellation tracking, cancellation lifecycle, cancellation propagation)
- Create integration tests with actual cancellation systems and cancellation integration
- Implement cancellation persistence and cancellation state management