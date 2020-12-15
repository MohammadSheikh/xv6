# xv6 - an OS consisting of a stripped down version of Unix

### Changes made to original version:
#### System Calls -
* Extended the current xv6 process implementation to maintain an exit status. Stores the exit status of the terminated process in the corresponding structure.
* The system call ```wait()``` prevents the current process from executing until the child processes are terminated. It returns the terminated child's exit status through the status that is stores. Returns the PID of the child that is terminated.
* New system call ```waitpid()``` is implemented in order to act similarly to the ```wait()``` system call but with additional features as such:
  * ```waitpid()``` waits for a process with a PID that equals to one provided by that specific pid argument. 
  * The return value is the PID of the process that was terminated.
  * A blocking waitpid where the kernel prevents the current process from executing until a process with the given PID terminates.
#### Scheduler -
* Changed the scheduler from a regular round-robin to a "priority" scheduler. 
  * Added a priority value to each process that ranges from 0 to 31. 
  * The highest priority process is scheduled first with all the processes having a default initialized priority of 10.
* Added a new system call ```setpriority()``` in order to change the priority of a process which can change the priority at any time. Whenever the priority becomes lower than any process on the "ready" list, it switches to that particular process
#### Memory Management -
* Growing the stack
  * It automatically starts growing the stack backwards whenever needed.
  * A page fault handler is implemented in order to prevent page fault from occurring when the stack grows beyond its allocated page because it is accesses an unmapped page.
* Changing the Memory Layout
  * Stack pointer will now point towards the top of the page (i.e. right under the KERNEL BASE).
  * The virtual address of the first page now points to the top page of the modified stack pointer (i.e. right under the KERNEL BASE).
  
