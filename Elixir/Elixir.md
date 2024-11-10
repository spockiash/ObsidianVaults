Elixir is functional programming language for reliable fault proof scalable. This note is root note that will act as signpost to different parts. Text here provides very high level overview and will evolve over time. As this is mostly notes, there will be mistakes.
# Functional Programming
In functional programming there generally are not classes, the data should be immutable and the functions should also be stateless. When the function is stateless it means it is not dependent on other parts of the system and the function can be easily distributed.

As a result of these restrictions in purely functional languages we cannot have for loops. This is because of immutability. Instead `FP` languages are relying on recursion.
## Recursion
In simplest of terms, recursion is the act of calling itself. Recursive function will call itself inside the function implementation.