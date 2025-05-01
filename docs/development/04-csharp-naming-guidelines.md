# C# Naming Guidelines

This document describes the naming guidelines to be used when naming identifiers in C# code used in this project.

## Overview and Sources

These C# identifier naming guidelines are designed to ensure consistency and maintainability across the codebase. They are sourced from the following locations.

- The [Microsoft C# identifier naming rules and conventions document][identifier-naming].
- The [IDesign C# Coding Standard document][idesign-csharp-standard].

## Naming Rules

Valid identifiers must follow these rules. The C# compiler produces an error for any identifier that doesn't follow these rules:

- Identifiers must start with a letter or underscore (`_`).
- Identifiers can contain Unicode letter characters, decimal digit characters, Unicode connecting characters, Unicode combining characters, or Unicode formatting characters.
- Avoid using C# reserved keywords as identifiers unless prefixed with `@` (e.g., `@class`).

## Naming Guidelines

In addition to the rules enforced by the compiler, this project adopts the following guidelines for naming identifiers.

- An identifier is the name you assign to any of the following:
  - `class`
  - `interface`
  - `struct`
  - `delegate`
  - `enum`
  - member
  - variable
  - parameter
  - type parameter (e.g. `List<T>`, `<TSession>`)
  - namespace
- While the compiler does not enforce these rules, these guidelines provide consistency and clarity in naming identifiers.
- This project will one contain or more `editor.config` files that will help enforce these guidelines.

### ***Readable and Descriptive***

All identifiers should be named with readability in mind, the following broad guidelines support this ideal.

- Identifiers should not contain two consecutive underscore (`_`) characters. Those names are reserved for compiler-generated identifiers.
- Names should clearly describe the purpose of the identifier.
- Prefer clarity over brevity.
- Avoid abbreviations unless they are widely understood (e.g., `Http`, `Xml`).

### ***PascalCase***

Use PascalCase for the following identifiers.

- #### `Class`

  ```csharp
  public class DataService
  {
  }
  ```

- #### `Record`

  In addittion to the record name, primary constructor/positional parameters of the record type should also be named using PascalCase as they are public properties of the record.

  ```csharp
  // Positional Parameters
  public record PhysicalAddress(
      string Street,
      string City,
      string StateOrProvince,
      string ZipCode);
  ```

- #### `Struct`

  ```csharp
  public struct ValueCoordinate
  {
  }
  ```

- #### `Delegate`

  ```csharp
  public delegate void DelegateType(string message);
  ```

- #### `Enum`

  Use pascal case for enum type names and values. In addition when naming enum types, use a singular noun for nonflags, and a plural noun for flags.

  ```csharp
  public enum Color
  {
      Red = 1,
      Blue = 2,
      Green = 3
  }

  [Flags]
  public enum Options
  {
      None = 0,
      Option1 = 1,
      Option2 = 2,
      Option3 = 4,
      Option4 = 8
  }
  ```

- #### `Interface`

  When naming an `interface`, use pascal case. In addition, prefix the name with an `I`. This prefix clearly indicates to consumers that it's an `interface`.

  ```csharp
  public interface IWorkerQueue
  {
  }
  ```

- #### Public Type Members (`properties`, and `events`)

  ```csharp
  public class ExampleEvents
  {
      // An init-only property
      public IWorkerQueue WorkerQueue { get; init; }

      // Standard auto property
      public string FirstName { get; set; }

      // An event
      public event Action EventProcessing;
  }
  ```

- #### Methods and Local Functions

  ```csharp
  // Method
      public void StartEventProcessing()
      {
          // Local function
          static int CountQueueItems() => WorkerQueue.Count;
          // ...
      }
  ```

- #### Type Parameters

  The following guidelines apply to type parameters on generic type parameters. Type parameters are the placeholders for arguments in a generic type or a generic method.

  - Name generic type parameters with descriptive names, unless a single letter name is completely self explanatory and a descriptive name wouldn't add value.

    ```csharp
    public interface ISessionChannel<TSession> { /*...*/ }
    public delegate TOutput Converter<TInput, TOutput>(TInput from);
    public class List<T> { /*...*/ }
    ```

  - Use `T` as the type parameter name for types where a single letter name is completely self explanatory and a descriptive name wouldn't add value.

    ```csharp
    public int IComparer<T>() => 0;
    public delegate bool Predicate<T>(T item);
    public struct Nullable<T> where T : struct { /*...*/ }
    ```

  - When naming descriptive type parameters, use pascal case. In addition prefix the type parameter name with a `T`. This prefix clearly indicates to consumers that this is a type parameter.

    ```csharp
    public interface ISessionChannel<TSession>
    {
        TSession Session { get; }
    }
    ```

  - Consider indicating constraints placed on a type parameter in the name of parameter. For example, a parameter constrained to `ISession` might be called `TSession`.

### ***camelCase***

Use camelCase for the following identifiers.
- #### `Private` or `Internal` fields

  When naming `private` or `internal` fields use camel case. In addition, prefix the name with an underscore (`_`).

  ```csharp
  public class DataService
  {
      private IWorkerQueue _workerQueue;

      public DataService(IWorkerQueue queue)
      {
        _workerQueue = queue;
      }
  }
  ```

- #### Method Parameters and Local Variables

  ```csharp
  void MyMethod(int someNumber)
  {
      int number;
  }
  ```

- #### Primary Constructor Paramaters on `class` and `struct` Types

  See [Declare primary constructors for classes and structs][primary-const-class-struct] for details on using primary constructors for `class` and `struct` types.

### ***ALL_CAPS***

- Use ALL_CAPS with an underscore (`_`) between words when naming constant identifiers, regardless of scope.

  ```csharp
  public class MyClass
  {
      const int MY_INT_CONSTANT = 10;

      private string MyMessage()
      {
          const string MY_STRING_CONSTANT = "Hello World";
          return MY_STRING_CONSTANT;
      }
  }
  ```

### ***Acronyms***

- Use pascal case for acronyms longer than two charactors (e.g., `XmlParser`, not `XMLParser`).
- Use all uppercase for two-character acronyms (e.g. `IOStream`).

[identifier-naming]: https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/identifier-names
[idesign-csharp-standard]: https://www.idesign.net/Resources/Standards
[primary-const-class-struct]: https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/tutorials/primary-constructors