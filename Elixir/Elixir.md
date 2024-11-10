Elixir is functional programming language for reliable fault proof scalable. This note is root note that will act as signpost to different parts. Text here provides very high level overview and will evolve over time. As this is mostly notes, there will be mistakes.
# Functional Programming
In functional programming there generally are not classes, the data should be immutable and the functions should also be stateless. When the function is stateless it means it is not dependent on other parts of the system and the function can be easily distributed.

As a result of these restrictions in purely functional languages we cannot have for loops. This is because of immutability. Instead `FP` languages are relying on recursion.
## Recursion
In simplest of terms, recursion is the act of calling itself. Recursive function will call itself inside the function implementation.
# Elixir files
Elixir can have two file extensions: `*.ex` and `*.exs`. The first one is compile file and second one is elixir script. the script files are not meant for production but instead for development purposes and testing.
# Modules and code structure
The elixir code is put inside modules. Elixir does not use brackets, instead it uses `do` `end` blocks:
```Elixir
defmodule Hello do

end
```
By convention the module and file name should be same.
## Hello world
Functions are defined using `def` keyword:
```Elixir
defmodule Hello do
	def world do
		IO.puts("Hello Elixir");
	end
end
```