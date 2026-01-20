# C# Cheat Sheet

Quick reference for C# syntax, features, and common patterns. C# is a modern, type-safe, object-oriented programming language for .NET development.

## Table of Contents

- [Basics](#basics)
- [Data Types](#data-types)
- [Variables and Constants](#variables-and-constants)
- [Operators](#operators)
- [Control Flow](#control-flow)
- [Methods](#methods)
- [Classes and Objects](#classes-and-objects)
- [Properties](#properties)
- [Collections](#collections)
- [String Operations](#string-operations)
- [Exception Handling](#exception-handling)
- [LINQ](#linq)
- [Async/Await](#asyncawait)
- [Generics](#generics)
- [Interfaces](#interfaces)
- [Delegates and Events](#delegates-and-events)
- [File I/O](#file-io)
- [Attributes](#attributes)
- [Nullable Types](#nullable-types)
- [Pattern Matching](#pattern-matching)
- [Records](#records)
- [Best Practices](#best-practices)
- [Common Patterns](#common-patterns)
- [Troubleshooting](#troubleshooting)
- [Tools & References](#tools--references)

## Basics

```csharp
using System;

// Entry point
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello, World!");
    }
}

// Comments
// Single line comment

/*
Multi-line
comment
*/

/// <summary>
/// XML documentation comment
/// </summary>

// Namespaces
namespace MyNamespace
{
    class MyClass
    {
        // Code here
    }
}
```

## Data Types

```csharp
// Value types
bool isTrue = true;
byte byteValue = 255;
sbyte sbyteValue = -128;
char character = 'A';
short shortValue = 32767;
ushort ushortValue = 65535;
int integer = 2147483647;
uint uintValue = 4294967295;
long longValue = 9223372036854775807L;
ulong ulongValue = 18446744073709551615UL;
float floatValue = 3.14F;
double doubleValue = 3.14159;
decimal decimalValue = 3.14159M;

// Reference types
string text = "Hello";
object obj = new object();
dynamic dynVar = 42; // Can be anything

// Nullable value types
int? nullableInt = null;
bool? nullableBool = true;

// Arrays
int[] numbers = {1, 2, 3, 4, 5};
string[] names = new string[3];
int[,] matrix = new int[3, 3]; // Multidimensional

// Type conversion
int num = Convert.ToInt32("42");
string str = num.ToString();
int parsed = int.Parse("123");
bool success = int.TryParse("abc", out int result);
```

## Variables and Constants

```csharp
// Variables
int age = 25;
var name = "Alice"; // Type inference
string firstName, lastName; // Multiple declarations

// Constants
const double PI = 3.14159;
const string APP_NAME = "MyApp";

// Read-only fields (set once, at runtime)
readonly DateTime startTime = DateTime.Now;

// Static variables
static int count = 0;

// Access modifiers
public int publicVar;
private int privateVar;
protected int protectedVar;
internal int internalVar;
```

## Operators

```csharp
// Arithmetic
+ - * / %

// Assignment
= += -= *= /= %= 

// Comparison
== != < > <= >=

// Logical
&& || !  // Short-circuiting
& | ^    // Bitwise

// Null-conditional operators
string? name = null;
int? length = name?.Length;        // null if name is null
string upper = name?.ToUpper() ?? "UNKNOWN";

// Null-coalescing
string result = name ?? "Default";
name ??= "Default"; // Assign if null

// Pattern matching (C# 8+)
string result = age switch
{
    < 13 => "Child",
    < 20 => "Teenager", 
    < 65 => "Adult",
    _ => "Senior"
};
```

## Control Flow

```csharp
// if/else
if (age >= 18)
{
    Console.WriteLine("Adult");
}
else if (age >= 13)
{
    Console.WriteLine("Teenager");
}
else
{
    Console.WriteLine("Child");
}

// Ternary operator
string category = age >= 18 ? "Adult" : "Minor";

// switch statement
switch (grade)
{
    case 'A':
        Console.WriteLine("Excellent");
        break;
    case 'B':
        Console.WriteLine("Good");
        break;
    case 'C':
    case 'D':
        Console.WriteLine("Pass");
        break;
    default:
        Console.WriteLine("Fail");
        break;
}

// switch expression (C# 8+)
string grade = score switch
{
    >= 90 => "A",
    >= 80 => "B", 
    >= 70 => "C",
    >= 60 => "D",
    _ => "F"
};

// Loops
for (int i = 0; i < 10; i++)
{
    Console.WriteLine(i);
}

foreach (string item in collection)
{
    Console.WriteLine(item);
}

while (condition)
{
    // code
}

do
{
    // code
} while (condition);

// Loop control
break;    // Exit loop
continue; // Skip to next iteration
```

## Methods

```csharp
// Method declaration
public static int Add(int a, int b)
{
    return a + b;
}

// Method overloading
public static double Add(double a, double b)
{
    return a + b;
}

// Optional parameters
public static void Greet(string name, string greeting = "Hello")
{
    Console.WriteLine($"{greeting}, {name}!");
}

// Named arguments
Greet(greeting: "Hi", name: "Alice");

// Variable arguments
public static int Sum(params int[] numbers)
{
    return numbers.Sum();
}

// Out parameters
public static bool TryDivide(int a, int b, out double result)
{
    if (b != 0)
    {
        result = (double)a / b;
        return true;
    }
    result = 0;
    return false;
}

// Ref parameters
public static void Swap(ref int a, ref int b)
{
    int temp = a;
    a = b;
    b = temp;
}

// Expression-bodied members
public static int Square(int x) => x * x;
public static void Log(string message) => Console.WriteLine(message);
```

## Classes and Objects

```csharp
// Class definition
public class Person
{
    // Fields
    private string name;
    private int age;
    
    // Constructor
    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }
    
    // Default constructor
    public Person() : this("Unknown", 0) { }
    
    // Methods
    public void Introduce()
    {
        Console.WriteLine($"Hi, I'm {name}, {age} years old");
    }
    
    // Static members
    public static int Population { get; set; }
    
    static Person()
    {
        Population = 0;
    }
}

// Object creation
Person person1 = new Person("Alice", 30);
Person person2 = new(); // Target-typed new (C# 9+)
var person3 = new Person { }; // Object initializer

// Primary constructors (C# 12+)
public class Point(int x, int y)
{
    public int X { get; } = x;
    public int Y { get; } = y;
    
    public double DistanceFromOrigin() => Math.Sqrt(X * X + Y * Y);
}

// Usage with primary constructor
var point = new Point(3, 4);

// Inheritance
public class Student : Person
{
    public string School { get; set; }
    
    public Student(string name, int age, string school) : base(name, age)
    {
        School = school;
    }
    
    // Method overriding
    public override void Introduce()
    {
        base.Introduce();
        Console.WriteLine($"I study at {School}");
    }
}

// Abstract class
public abstract class Animal
{
    public abstract void MakeSound();
    
    public virtual void Sleep()
    {
        Console.WriteLine("Sleeping...");
    }
}

// Sealed class (cannot be inherited)
public sealed class FinalClass
{
    // Implementation
}
```

## Properties

```csharp
public class Product
{
    // Auto-implemented properties
    public string Name { get; set; }
    public decimal Price { get; set; }
    
    // Read-only property
    public string Id { get; }
    
    // Init-only property (C# 9+)
    public DateTime CreatedDate { get; init; }
    
    // Property with backing field
    private int stock;
    public int Stock
    {
        get { return stock; }
        set 
        { 
            if (value < 0)
                throw new ArgumentException("Stock cannot be negative");
            stock = value;
        }
    }
    
    // Expression-bodied properties
    public bool InStock => Stock > 0;
    public string DisplayName => $"{Name} - ${Price}";
    
    // Constructor
    public Product(string id)
    {
        Id = id;
        CreatedDate = DateTime.Now;
    }
}

// Usage
var product = new Product("P001")
{
    Name = "Laptop",
    Price = 999.99m,
    Stock = 5
};
```

## Collections

```csharp
// List<T>
var numbers = new List<int> { 1, 2, 3, 4, 5 };
numbers.Add(6);
numbers.Remove(3);
numbers.RemoveAt(0);

// Collection expressions (C# 12+)
int[] array = [1, 2, 3, 4, 5];
List<string> list = ["apple", "banana", "cherry"];
HashSet<int> set = [1, 2, 3, 3, 4]; // Duplicates automatically handled

// Spread operator in collection expressions
int[] first = [1, 2, 3];
int[] second = [4, 5, 6];
int[] combined = [..first, ..second]; // [1, 2, 3, 4, 5, 6]
int[] withExtra = [0, ..first, 10]; // [0, 1, 2, 3, 10]

// Dictionary<K, V>
var ages = new Dictionary<string, int>
{
    ["Alice"] = 30,
    ["Bob"] = 25
};
ages["Charlie"] = 35;

if (ages.TryGetValue("Alice", out int age))
{
    Console.WriteLine($"Alice is {age} years old");
}

// HashSet<T>
var uniqueNumbers = new HashSet<int> { 1, 2, 3, 3, 4 }; // Only unique values

// Queue<T> and Stack<T>
var queue = new Queue<string>();
queue.Enqueue("first");
queue.Enqueue("second");
string first = queue.Dequeue();

var stack = new Stack<int>();
stack.Push(1);
stack.Push(2);
int top = stack.Pop();

// Array operations
int[] arr = { 1, 2, 3, 4, 5 };
Array.Sort(arr);
Array.Reverse(arr);
int index = Array.IndexOf(arr, 3);
```

## String Operations

```csharp
string text = "Hello World";

// Basic operations
int length = text.Length;
bool contains = text.Contains("World");
bool starts = text.StartsWith("Hello");
bool ends = text.EndsWith("World");
string upper = text.ToUpper();
string lower = text.ToLower();
string trimmed = "  text  ".Trim();

// Substring
string sub = text.Substring(6); // "World"
string sub2 = text.Substring(0, 5); // "Hello"

// Replace and Split
string replaced = text.Replace("World", "Universe");
string[] words = text.Split(' ');

// String interpolation
string name = "Alice";
int age = 30;
string message = $"Hello {name}, you are {age} years old";

// Verbatim strings
string path = @"C:\Users\Alice\Documents";

// String.Format
string formatted = string.Format("Hello {0}, you are {1} years old", name, age);

// StringBuilder for multiple operations
var sb = new StringBuilder();
sb.Append("Hello");
sb.AppendLine(" World");
sb.Insert(5, ",");
string result = sb.ToString();

// Null and empty checks
bool isEmpty = string.IsNullOrEmpty(text);
bool isWhitespace = string.IsNullOrWhiteSpace(text);
```

## Exception Handling

```csharp
// Basic try-catch
try
{
    int result = 10 / 0;
}
catch (DivideByZeroException ex)
{
    Console.WriteLine($"Error: {ex.Message}");
}
catch (Exception ex)
{
    Console.WriteLine($"General error: {ex.Message}");
}
finally
{
    Console.WriteLine("This always runs");
}

// Throwing exceptions
public void ValidateAge(int age)
{
    if (age < 0)
        throw new ArgumentException("Age cannot be negative", nameof(age));
    
    if (age > 150)
        throw new ArgumentOutOfRangeException(nameof(age), "Age too high");
}

// Custom exception
public class InvalidUserException : Exception
{
    public InvalidUserException() : base() { }
    public InvalidUserException(string message) : base(message) { }
    public InvalidUserException(string message, Exception innerException) 
        : base(message, innerException) { }
}

// Using statement for automatic disposal
using (var file = new StreamWriter("data.txt"))
{
    file.WriteLine("Hello");
} // file.Dispose() called automatically

// Using declaration (C# 8+)
using var file2 = new StreamWriter("data2.txt");
file2.WriteLine("World");
// file2.Dispose() called at end of scope
```

## LINQ

```csharp
using System.Linq;

var numbers = new[] { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
var people = new[]
{
    new { Name = "Alice", Age = 30, City = "New York" },
    new { Name = "Bob", Age = 25, City = "London" },
    new { Name = "Charlie", Age = 35, City = "New York" }
};

// Filtering
var evens = numbers.Where(n => n % 2 == 0);
var adults = people.Where(p => p.Age >= 18);

// Projection
var doubled = numbers.Select(n => n * 2);
var names = people.Select(p => p.Name);

// Aggregation
int sum = numbers.Sum();
double average = numbers.Average();
int max = numbers.Max();
int count = people.Count(p => p.City == "New York");

// Ordering
var sorted = numbers.OrderBy(n => n);
var sortedDesc = numbers.OrderByDescending(n => n);
var sortedPeople = people.OrderBy(p => p.Age).ThenBy(p => p.Name);

// Grouping
var groupedByCity = people.GroupBy(p => p.City);
foreach (var group in groupedByCity)
{
    Console.WriteLine($"{group.Key}: {group.Count()} people");
}

// First/Last/Single
var first = numbers.First(); // Throws if empty
var firstOrDefault = numbers.FirstOrDefault(); // Returns default if empty
var single = numbers.Single(n => n == 5); // Throws if 0 or >1 matches

// Any/All
bool hasEvens = numbers.Any(n => n % 2 == 0);
bool allPositive = numbers.All(n => n > 0);

// Query syntax
var query = from p in people
            where p.Age > 25
            orderby p.Name
            select p.Name;
```

## Async/Await

```csharp
using System.Threading.Tasks;

// Async method
public async Task<string> GetDataAsync()
{
    await Task.Delay(1000); // Simulate async work
    return "Data retrieved";
}

// Async method without return value
public async Task ProcessDataAsync()
{
    string data = await GetDataAsync();
    Console.WriteLine(data);
}

// Calling async methods
public async Task MainAsync()
{
    // Wait for completion
    string result = await GetDataAsync();
    
    // Fire and forget (generally avoid)
    _ = ProcessDataAsync();
    
    // Wait for multiple tasks
    Task<string> task1 = GetDataAsync();
    Task<string> task2 = GetDataAsync();
    string[] results = await Task.WhenAll(task1, task2);
    
    // Wait for first completion
    Task<string> completed = await Task.WhenAny(task1, task2);
    string firstResult = await completed;
}

// HTTP client example
using var client = new HttpClient();
string json = await client.GetStringAsync("https://api.example.com/data");

// ConfigureAwait
public async Task<string> LibraryMethodAsync()
{
    // Use ConfigureAwait(false) in library code
    return await GetDataAsync().ConfigureAwait(false);
}
```

## Generics

```csharp
// Generic class
public class GenericList<T>
{
    private List<T> items = new List<T>();
    
    public void Add(T item)
    {
        items.Add(item);
    }
    
    public T Get(int index)
    {
        return items[index];
    }
}

// Generic method
public static T GetFirst<T>(IEnumerable<T> collection)
{
    return collection.First();
}

// Constraints
public class Repository<T> where T : class, new()
{
    public T CreateNew()
    {
        return new T(); // new() constraint allows this
    }
}

// Multiple constraints
public static T Process<T>(T item) 
    where T : class, IComparable<T>, new()
{
    return item;
}

// Usage
var stringList = new GenericList<string>();
stringList.Add("Hello");

var intList = new GenericList<int>();
intList.Add(42);

string first = GetFirst(new[] { "a", "b", "c" });
```

## Records

```csharp
// Record declaration (C# 9+)
public record Person(string Name, int Age);

// Usage
var person1 = new Person("Alice", 30);
var person2 = person1 with { Age = 31 }; // Non-destructive mutation

// Record with additional members
public record Employee(string Name, int Age, string Department)
{
    public string DisplayName => $"{Name} ({Department})";
    
    public bool IsRetirementAge => Age >= 65;
}

// Record class vs record struct
public record class PersonClass(string Name, int Age); // Reference type
public record struct PersonStruct(string Name, int Age); // Value type

// Positional records with validation
public record Product(string Name, decimal Price)
{
    public Product : this(Name, Price)
    {
        if (Price < 0)
            throw new ArgumentException("Price cannot be negative");
    }
}

// Record inheritance
public record Animal(string Name);
public record Dog(string Name, string Breed) : Animal(Name);

// Deconstruction
var employee = new Employee("Bob", 25, "IT");
var (name, age, dept) = employee;
```

## Pattern Matching

```csharp
// Switch expressions with patterns
object value = "Hello";
string result = value switch
{
    string s when s.Length > 5 => "Long string",
    string s => "Short string", 
    int i when i > 0 => "Positive number",
    int i => "Non-positive number",
    null => "Null value",
    _ => "Unknown type"
};

// Property patterns
public record Point(int X, int Y);

string Classify(Point point) => point switch
{
    { X: 0, Y: 0 } => "Origin",
    { X: 0 } => "On Y axis",
    { Y: 0 } => "On X axis", 
    { X: var x, Y: var y } when x == y => "On diagonal",
    _ => "Somewhere else"
};

// List patterns (C# 11+)
int[] numbers = { 1, 2, 3, 4 };
string pattern = numbers switch
{
    [] => "Empty",
    [var x] => $"Single: {x}",
    [var x, var y] => $"Two: {x}, {y}",
    [var first, .., var last] => $"First: {first}, Last: {last}",
    _ => "Other"
};

// Type patterns
if (obj is string { Length: > 0 } str)
{
    Console.WriteLine($"Non-empty string: {str}");
}
```

## Nullable Types

```csharp
// Nullable reference types (enabled in project file)
#nullable enable

string? nullableString = null; // Can be null
string nonNullableString = "Hello"; // Cannot be null

// Null-forgiving operator
string result = nullableString!; // Tell compiler you know it's not null

// Null checks
if (nullableString is not null)
{
    Console.WriteLine(nullableString.Length); // Safe to use
}

// Pattern matching with null
string message = nullableString switch
{
    null => "No value",
    "" => "Empty string", 
    var s => $"Value: {s}"
};

// Nullable value types
int? nullableInt = null;
int value = nullableInt ?? 0; // Null coalescing

// Nullable attributes
public void ProcessString([NotNull] string? input)
{
    if (input is null)
        throw new ArgumentNullException(nameof(input));
    
    // Compiler knows input is not null here
    Console.WriteLine(input.Length);
}
```

## Interfaces

```csharp
// Interface definition
public interface IShape
{
    double Area { get; }
    void Draw();
    
    // Default implementation (C# 8+)
    void PrintInfo()
    {
        Console.WriteLine($"Shape with area: {Area}");
    }
}

// Implementation
public class Rectangle : IShape
{
    public double Width { get; set; }
    public double Height { get; set; }
    
    public double Area => Width * Height;
    
    public void Draw()
    {
        Console.WriteLine($"Drawing rectangle {Width}x{Height}");
    }
}

// Multiple interfaces
public interface IComparable<T>
{
    int CompareTo(T other);
}

public class Person : IComparable<Person>
{
    public string Name { get; set; }
    public int Age { get; set; }
    
    public int CompareTo(Person other)
    {
        return Age.CompareTo(other.Age);
    }
}
```

## Delegates and Events

```csharp
// Delegate declaration
public delegate void NotifyHandler(string message);

// Event declaration
public class Publisher
{
    public event NotifyHandler SomethingHappened;
    
    protected virtual void OnSomethingHappened(string message)
    {
        SomethingHappened?.Invoke(message);
    }
    
    public void DoSomething()
    {
        OnSomethingHappened("Something happened!");
    }
}

// Usage
var publisher = new Publisher();
publisher.SomethingHappened += message => Console.WriteLine($"Received: {message}");
publisher.SomethingHappened += PrintMessage;

static void PrintMessage(string msg)
{
    Console.WriteLine($"Handler: {msg}");
}

// Built-in delegates
Action action = () => Console.WriteLine("Action executed");
Action<string> actionWithParam = msg => Console.WriteLine(msg);
Func<int, int, int> add = (a, b) => a + b;
Predicate<int> isEven = n => n % 2 == 0;
```

## File I/O

```csharp
using System.IO;

// Reading files
string content = File.ReadAllText("file.txt");
string[] lines = File.ReadAllLines("file.txt");
byte[] bytes = File.ReadAllBytes("file.dat");

// Writing files
File.WriteAllText("output.txt", "Hello World");
File.WriteAllLines("lines.txt", new[] { "Line 1", "Line 2" });
File.AppendAllText("log.txt", "New log entry\n");

// Stream operations
using var fileStream = new FileStream("data.bin", FileMode.Create);
using var writer = new BinaryWriter(fileStream);
writer.Write(42);
writer.Write("Hello");

using var reader = new StreamReader("input.txt");
string line;
while ((line = reader.ReadLine()) != null)
{
    Console.WriteLine(line);
}

// Directory operations
Directory.CreateDirectory("NewFolder");
string[] files = Directory.GetFiles(".", "*.txt");
string[] directories = Directory.GetDirectories(".");
bool exists = Directory.Exists("SomeFolder");

// Path operations
string fullPath = Path.Combine("folder", "subfolder", "file.txt");
string extension = Path.GetExtension("file.txt"); // ".txt"
string fileName = Path.GetFileName(fullPath);
string directory = Path.GetDirectoryName(fullPath);
```

## Best Practices

```csharp
// 1. Use meaningful names
public class CustomerService // Good
{
    public async Task<Customer> GetCustomerByIdAsync(int customerId)
    {
        // Implementation
    }
}

// 2. Follow naming conventions
public class PascalCaseClass { }
public void PascalCaseMethod() { }
public int camelCaseField;
private const int UPPER_CASE_CONST = 42;

// 3. Use properties over public fields
public class Product
{
    public string Name { get; set; } // Good
    // public string name; // Avoid
}

// 4. Initialize collections
public class Order
{
    public List<OrderItem> Items { get; } = new List<OrderItem>(); // Good
}

// 5. Use string interpolation
string message = $"Hello {name}!"; // Good
// string message = "Hello " + name + "!"; // Avoid

// 6. Use var for obvious types
var customers = new List<Customer>(); // Good
Customer customer = new Customer(); // Also good when type isn't obvious

// 7. Handle nulls properly
public void ProcessName(string name)
{
    if (string.IsNullOrWhiteSpace(name))
        throw new ArgumentException("Name cannot be null or empty", nameof(name));
    
    // Process name
}

// 8. Use using statements for disposables
using (var connection = new SqlConnection(connectionString))
{
    // Use connection
} // Automatically disposed

// 9. Prefer readonly for immutable fields
private readonly ILogger logger;

// 10. Use ConfigureAwait(false) in library code
public async Task<string> GetDataAsync()
{
    return await httpClient.GetStringAsync(url).ConfigureAwait(false);
}
```

## Tools & References

### Development Tools
- **Visual Studio 2025** / **VS Code**: Primary IDEs
- **dotnet CLI**: Command-line interface (.NET 10+)
- **NuGet**: Package manager
- **MSBuild**: Build system
- **GitHub Codespaces**: Cloud development environment
- **JetBrains Rider**: Cross-platform .NET IDE

### Useful Commands
```bash
# Create new project (.NET 10+)
dotnet new console -n MyApp -f net10.0
dotnet new classlib -n MyLibrary
dotnet new web -n MyWebApp
dotnet new blazorserver -n MyBlazorApp

# Build and run
dotnet build
dotnet run
dotnet test
dotnet watch run  # Hot reload

# Package management
dotnet add package Microsoft.EntityFrameworkCore
dotnet restore
dotnet list package --outdated

# Publishing
dotnet publish -c Release --self-contained
dotnet publish -c Release -r win-x64 --single-file

# Global tools
dotnet tool install -g dotnet-ef
dotnet workload install aspire
```

### Documentation & Learning
- [Microsoft C# Documentation](https://docs.microsoft.com/en-us/dotnet/csharp/)
- [C# Programming Guide](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/)
- [.NET API Reference](https://docs.microsoft.com/en-us/dotnet/api/)

### Code Analysis
- **StyleCop**: Code style analysis
- **FxCop/Roslyn Analyzers**: Code quality analysis
- **SonarQube**: Static code analysis

---

*This cheat sheet covers C# essentials for everyday development. For advanced topics like unsafe code, P/Invoke, or framework-specific features, refer to the official documentation.*
```
```
```