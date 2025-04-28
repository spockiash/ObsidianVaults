Garbage is data that is no longer pointed to. The garbage collector automatically detects unused memory and cleans it.
## The stack
Stack is consecutive block of memory, every function call in a thread shares the same stack. Allocation to the stack is fast. This is done by changing the value of the stack pointer. When function is invoked a new stack frame is created for the function data. Local variables are stored on the stack, along with parameters passed into a function. Each variable moves the stack pointer by the size of the variable. When function returns value, the values are copied back to the calling function via the stack, the stack pointer is moved back to the beginning of the stack frame for the exited function and this the stack memory is deallocated.

To store something on a stack we have to know how big it is at compile time. For arrays we have to know how big they are before we can create them. Arrays therefore live on a stack instead of heap. The size of a pointer is also known, so pointers are on stack also.

### Go routines
Go routines can expand stack at run time. This is unique to Go because it uses Go runtime to manage the execution rather then relying on operating system.
### Allocating pointer to a stack
To allocate the data pointer points to on the stack the data must be local variable whose data size is known at compile time. The pointer cannot be returned from the function. If the size is not known, then the compiler cannot move the stack because it does not know how.
If the pointer is returned, then the memory that the pointer points to will no longer be valid.

| Situation                                                     | Heap Allocation?       | Why                                 |
| ------------------------------------------------------------- | ---------------------- | ----------------------------------- |
| Local variable, no pointer escaping                           | **No** (stack)         | Safe, short-lived                   |
| Pointer to local variable **returned** or **saved** elsewhere | **Yes** (heap)         | Must live beyond function           |
| Passed as pointer parameter, but callee doesn't store it      | **Usually No** (stack) | Compiler can prove safety           |
| Passed as pointer and **stored globally or returned**         | **Yes** (heap)         | Survives beyond function            |
| Structs of known size and no indirection                      | **No** (stack)         | Compiler knows size at compile time |

## The heap
When the compiler determines data cannot be stored on the stack it stores it on the heap. This is called data the pointer points to escapes the stack and the compiler stores the data on the heap.
Heap is managed by the garbage collector. Any data on the heap is valid as long as it can be tracked back to a pointer type variable on a stack. Once the data in stack is not pointed to by any variable, then the garbage collector frees the memory.

The Go compiler can sometimes be inefficient because it has to be strict and conservative. So it sometimes allocates to a heap something that could be allocated to the stack.
