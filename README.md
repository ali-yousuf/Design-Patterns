# What is design pattern?
Design patterns are typical solutions to commonly occurring problems in software design. They are like pre-made blue-
prints that you can customize to solve a recurring design problem in your code.

# Why Should I Learn Patterns?
- Design patterns are a toolkit of tried and tested solutions
  to common problems in software design. Even if you never
  encounter these problems, knowing patterns is still useful
  because it teaches you how to solve all sorts of problems using
  principles of object-oriented design.
  
- Design patterns define a common language that you and your
  teammates can use to communicate more efficiently. You can
  say, “Oh, just use a Singleton for that,” and everyone will
  understand the idea behind your suggestion. No need to
  explain what a singleton is if you know the pattern and
  its name.

# What is a factory design pattern?  
The Factory Design Pattern is one of the creational design patterns in software engineering. It provides an interface for creating objects in a super class but allows subclasses to alter the type of objects that will be created. The primary purpose of the Factory Pattern is to abstract the process of object creation and decouple it from the rest of the code.

# What problem it solve?
**1. Object Creation Abstraction:** It abstracts the process of object creation, allowing the client code to use an interface or base class to create objects, without needing to specify the exact class of object to be created. This makes the code more flexible and easier to maintain.

**2. Decoupling:** The Factory Pattern helps in decoupling the client code from the concrete implementation of classes. Clients interact with the factory interface, and they don't need to know the specific implementation details of the objects they're using. This promotes loose coupling and makes it easier to change or extend the system without affecting existing code.

**3. Extensibility:** It allows for easy extension of the system by adding new classes that implement the factory interface. When new types of objects need to be created, you can add new concrete factory classes without modifying existing code.

**4. Centralized Control:** It provides a centralized place (the factory) to manage object creation. This can be especially useful when object creation involves complex initialization or configuration that should be consistent across the application.

**5. Dependency Injection:** It can be used for dependency injection, where the factory is responsible for creating and injecting dependencies into other objects.

In summary, the Factory Design Pattern is used to address the problem of creating objects without tightly coupling the client code to the specific classes it needs to instantiate. It promotes flexibility, maintainability, and extensibility in software design by providing a common interface for object creation and allowing for the dynamic selection of the appropriate concrete class to instantiate.

# Example of factory pattern
In Flutter, you can use the Factory Pattern in various scenarios to create objects or widgets dynamically based on certain conditions. Let's consider a real-life example where the Factory Pattern can be applied to create different types of product widgets based on user preferences in an e-commerce app.

**Scenario**: In this scenario, we'll use the Factory Pattern to create product widgets, such as `ShirtWidget`, `ShoeWidget`, and `HatWidget`, based on the type of product selected by the user.

**Implementation**:

1. **Define a Product Widget Interface**:
   Create an abstract class or interface for product widgets. Each product widget should have a common set of properties and methods.

```dart
abstract class ProductWidget {
  String getName();
  String getDescription();
  Widget build(BuildContext context);
}
```

2. **Create Concrete Product Widgets**:
   Implement concrete classes for each type of product widget (e.g., `ShirtWidget`, `ShoeWidget`, and `HatWidget`) that inherit from the `ProductWidget` interface.

```dart
class ShirtWidget implements ProductWidget {
  @override
  String getName() => "T-Shirt";

  @override
  String getDescription() => "A stylish T-shirt for any occasion.";

  @override
  Widget build(BuildContext context) {
    return // Widget implementation for a shirt.
  }
}

class ShoeWidget implements ProductWidget {
  @override
  String getName() => "Running Shoes";

  @override
  String getDescription() => "Comfortable running shoes for sports enthusiasts.";

  @override
  Widget build(BuildContext context) {
    return // Widget implementation for shoes.
  }
}

class HatWidget implements ProductWidget {
  @override
  String getName() => "Baseball Cap";

  @override
  String getDescription() => "A classic baseball cap for a sporty look.";

  @override
  Widget build(BuildContext context) {
    return // Widget implementation for a hat.
  }
}
```

3. **Create a Product Widget Factory**:
   Implement a factory class, `ProductWidgetFactory`, to create product widgets based on user preferences. This class encapsulates the object creation logic.

