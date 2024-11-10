Computer memory has a general layout that consists of multiple segments. Some of those segments are:
- Stack: stores local variables
- Heap: dynamic memory for programmer to allocate
- Data: stores global variables, separated into initialized and unitialized
- Text: stores the code being executed
![[MemoryDiagramStackAndHeap.JPG]]
[Source](https://courses.engr.illinois.edu/cs225/fa2022/resources/stack-heap/)
Each byte of memory is assigned with  an address. The address is value is represented by convention in base 16 numbers. The address that is designated in low spectrum on the diagram above is have lower numerical values, while the high address ones have large numerical address value. The range goes from `0x00000000` to `0xFFFFFFFF`. 
## Stack
Stack is segment of memory near the top of the address value. Every time a function is called, some stack memory is allocated for it. After the function returns, the memory is deallocated. When new local variable is declared, more stack memory is allocated for that function to store the variable. Such allocations make the stack grow downwards. Allocation and deallocations is done automatically. The variables allocated on the stack are called stack variables or automatic variables.
## Heap
Heap is part of memory that is allocated explicitly by the programmer. Since functions cannot return pointers to stack variables, heap variables are more permanent. The memory space on heap will be allocated until it is deallocated by the programmer.