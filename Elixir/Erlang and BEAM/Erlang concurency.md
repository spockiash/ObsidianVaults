Erlang is sometimes called `concurrent oriented language`. It employs its own techniques for managing processes. Instead of relying on OS processes or threads it uses *BEAM - Bogdan/Björn's Erlang Abstract Machine* or also called the Erlang Virtual Machine. It uses its own scheduler to manage processes.

The processes are primitive type in the Erlang VM called Erlang process:
![[BEAM-Process-diagram.png]]
* The Erlang process is unit of concurrent execution
* The scheduler is an OS thread responsible for executing multiple processes
* BEAM utilizes multiple schedulers to parallelize the work over available CPU cores
# Features of BEAM
## Fault tolerance
Erlang processes are completely isolated from each other. When one crashes it does not affect others. Erlang provides means to detect crashes in processes.
## Scalability
