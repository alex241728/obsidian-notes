# Structure
```c
struct thread
```
- Represents a thread or a user process. In the projects, you will have to add your own members to `struct thread`. You may also change or delete the definitions of existing members.
- Every `struct thread` occupies the beginning of its own page of memory. The rest of the page is used for the thread's stack, which grows downward from the end of the page. It looks like this: 
	![[Pasted image 20260219141234.png]]
	This has two consequences. First, `struct thread` must not be allowed to grow too big. If it does, then there will not be enough room for the kernel stack. The base `struct thread` is only a few bytes in size. It probably should stay well under 1 kB.
	Second, kernel stacks must not be allowed to grow too large. If a stack overflows, it will corrupt the thread state. Thus, kernel functions should not allocate large structures or arrays as non-static local variables. Use dynamic allocation with `malloc()` or `palloc_get_page()` instead.
# Members
```c
tid_t tid
```
The thread's thread identifier or _tid_. Every thread must have a tid that is unique over the entire lifetime of the kernel. By default, `tid_t` is a `typedef` for `int` and each new thread receives the numerically next higher tid, starting from 1 for the initial process. You can change the type and the numbering scheme if you like.

```c
enum thread_status status
```
- The thread's state
- Thread States
	- `THREAD_RUNNING`
		- The thread is running. 
		- Exactly one thread is running at a given time. 
		- `thread_current()` returns the running thread.
	- `THREAD_READY`
		- The thread is ready to run, but it's not running right now. The thread could be selected to run the next time the scheduler is invoked. Ready threads are kept in a doubly linked list called `ready_list`.
##### `THREAD_BLOCKED`
- The thread is waiting for something, e.g. a lock to become available, an interrupt to be invoked.
- The thread won't be scheduled again until it transitions to the `THREAD_READY` state with a call to `thread_unblock()`.
##### `THREAD_DYING`
- The thread will be destroyed by the scheduler after switching to the next thread.
### char **name[16]**
The thread's name as a string, or at least the first few characters of it.
### uint8_t stack
- Every thread has its own stack to keep track of its state. 
	- When the thread is running, the CPU's stack pointer register tracks the top of the stack and this member is unused. 
	- But when the CPU switches to another thread, this member saves the thread's stack pointer. 
	- No other members are needed to save the thread's registers, because the other registers that must be saved are saved on the stack.
- When an interrupt occurs, whether in the kernel or a user program, an `struct intr_frame` is pushed onto the stack. When the interrupt occurs in a user program, the `struct intr_frame` is always at the very top of the page.
### int **priority**
- A thread priority, ranging from `PRI_MIN` (0) to `PRI_MAX` (63). 
	- Lower numbers correspond to lower priorities, so that priority 0 is the lowest priority and priority 63 is the highest.
### `struct list_elem` **allelem**
- This "list element" is used to link the thread into the list of all threads. Each thread is inserted into this list when it is created and removed when it exits. 
- The `thread_foreach()` function should be used to iterate over all threads.
### `struct list_elem` **elem**

A "list element" used to put the thread into doubly linked lists, either `ready_list` (the list of threads ready to run) or a list of threads waiting on a semaphore in `sema_down()`. It can do double duty because a thread waiting on a semaphore is not ready, and vice versa.

Member of `struct thread`: uint32_t ***pagedir**

Only present in project 2 and later. See section [4.1.2.3 Page Tables](https://thierrysans.me/CSCC69/projects/WWW/pintos_4.html#SEC59).

Member of `struct thread`: unsigned **magic**

Always set to `THREAD_MAGIC`, which is just an arbitrary number defined in threads/thread.c, and used to detect stack overflow. `thread_current()` checks that the `magic` member of the running thread's `struct thread` is set to `THREAD_MAGIC`. Stack overflow tends to change this value, triggering the assertion. For greatest benefit, as you add members to `struct thread`, leave `magic` at the end.
# Functions
```c
void thread_init (void)
```
- Called by `main()` to initialize the thread system.
- Main purpose: To create a `struct thread` for Pinto's initial thread.
- `thread_current()` will fail because the running thread's `magic` value is incorrect.

```c
void thread_start (void)
```
- Called by `main()` to start the scheduler. 
	- Creates the idle thread, that is, the thread that is scheduled when no other thread is ready. 
	- Then enables interrupts, which as a side effect enables the scheduler because the scheduler runs on return from the timer interrupt, using `intr_yield_on_return()`.

```c
void Thread_tick (void)
```
- Called by the timer interrupt at each timer tick. It keeps track of thread statistics and triggers the scheduler when a time slice expires.

```c
void thread_print_stats (void)
```
- Called during Pintos shutdown to print thread statistics.

```c
tid_t thread_create (const char *name, int priority, thread_func *func, void *aux)
```
- Creates and starts a new thread named name with the given priority, returning the new thread's tid. The thread executes func, passing aux as the function's single argument.
- `thread_create()` allocates a page for the thread's `struct thread` and stack and initializes its members, then it sets up a set of fake stack frames for it 
- The thread is initialized in the blocked state, then unblocked just before returning, which allows the new thread to be scheduled.
Type: 
```c
void thread_func (void *aux)
```
This is the type of the function passed to `thread_create()`, whose aux argument is passed along as the function's argument.

Function: void **thread_block** (void)

Transitions the running thread from the running state to the blocked state (see [Thread States](https://thierrysans.me/CSCC69/projects/WWW/pintos_6.html#Thread%20States)). The thread will not run again until `thread_unblock()` is called on it, so you'd better have some way arranged for that to happen. Because `thread_block()` is so low-level, you should prefer to use one of the synchronization primitives instead (see section [A.3 Synchronization](https://thierrysans.me/CSCC69/projects/WWW/pintos_6.html#SEC100)).

Function: void **thread_unblock** (struct thread *thread)

Transitions thread, which must be in the blocked state, to the ready state, allowing it to resume running (see [Thread States](https://thierrysans.me/CSCC69/projects/WWW/pintos_6.html#Thread%20States)). This is called when the event that the thread is waiting for occurs, e.g. when the lock that the thread is waiting on becomes available.

Function: struct thread ***thread_current** (void)

Returns the running thread.

Function: tid_t **thread_tid** (void)

Returns the running thread's thread id. Equivalent to `thread_current ()->tid`.

Function: const char ***thread_name** (void)

Returns the running thread's name. Equivalent to `thread_current ()->name`.

Function: void **thread_exit** (void) `NO_RETURN`

Causes the current thread to exit. Never returns, hence `NO_RETURN` (see section [E.3 Function and Parameter Attributes](https://thierrysans.me/CSCC69/projects/WWW/pintos_10.html#SEC148)).

Function: void **thread_yield** (void)

Yields the CPU to the scheduler, which picks a new thread to run. The new thread might be the current thread, so you can't depend on this function to keep this thread from running for any particular length of time.

Function: void **thread_foreach** (thread_action_func *action, void *aux)

Iterates over all threads t and invokes `action(t, aux)` on each. action must refer to a function that matches the signature given by `thread_action_func()`:

Type: **void thread_action_func (struct thread *thread, void *aux)**

Performs some action on a thread, given aux.

```c
int thread_get_priority (void)
```
```c
void thread_set_priority (int new_priority)
```
set and get thread priority.