**.NET**

- C#

- History Of C# #read:bookmark  
    https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history
- What's new in C# 8.0  
    https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-8

- Readonly members (for Struct)

- You can apply the readonly modifier to members of a struct. It indicates that the member doesn't modify state. It's more granular than applying the readonly modifier to a struct declaration.

- What's new in C# 7.0  
    https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-7-3
- Hashtable and dictionary internals  
    [https://docs.microsoft.com/en-us/previous-versions/ms379571(v=vs.80)](https://docs.microsoft.com/en-us/previous-versions/ms379571(v=vs.80))
- Garbage collection in dotnet  
    [https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals](https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals)
- History of changes to C#  
    https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history
- Roslyn SDK  
    https://docs.microsoft.com/en-us/dotnet/csharp/roslyn-sdk/syntax-visualizer?tabs=csharp
- Async TAP  
    https://docs.microsoft.com/en-us/dotnet/csharp/async
- https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap
- https://docs.microsoft.com/en-us/dotnet/standard/async-in-depth
- Drill Into .NET Framework Internals to See How the CLR Creates Runtime Objects  
    http://web.archive.org/web/20150107121958/http://msdn.microsoft.com/en-us/magazine/cc163791.aspx#S14
- Garbage collector in .net core  
    https://medium.com/criteo-labs/spying-on-net-garbage-collector-with-net-core-eventpipes-9f2a986d5705
- latest and greatest features, all used and un-used, language features

- What's new in C# 4.0 #pluralsight  
    https://app.pluralsight.com/player?course=skeet-csharp4&author=jon-skeet&name=skeet-csharp4-m1-overview&clip=3&mode=live

- multi-threading
- MEF Framework
- Dependency Injection  
    Miguel Castro https://youtu.be/RVpADaFIlRw
- https://app.pluralsight.com/library/courses/developing-extensible-software
- Dependency Injection in .NET - Mark Seedman - Manning
- Martin Fowler's DI/IoC article http://martinfowler.com/articles/injection.html

- DI is an architectural pattern designed to easily satisfy class dependencies

- Allows us to write decoupled code
- Facilitate testability
- Ease deployment of components
- typically implemented with the aid of an object container

- DI Containers are used in production. Setting our groundwork for DI Containers helps us write testable software

- A repository for definitions typically relating an abstraction to a concrete class
- Core Functionality

- Provide facility for registering classes

- Usually related to interfaces

- Provide facility for resolving a request

- Usually from a given interface (not always)

- R&R (Register & Resolve)

- Resolving is done recursively. The container recursively goes exporing constructor arguments that are interfaces, and checks if any are registered with it, and provides resolution
- We can ask container to resolve classes that are not registered with it. This will fire the register and resolve process on this class. (container.CreateType<Commerce>())

- Several Containers

- Unity
- NInject
- Castle Windsor
- StructureMap
- MEF

- Mocking tools

- Moq

- 4 Useful Skills With Moq in C# Tests #read:bookmark  
    https://justintimecoder.com/useful-skills-with-moq/
- Mocking delegates with Moq #read:bookmark  
    https://dogschasingsquirrels.com/2018/05/21/mocking-delegates-with-moq/

- RhinoMock
- JustMock
- They basically write a stub class of the interface you will be mocking to do the setup you need.

- Problem space

- One class depending on another (cannot exist without other class)
- Limits functionality to single implementation
- If classes perform DB work, difficult to test without hitting DB
- If two classes are coupled, 

- that is a compliation dependency, and a 
- behavior dependency

- Classes: 

- BillingProcessor (customer, creditCard, price)
- Custom (customer, product)
- Notifier (orderInfo)
- Logger (message)
- Commerce (billingProcessor, customer, notifier, logger) ->Orchestrator class

- Has ProcessOrder method(orderInfo)

- These classes are dependant on each other
- So we turn inputs of Commerce class constructor, into interfaces (to decouple from dependencies)
- In the host class, we create concrete dependencies and pass 

- Constructor injection
- Property injection

- async & Task

- two async functions can perform independently without interruption
- **Task** -> returns no value
- **Task<int>** -> returns int
- **async** method will run synchronously if it does not contain the **await** keyword

- How-To & What

- Array

- Multi-Dimensional (rectangular) [,]
-             //Assigning the array elements at the time of declaration
-             int[,] arr = {{11,12,13,14},
-                           {21,22,23,24},
-                           {31,32,33,34}};
-             //printing values of array using for each loop
-             foreach (int i in arr)
-             {
-                 Console.Write(i + " ");
-             }
-             Console.WriteLine("\n");
-             //printing the values of array using nested for loop
-             for (int i = 0; i < arr.GetLength(0); i++)
-             {
-                 for (int j = 0; j < arr.GetLength(1); j++)
-                 {
-                     Console.Write(arr[i, j] + " ");
-                 }
-             }
- Jagged (array of arrays) [][]  
    static void Main(string[] args)
-         {
-             //Creating an jagged array with four rows
-             int[][] arr = new int[4][];
-             //Initializing each row with different column size
-             // Uisng one dimensional array
-             arr[0] = new int[5];
-             arr[1] = new int[6];
-             arr[2] = new int[4];
-             arr[3] = new int[5];
-             //printing the values of jagged array using nested for loop
-             //It will print the default values as we are assigning any
-             //values to the array
-             for (int i = 0; i < arr.GetLength(0); i++)
-             {
-                 for (int j = 0; j < arr[i].Length; j++)
-                 {
-                     Console.Write(arr[i][j] + " ");
-                 }
-             }
-             Console.WriteLine();
-             //assigning values to the jagged array by using nested for loop
-             for (int i = 0; i < arr.GetLength(0); i++)
-             {
-                 for (int j = 0; j < arr[i].Length; j++)
-                 {
-                     arr[i][j] = j++;
-                 }
-             }
-             //print values the values of jagged array by using foreach loop within for loop
-             for (int i = 0; i < arr.GetLength(0); i++)
-             {
-                 foreach (int x in arr[i])
-                 {
-                     Console.Write(x + " ");
-                 }
-             }
-             Console.ReadKey();
-         }

- F#

- PluralSight  
    https://app.pluralsight.com/profile/author/mark-seemann

- Visual Studio

- Bulk Upgrade dotnet framwork on csproj project files

- Using VS Extension "Target Framework Migrator" by Pavel
- [https://github.com/TargetFrameworkMigrator/TargetFrameworkMigrator](https://github.com/TargetFrameworkMigrator/TargetFrameworkMigrator)

- Remove old *.lock.json *.dgspec.json *.assets.json by del /s *.lock.json recursively removes files matching extensions

- Build csproj from commandline  
    D:\Users\sdivekar\Documents\Git\standard-widgets\OEMS.Common>nuget pack OEMS.Common.csproj   -Properties "Configuration=Release;Platform=AnyCPU" -Verbosity Detailed