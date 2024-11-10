Delegate is a type that references a method. It is effectively a function pointer. When delegate is instantiated, any method with compatible signature and return type can be assigned to it. Delegates are used to pass methods as arguments to other methods. For example event handlers are nothing more than methods that are invoked through delegates. Below is example of an delegate declaration.
```C#
public delegate int PerformCalculation(int x, int y)
```
Any method from accessible class or struct that matches delegate type (integer in case above)  and its parameters can be assigned to the delegate. The method can be either static or an instance method. The de

## Overview of delegates
* Delegates are similar to C++ function pointers
* Delegates allow methods to be passed as parameters
* Delegates can be used to define callback methods
* Delegates can be chained together, so multiple methods can be called on single event
* Methods do not have to match the delegate type exactly (variance and covariance)
* Lambda expressions are compiled to delegate type
## Simple delegate example
Delegates can be useful when we want to delegate implementation of method. When we have the following class:
```C#
using WarehouseManagementSystem.Domain;

namespace WarehouseManagementSystem.Business
{
    public class OrderProcessor
    {
        public delegate void OrderInitialized();
        public delegate void ProcessCompleted();

        public OrderInitialized OnOrderInitialized { get; set; }
        private void Initialize(Order order)
        {
            ArgumentNullException.ThrowIfNull(order);

            OnOrderInitialized?.Invoke();
        }

        public void Process(Order order, ProcessCompleted? onCompleted = default)
        {
            // Run some code..

            Initialize(order);

            onCompleted?.Invoke();
            // How do I produce a shipping label?
        }
    }
}
```
First we declare delegates `OrderInitialized` and `ProcessCompleted`. The first delegate is then used as type for declaring property `OnOrderInitialized` that is used as event handler when order is initialized via the `Initialize` method. The Invoke method is used to invoke the method. The delegate can be called directly as a method `OnOrderInitialized`, but using Invoke method is better. The second delegate is used as parameter for `Process` method. Both delegates can be assigned with matching method:
```C#
using WarehouseManagementSystem.Business;
using WarehouseManagementSystem.Domain;

var order = new Order();

var processor = new OrderProcessor();

processor.OnOrderInitialized = SendMessageToWarehouse;

processor.Process(order, SendConfirmationEmail);

void SendMessageToWarehouse()
{
    Console.WriteLine("Plelase pack the order");
}

void SendConfirmationEmail()
{
    Console.WriteLine("Order Confirmation Email");
}
```
In this example we first access the `OnOrderInitialized` property of the `OrderProcessor` class and assign it with `SendMessageToWarehouse` method. We do not use parentheses and simply state its name. 
The second delegate is used in method signature, so we can pass method `SendConfirmationEmail` to the `Process` method.
## Multicast delegate and chains
Multiple methods can be appended to one delegate. This is done using `+` operator with limitation that left hand operand must be a delegate type:
```C#
public delegate SomeDelegateType MyDelegate {get; set;}
MyDelegate += FirstMethod;
MyDelegate += SecondMethod;
MyDelegate += ThirdMethod;
```
The delegate can be assigned with same method multiple times. This will result with the method executing that times it was assigned to that delegate when invoked.
```C#
MyDelegate += FirstMethod;
MyDelegate += FirstMethod;
MyDelegate.Invoke(); //Executed first method twice
```
The delegate can be assigned with method multiple times on same line when we cast the the first element to delegate type. Otherwise we cannot assign multiple methods to a delegate on one line.
Delegates can be removed as well using `-` operator:
```C#
MyDelegate -= FirstMethod;
```
When multiple delegates of the same type are assigned multiple times, when we remove a delegate using this operator, last method being removed present in the delegate chain will be removed.
## Lambdas
Lambdas are anonymous function useful for defining a method inline. Lambda syntax uses parameters in parentheses on left hand side and assigned to right hand side expression or statement using lambda operator `=>`. 
```C#
(parameter1, parameter2) => parameter1 + parameter2; //right hand side is expression, this is called lambda expression
(parameter1, parameter2) => 
//statement body
{
	//this is lambda statement
	return parameter1 + parameter2;
}
```

When lambda is used, the compiler will try to infer correct parameter types and return types. Lambda expressions are meant to return value. Lambda statements can return void. To return void in lambda expression void return type method must be called. Here is example of lambda assigned to delegate:
```C#
OrderProcessor.OrderInitialized action = (order) =>
{
	return order.IsReadyForShipment;
}
```

Lambdas can be chained as well:
```C#
OrderProcessor.ProcessCompleted chain = (order) =>
{
    Console.WriteLine($"Process completed: {order.OrderNumber}");
};

chain += (order) =>
{
    Console.WriteLine("Refill stock...");
};
```
## Lambdas, Minimal APIs and Attributes
Lambdas are important in ASP.NET Minimal APIs. They are used to construct behavior of API endpoints. Together with their usage in minimal APIs they can be used with attributes. The attribute is placed inside left hand side parentheses before parameter:
```C#
//minimal API example with attributes
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();
//FromHeader attribute signifies that the parameter comes from request header
app.MapGet("/", ([FromHeader]string accept) => $"Header: {accept}");
```
### Lambdas in LINQ
In LINQ there are generic methods that accepts delegates as an argument. Therefore lambdas can be sued to define the method for example filter method in where:
```c#
people.Where(person => person.Age > 20);
```
## Generic delegates
.NET provides [[FP Intro#Func and Action delegates|`Action<T>` and `Func<T, TResult>`]] for working with generic delegates. They can accept up to 16 parameters of generic type. `Action` is used for void return type delegates and `Func` is used for delegates that have value return type. If we define `Func` with Order and bool type, we get a delegate that accepts `Order` type and return `bool` type. 
```C#
Func<Order, bool> func = SendMessageToWarehouse;

public bool SendMessageToWarehouse(Order order)
{
	//logic
	return true; //or false
}
```
The above defines delegate `func` that point to a method that sends message to warehouse. We can now use it as a normal delegate and pass it to a method for example.