```dart
class ProductWidgetFactory {
  ProductWidget createProductWidget(String productType) {
    switch (productType) {
      case "Shirt":
        return ShirtWidget();
      case "Shoe":
        return ShoeWidget();
      case "Hat":
        return HatWidget();
      default:
        throw Exception("Invalid product type");
    }
  }
}
```

4. **Client Code in a Flutter Screen**:
   In a Flutter screen or widget, you can use the `ProductWidgetFactory` to create and display product widgets dynamically based on user selections:

```dart
// Inside a Flutter screen or widget
final productType = "Shirt"; // User's product selection
final factory = ProductWidgetFactory();
final productWidget = factory.createProductWidget(productType);

return Column(
  children: [
    Text(productWidget.getName()),
    Text(productWidget.getDescription()),
    productWidget.build(context),
  ],
);
```

In this Flutter example, the Factory Pattern is used to create product widgets dynamically based on user preferences, without the client code needing to know the concrete widget classes. This approach is especially useful in situations where you have various product types, and you want to maintain flexibility in creating and displaying them based on user interactions.

# What is builder pattern?
The Builder Pattern is a creational design pattern in software engineering. It is used to construct a complex object step by step. The pattern provides a way to create an object with numerous parameters, where not all parameters are required or where some have default values. It separates the construction of a complex object from its representation, allowing you to create different variations of an object with the same construction process.

# What problem it solve?

1. **Complex Object Construction**: It simplifies the construction of objects with many optional or default parameters. Instead of having a constructor with a long parameter list, you can use a builder to set only the properties you need, making the code more readable and maintainable.

2. **Immutability**: It allows you to create immutable objects, which can be beneficial in multithreaded environments or when you want to ensure that the object's state remains consistent after construction.

3. **Fluent Interface**: The Builder Pattern often results in a fluent interface, where you can chain method calls to set different properties. This can lead to code that is more expressive and self-documenting.

4. **Variability**: It allows you to create different configurations or variations of an object using the same construction process, making it useful for creating complex objects with different feature sets.

5. **Telescoping Constructors**: It eliminates the need for "telescoping constructors," where you have multiple constructors with varying numbers of parameters, which can be error-prone and hard to maintain.

# Example of builder pattern
In a Flutter project, you can use the Builder Pattern to construct complex UI components, such as forms, dialogs, or custom widgets, by defining a builder class that separates the construction of these components from their final representation. Here's a real-life example using Flutter:

**Scenario**: You're building a Flutter app for creating and customizing user profiles, and you want to use the Builder Pattern to construct user profile widgets, allowing users to customize their profiles with different features, such as avatars, names, and biographies.

**Implementation**:

1. **Define a UserProfile class**:
   Create a class that represents a user profile. The UserProfile class may contain various properties that users can customize.

```dart
class UserProfile {
  final String avatarUrl;
  final String username;
  final String bio;

  UserProfile({required this.avatarUrl, required this.username, required this.bio});
}
```

2. **Create a UserProfileBuilder class**:
   Define a builder class, `UserProfileBuilder`, responsible for constructing user profile widgets. This class will allow users to set the avatar, username, and bio while abstracting the widget construction.

```dart
class UserProfileBuilder {
  String avatarUrl = '';
  String username = '';
  String bio = '';

  UserProfile build() {
    return UserProfile(avatarUrl: avatarUrl, username: username, bio: bio);
  }
  
  UserProfileBuilder withAvatar(String url) {
    avatarUrl = url;
    return this;
  }

  UserProfileBuilder withUsername(String name) {
    username = name;
    return this;
  }

  UserProfileBuilder withBio(String description) {
    bio = description;
    return this;
  }
}
```

3. **Client Code in Flutter UI**:
   In your Flutter UI, you can use the `UserProfileBuilder` to create and customize user profile widgets with different features:

```dart
UserProfile userProfile = UserProfileBuilder()
  .withAvatar('https://example.com/avatar.png')
  .withUsername('John Doe')
  .withBio('A Flutter enthusiast')
  .build();

return Column(
  children: [
    Image.network(userProfile.avatarUrl),
    Text(userProfile.username, style: TextStyle(fontSize: 20)),
    Text(userProfile.bio, style: TextStyle(fontSize: 16)),
  ],
);
```

