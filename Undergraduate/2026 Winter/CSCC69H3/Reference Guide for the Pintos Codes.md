# Loader

# Synchronization
## Disabling Interrupts
The crudest way to do synchronization.
If interrupts are off, no other thread will preempt (forestall) the running thread.
Pintos is a preemptible kernel, meaning that the kernel threads can be preempted at any time.
The main reason to disable interrupts is to synchronize kernel threads with external interrupt handlers
### Types
```c
enum intr_level
```
One of INTR_OFF or INTR_ON
denotes that intrrupts are disabled or enabled
### Functions
```c
enum intr_level intr_get_level(void)
```
Returns the current interrupt state.

```c
enum intr_level intr_set_level(enum intr_level level)
```
Turns interrupts on or off according to *level* and returns the previous interrupt state.

```c
enum intr_level intr_enable(void)
```
Turns interrupts on and returns the previous interrupt state.

```c
enum intr_level intr_disable(void)
```
Turns interrupts off and returns the previous interrupt state.
## Semaphores
Non-negative integer together with two operators that manipulate it atomically
* "Down" or "P": Wait for the value to become positive, then decrement it.
* "Up" or "V": Increment the value (and wake up one waiting thread, if any).
### Types
```c
struct semaphore
```
Represents a semaphore
### Functions
```c
void sema_init(struct semaphore *sema, unsigned value)
```
Initializes *sema* as a new semaphore with the given initial value.

```c
void sema_down (struct semaphore *sema)
```
Executes the "down" or "P" operation on *sema*, waiting for its value to become positive and then decrementing it by one.

```c
void sema_try_down(struct semaphore *sema)
```
* Tries to execute the "down" or "P" operation on *sema*, without waiting.
* Returns true if *sema* was successfully decremented, or false if it was already zero and thus could not be decremented without waiting.
* (Calling this function in a tight loop wastes CPU time, so use *sema_down()* or find a different approach instead.)

```c
void sema_up(struct semaphore *sema)
```
* Executes the "up" or "V" operation on *sema*, incrementing its value. If any threads are waiting on *sema*, wakes one of them up.
* *sema_up()* may be called inside an external interrupt handler.
## Locks
### Types
### Functions
```c
void lock_init(struct lock *lock)
```
Initializes *lock* as a new lock. The lock is not initially owned by any thread.

```c
void lock_acquire(struct lock *lock)
```

