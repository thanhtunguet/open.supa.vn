---
title: What is a bloc
sidebar_position: 1
---

# What is a bloc

Bloc (Business Logic Component) is a design pattern that helps separate the presentation layer from the business logic in Flutter applications. This pattern was created by Google developer Felix Angelov and has become one of the most popular state management solutions in the Flutter ecosystem.

## Core Concepts

The Bloc pattern is built on three main pillars:

1. **Events**: Input that trigger changes in state. Events are dispatched by the UI or other parts of the application.

2. **States**: The output that represents parts of your application's state. UI components react to state changes.

3. **Bloc**: The component that converts events into states. It takes incoming events, processes them with business logic, and outputs new states.

## Benefits of the Bloc Pattern

- **Separation of Concerns**: Clearly separates UI from business logic
- **Testability**: Business logic can be tested independently of the UI
- **Reusability**: The same bloc can be used across different UI components
- **Predictability**: State transitions are explicit and traceable

## When to Use Bloc

Bloc is particularly useful for:
- Medium to large applications with complex state management needs
- Applications requiring high testability
- Projects with multiple developers working simultaneously
- Features that need to maintain state across screen navigations

<!-- Add content here -->
