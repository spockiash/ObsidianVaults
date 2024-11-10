`Event` keyboard that is used to declare an event in a publisher class. When we talk about events there are two classes:
* Publisher - the class that owns the event and is in charge of raising it
* Subscriber - the class that subscribes to events exposed by publisher
## Creating event
The event is created by starting with `event` keyword followed by [[Delegates in CSharp#Overview of delegates|delegate]]:
```C#
public event EventHandler OrderCreated; 
```
Do not use your own delegates `Func` or `Action`. The event delegate should never return a value. Therefore the delegate that it is based on is always void. We should use delegate `EventHandler` or `EventHandler<T>`. 
The `EventHandler` delegate defines two parameters:
* `sender` - source of the event of type object
* `EventArgs e` - the event data
The sender is instance of the publisher that raised the event. The `EventArgs` inherits from `EventArgs` to create class that represents the event data.
Without the `event` keyword it would behave like delegate. With the keyword it can be invoked only in the class where it is declared.
The `event` keyword will generate add and remove as opposed getters and setters on publicly exposed properties.

This ensures that whoever is accessing the event from outside is only allowed to add or remove the delegate from invocation list.
```C#
public class OrderProcessor
{
public event EventHandler OrderCreated;
}

var processor = new OrderProcesor();
processor.OrderCreated += Procesor_OrderCreated;
```
Above is an example of creating event `OrderCreated` that anyone can access via instance of the class in where the event is defined.

To use events practically in the publisher class we define the event with its delegate and provide overridable invocation using `virtual` method with type `void`:
```C#
public class OrderProcessor
{
	public event EventHandler OrderCreated;
	protected virtual void OnOrderCreated()
	{
		OrderCreated?.Invoke(this, EventArgs.Emtpy);
	}
}
```
Because the method is protected and virtual, derived class can override this and provide custom implementation. The subclass should always provide base implementation for the event to be properly published:
```C#
public class BatchOrderProcessor : OrderProcessor
{
	protected override void OnOrderCreated()
	{
		base.OnOrderCreated();
	}
}
```
The subclass cannot call the event by itself. The only class that is allowed to call the event is the one who ones it. To execute the event we need to call it when needed in the publisher:

```C#
//inside class OrderProcessor
public void Process(Order order, Action<Order> onCompleted)
{
    // Run some code..

    Initialize(order);
    OnOrderCreated(); // here we raise the event
    onCompleted?.Invoke(order);
    // How do I produce a shipping label?
}
```
The publisher should never care about what the subscriber does when event is raised.
### Subscribing to Events
The raising of an event is handled only in the publisher class, the subscriber does not have access to the execution. It only provides what will be invoked. The invocation is done sequentially in order in which it was created. If there is slow function, it will slow down the whole process.

> [!warning] Warning!
> When adding handler to event, it is important to remove it afterwards (unsubscribe)

```C#
var processor = new OrderProcessor();
processor.OrderCreated += Handle_OrderCreated;
...// do stuff
processor.OrderCreated -= Handle_OrderCreated; //unsubscribe
```

## Event Data

To receive custom data we can use `EventArgs` type. We can expand using custom class:
```C#
class OrderCreatedEventArgs : EventArgs
{
	public Order Order {get; set;}
}

//The event handler
void Processor_OrderCreated(object sender, EventArgs args)
{
var eventData = args as OrderCreatedEventArgs;
}
```
In modern .NET there is generic version of `EventArgs<T>` that can do the same as above code:
```C#
class OrderProcessor
{
	public event EventHandler<OrderCreatedEventArgs> OrderCreated;
}
```
Having event data that inherits from `EventArgs` can be useful and is valid method. A method using `EventArgs` could be used as delegate if the event data class inherits from it.
## Unsubscribing
Unsubscribing is done using `-=` operator. When using event do not use lambdas, because they are not easily removed from the event invocation chain. Unsubscribing is important, because objects with subscribed events cannot be disposed of.
When using event or delegates remember:
* Events can be invoked only by its publisher
* Delegates can be invoked by everyone who has access to it