In this example, the Builder Pattern is applied to create user profile widgets, allowing users to customize their profiles with varying features. The `UserProfileBuilder` class abstracts the widget construction process, providing a fluent interface for setting different profile attributes. This approach separates the construction of the user profile from its representation, making the code more readable and maintainable, especially when dealing with complex UI components.

# What is adapter design pattern?
The Adapter Design Pattern is a structural design pattern that allows objects with incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces, making them compatible without changing their existing code. The Adapter Pattern is often used to integrate new or existing code with third-party libraries or components.

The primary purpose of the Adapter Pattern is to resolve the incompatibility between interfaces or classes by providing a wrapper (the adapter) that translates one interface into another. This pattern solves several problems:

1. **Integration of Legacy Code**: It helps integrate legacy or existing code with new systems or libraries, even if they have different interfaces or expectations.

2. **Third-party Component Integration**: When you want to use a third-party component or library with an interface that doesn't match your requirements, the Adapter Pattern allows you to make it compatible with your existing code.

3. **Interoperability**: It promotes interoperability by allowing systems with different interfaces to communicate and work together effectively.

4. **Maintenance and Extendibility**: When you need to add or replace components in a system, you can create adapters for new components, making it easier to maintain and extend the software.

5. **Testing**: It simplifies the testing of components by providing a consistent and standardized interface for interactions.

6. **Decoupling**: It helps decouple client code from specific implementations, allowing you to change the underlying implementations without affecting the clients.

The Adapter Pattern is particularly useful in scenarios where you cannot or do not want to modify the existing interfaces or code, but you need them to work together seamlessly. It promotes code reusability and maintainability by encapsulating the translation logic within the adapter class, allowing the client code to remain agnostic about the underlying implementation details.

# Example of adapter pettern

In a Flutter project, you can encounter scenarios where you need to use third-party libraries or APIs with different interfaces than what your app expects. The Adapter Pattern can be used to make these third-party components or services compatible with your Flutter application. Here's a real-life example of the Adapter Pattern in a Flutter project:

**Scenario**: You are developing a weather app that fetches weather data from multiple weather service providers, each of which has a different API with distinct methods and data structures. You want to create an adapter to make the weather data retrieval consistent across all providers.

**Implementation**:

1. **Define a Weather Service Interface**:
   Create an abstract class or interface that defines the methods for fetching weather data.

```dart
abstract class WeatherService {
  Future<WeatherData> getWeather(String location);
}
```

2. **Implement Concrete Weather Services**:
   Implement classes for each weather service provider that adhere to the `WeatherService` interface. These classes have their own methods and data structures for fetching weather data.

```dart
class WeatherServiceA implements WeatherService {
  @override
  Future<WeatherData> getWeather(String location) {
    // Implement the logic for fetching data from Service A.
  }
}

class WeatherServiceB implements WeatherService {
  @override
  Future<WeatherData> getWeather(String location) {
    // Implement the logic for fetching data from Service B.
  }
}
```

3. **Create an Adapter for Incompatible Service**:
   Suppose you want to integrate a third-party weather service, Service C, which has a different interface. Create an adapter for Service C that translates its methods into the standard `WeatherService` interface.

```dart
class WeatherServiceCAdapter implements WeatherService {
  final WeatherServiceC serviceC;

  WeatherServiceCAdapter(this.serviceC);

  @override
  Future<WeatherData> getWeather(String location) async {
    final response = await serviceC.fetchWeatherData(location);

    // Convert response from Service C to WeatherData format.
    WeatherData weatherData = WeatherData.fromServiceCResponse(response);

    return weatherData;
  }
}
```

4. **Client Code in Flutter UI**:
   In your Flutter app, you can use the `WeatherService` interface and switch between different weather service providers seamlessly, thanks to the Adapter Pattern:

```dart
void fetchAndDisplayWeather(WeatherService weatherService, String location) async {
  final weatherData = await weatherService.getWeather(location);

  // Update UI with weatherData.
}
```

Now, you can use the `fetchAndDisplayWeather` function with any weather service provider (Service A, Service B, or the adapted Service C) without needing to change the client code. The Adapter Pattern allows you to integrate third-party components with varying interfaces into your Flutter project and maintain a consistent interface for working with them.
