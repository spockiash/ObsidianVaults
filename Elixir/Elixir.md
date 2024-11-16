Elixir is functional programming language for reliable fault proof scalable. This note is root note that will act as signpost to different parts. Text here provides very high level overview and will evolve over time. As this is mostly notes, there will be mistakes.
# [[Functional vs OOP Concepts|Functional Programming]]
In [[Functional vs OOP Concepts| functional programming]] there generally are not classes, the data should be [[Immutability | immutable]] and the functions should also be stateless. When the function is stateless it means it is not dependent on other parts of the system and the function can be easily distributed.

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
When we run this nothing happens, because we need to add one line:
```Elixir
Hello.world()
```
# Execution
The simplest way to execute a script is with command `elixir hello.exs`. This will execute the script. If we want to compile our program we use `elixirc hello.exs`. This creates file `*.beam` and executes our compiled program.
# [[Types Overview]]
```sh
1          # integer
0x1F       # integer
1.0        # float
true       # boolean
:atom      # atom / symbol
"elixir"   # string
[1, 2, 3]  # list
{1, 2, 3}  # tuple
```
Elixir supports as fundamental: integers, floats, booleans, atoms and strings.
## [[Basic Arithmetic]]
## [[Numeric Literals]]
# [[Pattern Matching]]
