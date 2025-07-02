---
applyTo: "**"
---
# General Code Guidelines

This document describes the coding guidelines to be applied to this project.

## Overview and Sources

Coding guidelines are essential for maintaining code readability, consistency, and collaboration within a development team. The guidelines in this document are sourced from the following locations. After creating your project from this template, the primary code maintainer should update this document to reflect the guidelines specific to this project and remove this sentence to indicate that any required updates have been completed.

- The [Microsoft Common C# code conventions document][coding-conventions].
- The [IDesign C# Coding Standard][idesign-csharp-standard].
- The [Ode to Code .NET Core Opinion Blog Series][ode-to-code].

## .NET Solution and File Organization

See [Repository Directory Structure][repo-dir-structure] for overall directory layout.

- The .NET solution file should be located in the root of the `src` directory.
- Each C# project should be located in its own directory under the the appropriate root directory.
  - `src` for functional projects
  - `tst` for test projects.
- Logical folder structure. The folder structure beneath each root project folder should match the project namespace structure as much as possible.
- Clear and nonconflicting namespaces
- One class per file
- File names match class names unless partial class definitions are required.

## Tools and Analyzers

- **Tools** such as [CodeRush][coderush], [ReSharper][resharper], and others can help your team enforce your conventions. You can enable code analysis to enforce the rules you prefer. You can also create one or more `.editorconfig` files so that Visual Studio automatically enforces your style guidelines. Mutliple `.editorconfig` files can be placed in scope based on file location. Both of the tools described above also support the same `.editorconfig` file(s) for enforcing rules.

- **Analyzers** like [GitHub Code Scanning][github-code-scan] can be used to scan code during a CI/CD process and produce warnings and diagnostics when it detects rule violations. You can configure the rules you want, including those defined in the solution's `.editorconfig` file(s). Then, each CI build notifies developers when they violate any of the rules.

## C# Language Guidelines

### General Language Style Guidelines

- Utilize modern language features and C# versions whenever possible.
- Avoid outdated language constructs.
- Use LINQ queries and methods for collection manipulation to improve code readability.
- Use asynchronous programming with async and await for I/O-bound operations.
- Be cautious of deadlocks and use Task.ConfigureAwait when appropriate.
- Use the language keywords for data types instead of the runtime types. For example, use `string` instead of `System.String`, or `int` instead of `System.Int32`. This recommendation includes using the types `nint` and `nuint`.
- Use `int` rather than unsigned types. The use of `int` is common throughout C#, and it's easier to interact with other libraries when you use `int`.
- Avoid overly complex and convoluted code logic (i.e. keep it simple).

### Layout Guidelines

- Use four spaces for indentation, except for `.csproj` files, use two spaces for indentation of `.csproj` files. Don't use tabs.
- Write only one statement per line.
- Write only one declaration per line.
- If continuation lines aren't indented automatically, indent them one tab stop (four spaces).
- Add at least one blank line between method definitions and property definitions.
- Use parentheses to make clauses in an expression apparent

  ```csharp
  if ((startX > endX) && (startX > previousX))
  {
      // Take appropriate action.
  }
  ```

- Align code consistently to improve readability.
- Improve clarity and user experience by breaking long statements into multiple lines.
- Line breaks should occur before binary operators, if necessary.
- Use the "Allman" style for braces: open and closing brace its own new line. Braces line up with current indentation level.

  ```csharp
  public class Math
  {
    public int Add(int firstNumber, int secondNumber)
    {
        return firstNumber + secondNumber;
    }
  }
  ```

### Comment Guidelines

- Use single-line comments (`//`) for brief explanations.
- Avoid multi-line comments (`/* */`).
- If multi-line comments are absolutely required, use a series of single-line comments (`//`).
- Place the comment on a separate line, not at the end of a line of code.
- Comments should be complete sentences compleate with upper case first letter and appropriate punctuation to end the comment.
- Insert one space between the comment delimiter (`//`) and the comment text.

  ```csharp
  // The following declaration creates a query. It does not run
  // the query.
  ```

- Avoid comments that explain the obvious. Code should be selfexplanatory. Good code with readable variables and method names should not require comments.
- Comments should generally describe *why* code is written as it is, not *what* the code does. Examples of the kinds of things to document with comments include operational assumptions and algorithm insights.

- If your code is accessible outside the current solution (e.g. API or Class Library), use [XML comments][xml-comments] for describing methods, classes, fields, and all public members. See [Recommended XML tags for C# documentation comments][xml-recommended-tags] for detailed XML tag recommendations.

### String Data Guidelines

- Use [string interpolation][string-interpolation] to concatenate short strings.

  ```csharp
  string displayName = $"{nameList[n].LastName}, {nameList[n].FirstName}";
  ```

- To append strings in loops, especially when you're working with large amounts of text, use a [StringBuilder][string-builder] object.

  ```csharp
  var phrase = "lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala";
  var manyPhrases = new StringBuilder();
  for (var i = 0; i < 10000; i++)
  {
      manyPhrases.Append(phrase);
  }
  //Console.WriteLine("tra" + manyPhrases);
  ```

- Prefer raw string literals to escape sequences or verbatim strings.

  ```csharp
  var phrase = "lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala";
  var manyPhrases = new StringBuilder();
  for (var i = 0; i < 10000; i++)
  {
      manyPhrases.Append(phrase);
  }
  //Console.WriteLine("tra" + manyPhrases);
  ```

- Use the expression-based string interpolation rather than positional string interpolation.

  ```csharp
  // Execute the queries.
  Console.WriteLine("scoreQuery:");
  foreach (var student in scoreQuery)
  {
      Console.WriteLine($"{student.Last} Score: {student.score}");
  }
  ```

### Constructor and Initialization Guidelines

- Use Pascal case for primary constructor parameters on record types (See [/docs/development/04-csharp-naming-guidelines.md#record][record-param-pascal]).
- Use camel case for primary constructor parameters on class and struct types (See [/docs/development/04-csharp-naming-guidelines.md#primary-constructor-paramaters-on-class-and-struct-types][class-struct-primary])
- Use required properties instead of constructors to force initialization of property values.

  ```csharp
  public class LabelledContainer<T>(string label)
  {
      public string Label { get; } = label;
      public required T Contents
      {
          get;
          init;
      }
  }
  ```

### Array and Collection Guidelines

- Use collection expressions to initialize all collection types.

  ```csharp
  string[] vowels = [ "a", "e", "i", "o", "u" ];
  List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
  ```

### Delegate Guidelines

- Use [`Func<>` and `Action<>`][func-action] instead of defining delegate types. In a class, define the delegate method.

  ```csharp
  Action<string> actionExample1 = x => Console.WriteLine($"x is: {x}");

  Action<string, string> actionExample2 = (x, y) =>
      Console.WriteLine($"x is: {x}, y is {y}");

  Func<string, int> funcExample1 = x => Convert.ToInt32(x);

  Func<int, int, int> funcExample2 = (x, y) => x + y;
  ```

- Call the method using the signature defined by the Func<> or Action<> delegate.

  ```csharp
  actionExample1("string for x");

  actionExample2("string for x", "string for y");

  Console.WriteLine($"The value is {funcExample1("1")}");

  Console.WriteLine($"The sum is {funcExample2(1, 2)}");
  ```

- If you create instances of a delegate type, use the concise syntax. In a class, define the delegate type and a method that has a matching signature.

  ```csharp
  public delegate void Del(string message);

  public static void DelMethod(string str)
  {
      Console.WriteLine($"DelMethod argument: {str}");
  }
  ```

- Create an instance of the delegate type and call it. The following declaration shows the condensed syntax.

  ```csharp
  Del exampleDel2 = DelMethod;
  exampleDel2("Hey");
  ```

### Exception Handling Guidelines

- Only catch exceptions for which you have explicit handling.
- Use a try-catch statement for most exception handling.
- If a catch statement throws an exception, always rethrow the original exception (or another exception constructed from the original exception) to maintain the stack location of the original error.

  ```csharp
  using System;
  using System.IO;
  using System.Data.SqlClient;

  public class DataProcessor
  {
      public string ProcessFile(string filePath)
      {
          try
          {
              // Attempt to read from file
              string content = File.ReadAllText(filePath);
              return ProcessContent(content);
          }
          catch (FileNotFoundException ex)
          {
              // Explicit handling for missing file
              Console.WriteLine($"File not found: {filePath}");
              return string.Empty;
          }
          catch (SqlException ex) when (ex.Number == 4060)
          {
              // Explicit handling for database access issue
              try
              {
                  LogDatabaseFailure(ex);
                  return "Database unavailable";
              }
              catch (Exception loggingEx)
              {
                  // Rethrow the original exception to preserve the stack trace
                  // by passing it as inner exception
                  throw new ApplicationException("Failed while handling database error", ex);
              }
          }
          catch (UnauthorizedAccessException ex)
          {
              // Example of simple rethrowing - preserves original stack trace
              Console.WriteLine("Permission error detected");
              throw; // Use naked "throw" to preserve the original stack trace
          }
          // We don't catch IOException or other exceptions - they'll propagate up
      }

      private string ProcessContent(string content)
      {
          return content.ToUpper();
      }

      private void LogDatabaseFailure(Exception ex)
      {
          // Simulate logging that might fail
          if (DateTime.Now.Second % 2 == 0) // Arbitrary condition to simulate failure
              throw new IOException("Log storage unavailable");

          Console.WriteLine($"Logged error: {ex.Message}");
      }
  }
  ```

### `IDisposable` Object Guidelines

- Prefer `using` statement over `try-finally` block.

  ```csharp
  using System.IO;

  class UsingStatement
  {
      static void Main()
      {
          var buffer = new char[50];
          using (StreamReader streamReader = new("file1.txt"))
          {
              int charsRead = 0;
              while (streamReader.Peek() != -1)
              {
                  charsRead = streamReader.Read(buffer, 0, buffer.Length);
                  //
                  // Process characters read.
                  //
              }
          }
      }
  }
  ```

- Prefer new using declaration syntax when the intent is clear without the additional braces

  ```csharp
  using System.IO;

  class UsingDeclaration
  {
      static void Main()
      {
          var buffer = new char[50];
          using StreamReader streamReader = new("file1.txt");

          int charsRead = 0;
          while (streamReader.Peek() != -1)
          {
              charsRead = streamReader.Read(buffer, 0, buffer.Length);
              //
              // Process characters read.
              //
           }
     }
  }
  ```

### Logical Operator Guidelines

- Use `&&` instead of `&` and `||` instead of `|` when you perform comparisons, as shown in the following example.

  ```csharp
  Console.Write("Enter a dividend: ");
  int dividend = Convert.ToInt32(Console.ReadLine());

  Console.Write("Enter a divisor: ");
  int divisor = Convert.ToInt32(Console.ReadLine());

  if ((divisor != 0) && (dividend / divisor) is var result)
  {
      Console.WriteLine($"Quotient: {result}");
  }
  else
  {
      Console.WriteLine("Attempted division by 0 ends up here.");
  }
  ```

  If the divisor is 0, the second clause in the if statement would cause a run-time error. But the `&&` operator short-circuits when the first expression is false. That is, it doesn't evaluate the second expression. The `&` operator would evaluate both, resulting in a run-time error if the divisor is 0.

### 'new' Operator Guidelines

- Use one of the concise forms of object instantiation when the variable type matches the object type, as shown in the following declarations. This form isn't valid when the variable is an interface type, or a base class of the runtime type.

  ```csharp
  var firstExample = new ExampleClass();
  ```

  ```csharp
  ExampleClass instance2 = new();
  ```

  The preceding declarations are equivalent to the following declaration.

  ```csharp
  ExampleClass secondExample = new ExampleClass();
  ```

- Use object initializers to simplify object creation.

  ```csharp
  var thirdExample = new ExampleClass { Name = "Desktop", ID = 37414,
    Location = "Redmond", Age = 2.3 };
  ```

### Event Handling Guidelines

- Use a lambda expression to define an event handler that you don't need to remove later.

  ```csharp
  public Form2()
  {
      this.Click += (s, e) =>
          {
              MessageBox.Show(
                  ((MouseEventArgs)e).Location.ToString());
          };
  }
  ```

### Static Member Guidelines

Call static members by using the class name: `ClassName.StaticMember`. This practice makes code more readable by making static access clear. Don't qualify a static member defined in a base class with the name of a derived class. While that code compiles, the code readability is misleading, and the code might break in the future if you add a static member with the same name to the derived class.

### LINQ Query Guidelines

- Prefer [method syntax][linq-method-syntax] over [query syntax][linq-query-syntax].

  ```csharp
  // Define list to query
  List<int> numbers = [ 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 ];

  //LINQ Query Syntax (less desirable syntax)
  IEnumerable<int> filteringQuery =
      from num in numbers
      where num is < 3 or > 7
      select num;

  //LINQ Method Syntax (preferred syntax)
    IEnumerable<int> filteringQuery = numbers.Where(num => num < 3 || num > 7);
  ```

- Use aliases to make sure that property names of anonymous types are correctly capitalized, using Pascal casing.

  ```csharp
  var localDistributors = Customers.Join(
      Distributors,
      customer => customer.City,
      distributor => distributor.City,
      (customer, distributor) => new { Customer = customer, Distributor = distributor });
  ```

- Rename properties when the property names in the result would be ambiguous. For example, if your query returns a customer name and a distributor name, instead of leaving them as a form of `Name` in the result, rename them to clarify `CustomerName` is the name of a customer, and `DistributorName` is the name of a distributor.

  ```csharp
  var localDistributors2 = Customers.Join(
      Distributors,
      customer => customer.City,
      distributor => distributor.City,
      (customer, distributor) => new { CustomerName = customer.Name, DistributorName = distributor.Name });
  ```

- Use implicit typing in the declaration of query variables and range variables. This guidance on implicit typing in LINQ queries overrides the general rules for implicitly typed local variables. LINQ queries often use projections that create anonymous types. Other query expressions create results with nested generic types. Implicit typed variables are often more readable.

  ```csharp
  var seattleCustomers = Customers
      .Where(customer => customer.City == "Seattle")
      .Select(customer => customer.Name);
  ```

- Use where clauses before other query clauses to ensure that later query clauses operate on the reduced, filtered set of data.

  ```csharp
  var seattleCustomers2 = Customers
      .Where(customer => customer.City == "Seattle")
      .OrderBy(customer => customer.Name);
  ```

### Implicitly Typed Local Variable Guidelines

- Use [implicit typing][implicit-typing] for local variables when the type of the variable is obvious from the right side of the assignment.

  ```csharp
  var message = "This is clearly a string.";
  var currentTemperature = 27;
  ```

- Don't use `var` when the type isn't apparent from the right side of the assignment. Don't assume the type is clear from a method name. A variable type is considered clear if it's a `new` operator, an explicit cast, or assignment to a literal value.

  ```csharp
  int numberOfIterations = Convert.ToInt32(Console.ReadLine());
  int currentMaximum = ExampleClass.ResultSoFar();
  ```

- Don't use variable names to specify the type of the variable. It might not be correct. Instead, use the type to specify the type, and use the variable name to indicate the semantic information of the variable. The following example should use `string` for the type and something like `iterations` to indicate the meaning of the information read from the console.

  ```csharp
  var inputInt = Console.ReadLine();
  Console.WriteLine(inputInt);
  ```

- Avoid the use of `var` in place of [dynamic][built-in-ref]. Use `dynamic` when you want run-time type inference. For more information, see [Using type dynamic (C# Programming Guide)][using-dynamic].
- Use implicit typing for the loop variable in `for` loops.

  ```csharp
  var phrase = "lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala";
  var manyPhrases = new StringBuilder();
  for (var i = 0; i < 10000; i++)
  {
      manyPhrases.Append(phrase);
  }
  //Console.WriteLine("tra" + manyPhrases);
  ```

- Don't use implicit typing to determine the type of the loop variable in `foreach` loops. In most cases, the type of elements in the collection isn't immediately obvious. The collection's name shouldn't be solely relied upon for inferring the type of its elements.

  ```csharp
  foreach (char ch in laugh)
  {
      if (ch == 'h')
      {
          Console.Write("H");
      }
      else
      {
          Console.Write(ch);
      }
  }
  Console.WriteLine();
  ```

- Use implicit type for the result sequences in LINQ queries. Many LINQ queries result in anonymous types where implicit types must be used. Other queries result in nested generic types where `var` is more readable.

### Namespace Guidelines

- Prefer block scoped namespace declarations. While most code files declare a single namespace, this not always the case. More importantly, the block scoped namespace declaration more clearly defines the scope of the namespace and provides better visual separation of namespace and type definitions.

  ```csharp
  using System;

  namespace MySampleCode
  {
      public MySampleClass
      {
        // Class definition
      }
  }
  ```

- Place `using` directives outside the namespace declaration. When a `using` directive is outside a namespace declaration, that imported namespace is its fully qualified name. The fully qualified name is clearer. When the `using` directive is inside the namespace, it could be either relative to that namespace, or its fully qualified name.

  ```csharp
  using Azure;

  namespace CoolStuff.AwesomeFeature
  {
      public class Awesome
      {
          public void Stuff()
          {
              WaitUntil wait = WaitUntil.Completed;
              // ...
          }
      }
  }
  ```

[coding-conventions]: https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions
[idesign-csharp-standard]: https://www.idesign.net/Resources/Standards
[ode-to-code]: https://odetocode.com/blogs/scott/archive/2018/08/28/net-core-opinion-1-structuring-a-repository.aspx
[repo-dir-structure]: /docs/development/01-repository-guidelines.md#directory-structure
[coderush]: https://www.devexpress.com/products/coderush/
[resharper]: https://www.jetbrains.com/resharper/
[github-code-scan]: https://docs.github.com/en/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning
[string-interpolation]: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated
[string-builder]: https://learn.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=net-9.0
[record-param-pascal]: /docs/development/04-csharp-naming-guidelines.md#record
[class-struct-primary]: /docs/development/04-csharp-naming-guidelines.md#primary-constructor-paramaters-on-class-and-struct-types
[func-action]: https://learn.microsoft.com/en-us/dotnet/standard/delegates-lambdas
[linq-method-syntax]: https://learn.microsoft.com/en-us/dotnet/csharp/linq/get-started/write-linq-queries#example---method-syntax
[linq-query-syntax]: https://learn.microsoft.com/en-us/dotnet/csharp/linq/get-started/write-linq-queries#example---query-syntax
[implicit-typing]: https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables
[built-in-ref]: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types
[using-dynamic]: https://learn.microsoft.com/en-us/dotnet/csharp/advanced-topics/interop/using-type-dynamic
[xml-comments]: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/xmldoc/
[xml-recommended-tags]: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/xmldoc/recommended-tags
