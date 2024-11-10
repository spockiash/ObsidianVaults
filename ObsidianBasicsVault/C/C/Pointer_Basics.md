Pointers are variables that point to memory address of another variable. Variable can be stored in range of memory addresses that are represented by hexadecimal numbers. Pointers store the address range for any variable that the pointer points to.

## Declaring pointers
Pointer is declared in same way as ordinary variable. The name of the pointer is preceded by asterisk:
`int *p`
The declaration states that pointer variable is capable of pointing to objects of type int. Pointers can point to area of memory that does not belong to any variable. Pointer declarations can appear alongside another variables:
`int i, j a[10], b[20], *p, *q`
C requires that pointer can point only to particular type as it were declared:
- integer pointer can point only to integer variable
- float pointer can point only to float variable
- etc.
## The Address and Indirection operators
C provides pair of operators designed specifically for use with pointers. To find an address we use `&` address operator. If `x` is an variable then `&x` is address of x in memory. To gain access to the object that pointer points to we use indirection `*` operator. If p is an pointer, then `*p` represents the object to which `p` points to.
### The Address Operator
When we declare pointer, it does not make it point to an object:
`int *p; /* point to nowhere */`
It is crucial to initialize p before we use it. When we declare pointer, we then need to assign to it address of some variable or more generally an lvalue:
`int i, *p;`
`...`
`p = &i;`
That statement of assigning address of `i` to variable `p` is what makes the pointer point to variable.
It is also possible to assign pointer at the same time we declare it:
```c
int i;
int *p = &i;
```
We can combine declaration of `i` with declaration of `p`, provided that `i` is declared first:
```c
int i, *p = &i;
```
### The Indirection Operator
Once a pointer variable points to an object, we can use the indirection operator `*` to access what is stored in the object. If `p` point to `i`, for example, we can print the value of `i` as follows:
```c
printf("%d\n", *p);
```
Above statement will print the value of the object that pointer points to, not its address.
Applying '&' to a variable produces a pointer to that variable, while applying `*` to the pointer takes us back to the original value:
```c
j = *&i; /* same as j = i */
```
As long as `p` points to `i`, `*p` is an alias for `i`. `*p`  has the same value as `i`, but changing the value of `*p` also changes the value of `i`.

>[!warning] Warning!
> Never assign value directly to an pointer. Never apply indirection operator directly to an uninitialized variable. If pointer variable has not been initialized, attempting to use it will cause undefined behavior.

### Pointer Assignment
C allows the use of assignment operator to copy pointers, provided that they have the same type. Suppose that `i`, `j`, `p` and  `q` have been declared as follows:
`int i, j, *p, *q;
Then statement:
`p = &i;`
is an example of pointer assignment. The address of `i` is copied into `p`. Here another example of pointer assignment:
`q = p`;
The statement copies the contents of `p` (the address of `i`) into `q`, in effect making `q` point to the same place as `p`.
If we change `p` or `q` value by assigning we can change the value of `i`:
![[PointerAssignment.JPG]]
The assignment `*q = *p` copies value that p points to into object that q points to.