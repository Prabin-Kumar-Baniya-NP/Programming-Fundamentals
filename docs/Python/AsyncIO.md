# AsyncIO

- Parallelism consists of performing multiple operations at the same time. [Multiprocessing]

- In concurrency, multiple tasks have the ability to run in an overlapping manner. [Threading, AsyncIO]

## Coroutine

- A coroutine is a function that can suspend its execution before reaching return, and it can indirectly pass control to another coroutine for some time.

- Coroutines are defined using the async def keyword, and they are executed using an event loop, which manages the scheduling of coroutines and I/O operations.

- A function that you introduce with async def is a coroutine. It may use await, return, or yield, but all of these are optional.

- Using await will schedule a coroutine for execution in event loop.

- A key feature of coroutines is that they can be chained together.

- Coroutines don’t do much on their own until they are tied to the event loop.

- By default, an async IO event loop runs in a single thread and on a single CPU core. Usually, running one single-threaded event loop in one CPU core is more than sufficient. It is also possible to run event loops across multiple cores.

- Event loops are pluggable. That is, you could, if you really wanted, write your own event loop implementation and have it run tasks just the same.

```python
import asyncio

async def count():
    print("One")
    await asyncio.sleep(1)
    print("Two")

async def main():
    await asyncio.gather(count(), count(), count())

asyncio.run(main())
```

```
One
One
One
Two
Two
Two
```

## Event Loop

- Event loop is responsible for managing the scheduling and execution of asynchronous code.

- Coroutines are defined using the async def keyword, and they can be scheduled for execution using the await keyword. When a coroutine is scheduled for execution, it is added to the event loop's task queue.

- The event loop continuously monitors the task queue, and when a coroutine becomes ready to run (i.e., it has no pending I/O operations or other blocking tasks), it is removed from the task queue and executed.

### Example

```python
import aiohttp
import asyncio

async def fetch_data():
    async with aiohttp.ClientSession() as session:
        async with session.get('https://jsonplaceholder.typicode.com/posts/') as response:
            data = await response.json()
            return data

async def main():
    data = await fetch_data()
    print(data)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```

## Task

- In Python's asyncio library, asyncio.create_task() is a function that can be used to create a Task object from a coroutine. - A Task is an object that represents a coroutine that has been scheduled to run on the event loop.
- asyncio.create_task() is useful when you need to schedule a coroutine to run on the event loop, but you don't want to wait for it to complete before continuing with other tasks. Instead, you can create a Task object for the coroutine and allow it to run in the background while you continue with other tasks.

```python
import asyncio

async def coroutine():
    # some asynchronous task
    pass

async def main():
    task = asyncio.create_task(coroutine())
    await task

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```

## Async IO Gather

- asyncio.gather() is a method in the Python asyncio library that allows you to execute multiple coroutines concurrently and await their results.
- It takes one or more coroutines as input and returns a future object that represents the combined result of all the coroutines.

- The asyncio.gather() method can take any number of coroutines as input, and it will execute them concurrently, returning the results in the order in which the coroutines were passed to it. This can be useful when you need to execute multiple asynchronous tasks and wait for all of them to complete before continuing.

```python
import asyncio

async def coroutine_1():
    # some asynchronous task
    pass

async def coroutine_2():
    # some other asynchronous task
    pass

async def main():
    results = await asyncio.gather(coroutine_1(), coroutine_2())
    print(results)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())

```
