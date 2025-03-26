---
title: Define and use a BLoC
sidebar_position: 2
---

# Define and use a BLoC

[BLoC (Business Logic Component)](https://pub.dev/packages/flutter_bloc) is a state management pattern for Flutter applications. It helps separate business logic from UI components, making your code more testable and maintainable.

## Basic Concepts

The BLoC pattern involves three main components:

1. **Events** - Input actions that the bloc responds to
2. **States** - Output that represents the UI state
3. **BLoC** - Business logic that converts events to states

## Implementation Steps

### 1. Add Dependencies

```dart
// In your pubspec.yaml
dependencies:
  flutter_bloc: ^8.1.3  # Check for the latest version
```

### 2. Create State Class

```dart
// Define all possible states
abstract class CounterState {}

class CounterInitial extends CounterState {}
class CounterLoaded extends CounterState {
  final int count;
  CounterLoaded(this.count);
}
```

### 3. Create Event Class

```dart
// Define all possible events
abstract class CounterEvent {}

class IncrementEvent extends CounterEvent {}
class DecrementEvent extends CounterEvent {}
```

### 4. Create BLoC Class

```dart
import 'package:flutter_bloc/flutter_bloc.dart';

class CounterBloc extends Bloc<CounterEvent, CounterState> {
  CounterBloc() : super(CounterInitial()) {
    on<IncrementEvent>((event, emit) {
      if (state is CounterInitial) {
        emit(CounterLoaded(1));
      } else if (state is CounterLoaded) {
        final currentState = state as CounterLoaded;
        emit(CounterLoaded(currentState.count + 1));
      }
    });
    
    on<DecrementEvent>((event, emit) {
      if (state is CounterLoaded) {
        final currentState = state as CounterLoaded;
        emit(CounterLoaded(currentState.count - 1));
      }
    });
  }
}
```

### 5. Provide and Consume the BLoC

```dart
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocProvider(
      create: (context) => CounterBloc(),
      child: MaterialApp(
        home: CounterPage(),
      ),
    );
  }
}

class CounterPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Counter Example')),
      body: Center(
        child: BlocBuilder<CounterBloc, CounterState>(
          builder: (context, state) {
            if (state is CounterInitial) {
              return Text('Press the button to start counting');
            } else if (state is CounterLoaded) {
              return Text('Count: ${state.count}');
            }
            return Text('Unknown state');
          },
        ),
      ),
      floatingActionButton: Column(
        mainAxisAlignment: MainAxisAlignment.end,
        crossAxisAlignment: CrossAxisAlignment.end,
        children: [
          FloatingActionButton(
            child: Icon(Icons.add),
            onPressed: () => context.read<CounterBloc>().add(IncrementEvent()),
          ),
          SizedBox(height: 10),
          FloatingActionButton(
            child: Icon(Icons.remove),
            onPressed: () => context.read<CounterBloc>().add(DecrementEvent()),
          ),
        ],
      ),
    );
  }
}
```

## Key Widgets

- **BlocProvider**: Provides a bloc to its children
- **BlocBuilder**: Rebuilds the UI based on bloc state changes
- **BlocListener**: Performs side effects based on state changes
- **BlocConsumer**: Combines BlocBuilder and BlocListener
- **MultiBlocProvider**: Provides multiple blocs to children

For more detailed documentation, refer to the [flutter_bloc package documentation](https://pub.dev/packages/flutter_bloc).

<!-- Add content here -->