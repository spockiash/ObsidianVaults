## Thinking in functions
In mathematics function is a map between two sets named domain and codomain. Given an element from domain function yields an element from its codomain. The actual formula or logic can be completely arbitrary. Therefore mathematical function is completely abstract object and its output is determined exclusively by its output. In computer programming languages this is not necessarily the case.

### Function as a map
Function can be thought of as a map between its domain and codomain. We can have for example function that maps lower case characters to upper case one. The domain is set of lower case characters `{a,b,c..}` and is mapped to its codomain `{A,B,C...}`. That function can be programmed using char type as its input and output.  We would get function that maps `char` to `char`. The type of function domain and codomain represents interface/signature of that function.

### Representing functions
Functions can be represented in C# by multiple ways:
* [[Delegates in CSharp#Simple delegate example|Delegates]]
* Methods
*  [[Delegates in CSharp#Lambdas|Lambdas]]
* Dictionaries
#### Methods
Methods are C# representation of functions. Methods represents functions but also fit in OOP imperative. They can be used to implement interfaces, be overloaded and so on.
#### Delegates
Delegates are type-safe function pointers. The delegate is strongly typed, so output and input type is known at compilation. Creating delegates is two step process. First delegate is declared and then implementation is provided. This is analogous to creating interface and then instantiating class. First step is done using `delegate` keyword and providing signature for the delegate. For example .NET includes the following definition of a `Comparison<T>` delegate:
```C#
namespace System
{
public delegate int Comparison<in T>(Tx, Ty);
}
```
In this example the delegate can be given two T´s and return `int` indicating which is greater. Once the delegate is declared it can be instantiated providing implementation:
```C#
var list = Enumerable.Range(1,10).Select(i => i * 3).ToList();
// list => {3, 6, 9, 12, 15, 18, 21, 24, 27, 30}
Comparison<int> alphabetically = (l, r) //Provided implementation to delegate Comparison
	=> l.ToString().Compare(r.ToString()); //the delegate is now instantiated as object //alphabetically
list.Sort(alphabetically); //The delegate is now passed as an argument to Sort
// list => {12, 15, 18...}
 ```

#### Func and Action delegates
.NET provides multiple ways of representing functions:
* `Func<R>` represents function that takes no input and returns value of type `R`
* `Func<T1, R>` represents function that takes one input and returns value
* `Func<T1, T2.., R>` represents function that can take up to 16 arguments and return value
* `Action<T>` represents function that does not return value
* `Action` represents function without any input or output
[[Delegates in CSharp#Generic delegates|Func and Action]] provides more convenient way of working with delegates. Instead of writing:
```C#
delegate Greeting Greeter(Person P);
```
We can just use the type:
```C#
Func<Person, Greeting>
```
The Func provides more general way of creating delegates instead of creating custom delegates. For example in previous versions of .NET the delegate `Predicate<T>` was used to represent functions for instance in the `FindAll`method to filter a `List<T>`. In modern .NET there is no more `Predicate<T>` but rather `Funct<T, bool>`. Both functions are equivalent but using `Func` is recommended. Custom delegates can still be useful for more readable code.

#### Lambda expressions
Lambdas are used for declaring inline functions. The compiler converts lambdas into delegates. Lambdas are useful for creating closures, because lambdas have access to variable in scope in which it is defined.
```C#
var days = Enum.GetValues(typeof(DayOfWeek)).Cast<DayOfWeek>();
// => {Sunday, Monday...}
IEnumerable<DayOfWeek> daysStartingWith(string pattern)
	=> days.Where(d => d.ToString().StartsWith(pattern));

daysStartingWith("S")
// => Sunday, Saturday
```
In above example the lambda accepts parameter pattern and has access to days collection. Where method accepts a function that takes `DayOfWeek` and return true or false. The function provided by lambda expression also takes pattern as argument which is captured by the closure.

#### Dictionaries as a function
Dictionaries also called maps or `hashtables` provide very direct representation of a function via data structure. They contain association of keys (domain) and values (codomain). They can be used as functions where we need completely arbitrary where the mapping cannot be computed but must be stored. For example we can have function that maps Boolean values to phrases in French:
```C#
var frenchFor = new Dictionary<bool, string>
{
	[true] = "Vrai",
	[false] = "Faux"
}
frenchFor[true];
// => "Vrai"
```

## Higher order functions
HOFs are functions that take other functions as their argument. Some HOFs take other functions as arguments and then they invoke them. For example `Sort` and `Where`.

For example `List.Sort` when called with a `Comparison` delegate is a method that sorts list elements based on implementation of Comparison we feed it.  `Sort` does the sorting part, but caller decides what logic is used via the delegate. Similarly `Where` does the job of filtering and the caller decides what logic is used. It can be represented like this:
![[HOF_Where_Example.svg]]
Where is a method that iteratively applies predicate. It is typical example of HOF:
```C#
public static IEnumerable<T> Where<T>
	(this IEnumerable<T> ts, Func<T, bool> predicate)
{
	foreach(T t in ts)
	{
		if(predicate(t))
			yield return t;
	}
}	
```
The above example means that Where is iterating over collection and uses predicate function to determine which item are included. The logic is provided by the caller of Where.
HOFs help with separation of concerns where otherwise it would be harder. Where and Sort are examples of iterative application of HOFs.

Another application of HOFs can be conditional invoking. That is invoke the function only when some conditions are met. For example:
```C#
class Cache<T> where T : class
{
	public T Get(Guid id) => //
	public T Get(Guid id, Func<T> onMiss)
		=> Get(id) ?? onMiss();
}
```
The logic of `onMiss`can be computationally expensive task that is called only when `Get(id)` is null. This pattern of passing HOF as parameter is called `inversion of controll`. It is most common way of utilizing HOFs. The caller decides what to do by supplying a function implementation.

## Adapter functions
Some HOFs do not apply the given function at all but rather return a new function related to the function given as an argument. For example lets have function that performs integer division:
```C#
Func<int, int, int> divide = (x, y) => x/y;
divide(10, 2); // => 5
```
We now want to change the order of arguments so that the divisor comes first. We can do that using generic HOF that modifies any binary function by swapping order of its arguments:
```C#
static Func<T2, T1, R> SwapArgs<T1, T2, R> (this Func<T1, T2, R> f)
	=> (t2, t1) => f(t1, t2);
```
This extension method when called upon any binary function will swap order of arguments:
```C#
var divideBy = divide.SwapArgs();
divideBy(2,10);
```
As is seen, when called upon a divide function it will return new function that can be stored in a variable as delegate. When invoked it will call the original function with swapped arguments.
Analogous to adapter pattern in OOP programming, this can be done with functions as well. If one does not like interface of an function we can call it via another function that provides more suitable interface.
### Functions that create another functions
We can have function factories in a sense. That is function that creates another function as a result. The following example shows lambda to filter numbers divisible by two:
```C#
var range = Enumerable.Range(1,20);

range.Where(i => i % 2 == 0);
```
What if we wanted more general way of returning numbers divisible by any number? We can do that by having function that returns suitable predicate that can be passed onto `Where`:
```C#
Funct<int, bool> isMod(int n) => i => i % n == 0;
```
That is example of [[Additional concepts#Curried function|Curried]] function. This takes some static data and returns a function. It can be used like this:
```C#
Range(1,20).Where(isMod(2)); //returns element divisible by 2
```
In this example we use HOF to produce a function that is feed as input to another function `Where`. 
## Using HOFs to avoid duplication
Another common use case for HOFs is to encapsulate and teardown operations. For example when interacting with database it requires some setup to open connection and do some cleanup after it is closed:
```C#
string ConnString = "myDatabase";

var conn = new SqlConnection(connString); //Setup: get connection
conn.Open();

// interact with db

conn.Close(); //Teardown
conn.Dispose(); 
```
More commonly instead of manually disposing the connection we use using statement where the disposal is done automatically at the end of scope:
```C#
using var(var conn = new SqlConnection(connString))
{
	conn.Open();
	//interact wiht db
}
```
Lets have more complicated example of `DbLogger` class with couple of methods that interact with database: `Log` and `GetLogs`:
```C#
using Dapper

public static class DbLogger
{
	string connString;
	public void Log(LogMessage msg)
	{
		using (var conn = new SqlConnection(connString))
		{
			int affectedRows = conn.Execute("sp_create_log",
				msg, commandType: CommandType.StoredProcedure);
		}
	} 
	public IEnumerable<LogMessage> GetLogs(DateTime since)
	{
		var sqlGetLogs = "SELECT * FROM [Logs] WHERE [Timestamp] > @since;"
		using (var conn = new SqlConnection(connString))
		{
			return conn.Query<LogMessage>(sqlGetLogs,
				new {since = since});	
		}
	}
}
```
Notice the two methods have duplication. The setup and teardown logic. The `Execute` and `Query` methods are extension methods on the connection. In both cases the execution depends on acquired connection. This will allow us to represent the connection as a function.
The setup and teardown are always identical, so we can avoid duplication by extracting them into HOFs.
### Encapsulating setup and teardown
What we want to do is to create HOF that will do the setup and teardown while performing parametrized action in the middle. Because connection setup and teardown are much more general than `DbLogger` they can be extracted to new `ConnectionHelper` class.
```C#
using System;
using System.Data;
using System.Data.SqlClient;

public static class ConnectionHelper
{
	public static R Connect<R> (string connString, Func<IDbConnection, R> f)
	{
		using var(conn = new SqlConnection(connString))
		{
			conn.Open();
			return f(conn);
		}
	}
}
```
The connect function performs the setup and teardown and it is parametrized by what it should do between. The signature takes `IDbConnection` and returns generic object. It could be used like this:
```C#
using Dapper;
using static ConnectionHelper;

public class DbLogger
{
	string connString;
	public void Log(LogMessage message)
		=> Connect(connString, c => c.Execute("sp_create_log",
				msg, commandType: CommandType.StoredProcedure));
				
	public IEnumerable<LogMessage> GetLogs(DateTime since)
		=> Connect(connString, c => c.Query<LogMessage>(@"SELECT * FROM [Logs] WHERE [Timestamp] > @since;", new {since = since}));
}
```
Now the `DbLogger` no longer needs to know the details about creating, opening or disposing the connection.
### Turning the using statement into HOF
The using statement can be converted into HOF. The using block does the following:
* Setup - acquires `IDisposable` resource by evaluating a given declaration or expression
* Body - Executes what is inside the block
* Teardown - Exits the block, causing Dispose to be called
```C#
//Convert using into HOF
public static R Using<TDisp, R>(TDisp disposable, Func<TDisp, R> f) where TDisp : IDisposable
{
	using (disposable) return f(disposable); 
}
```
That method can be used now in `ConnectionHelper`:
```C#
using static F; //Name of class where Using is defined
public static R Connect<R>(string connString, Func<IDbConnection, R> f)
	=> Using(new SqlConnection(connString), conn => 
		{conn.Open(); return f(conn);});
```
The `using static` enables invocation of the `Using` function as sort of global replacement for using statement. Unlike using statement we now have Using expression. This has benefits:
* Allows more compact expression-bodied method syntax
* An expression has a value, so the Using function can be composed with other functions

### Drawbacks of HOFs
Using HOFs can have impact of performance because of increased stack use. Debugging can be more difficult. Overusing HOFs can have impact on code readability. 