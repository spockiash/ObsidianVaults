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
The processes communicate via asynchronous messages. This means there are no complex synchronization mechanisms such as locks, mutexes or semaphores.
Typical Erlang systems are divided into large number of processes that combine into single system. The virtual machine can efficiently parallelize the execution and distributes the workload across available CPU cores making Erlang very scalable.
## Distribution
