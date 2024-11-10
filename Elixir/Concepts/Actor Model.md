Elixir abstracts work into actors. Actor is something that receives, processes and outputs data. Actors live inside processes (not to confuse with actual system processes). Here comes the importance of [[Immutability]], we can have millions of actors acting on the same data. Because the data is immutable, this action is not dangerous.

We can have some cluster of computation and thanks to this model, this is easily done without worry about race conditions and so on. Here are important takeaways:
* Actors run in a processes
* These processes have PIDs
* The processes communicate via Message Passing
* Each process has its own stack and heap allocation
Every actor works with following:
* Actors receive messages in a mailbox
* The messages are ordered in FIFO order
* They are very cheap to create (< 3kb memory)
The process ID can be viewed with command `self`:
```sh
iex(9)> self()  
#PID<0.105.0>
```
