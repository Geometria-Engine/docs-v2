# Multithreading API

Welcome to the Multithreading API!

This API is mostly used to run functions asynchronously, without interrupting the flow of the main thread. Is used a lot for handling heavy tasks or doing a lot of stuff on other cores of your CPU.

Thanks to this API, a lot of stuff like animations and heavy rendering calculations can run on low-end devices.

# Multithreading

**Is a Global Manager.**

The Multithreading struct/class is basically the heart of this API. It handles the amount of cores and functions you're currently using in the background.

The whole system works like a tree, inside this Multithreading manager you have the **PhysicalCore**s in form of a struct aswell, and inside the physical cores you have the **Thread**s.

## Functions:

### Thread* RunThread(std::function\<void()\> v)

**Requires**: One void function.
**Returns**: One Thread.

This is the basic function to run a function in parallel.

By calling this, its going to execute a specific function you add in the parameter in another core of your CPU.

**Short Example**:

```cpp
... // Top code

// We're inside of GameMain struct in GameMain.h...

// We have two functions:
static void SayHelloWorld()
{
	std::cout << "Hello World!" << std::endl;
}

static void Say(std::string something)
{
	std::cout << something << std::endl;
}

... // More code

static void Init()
{
	// Let's run "SayHelloWorld()" asynchronously, for this we're going to add a lambda.
	Multithreading::RunThread([](){ SayHelloWorld(); });

	// Now let's run "Say()".
	// Because it needs a parameter, we're gonna use std::bind.
	std::string saySmth = "Hello from another thread!";
	Multithreading::RunThread(std::bind(Say, saySmth));
}

... // Bottom code
```

### Thread* RunUpdateThread(std::function\<void()\> v, int milliseconds)

**Requires**: One void function.
**Returns**: One Thread.

The same as RunThread() but with the difference is that this is going to run constantly for each "x" milliseconds *(set via the second parameter)*.

**Short Example**:

```cpp
... // Top code

// We're inside of GameMain struct in GameMain.h...

// We have two functions:
static void SayHelloWorld()
{
	std::cout << "Hello World! (at 200 ms)." << std::endl;
}

static void Say(std::string something)
{
	std::cout << something << std::endl;
}

... // More code

static void Init()
{
	// Let's run "SayHelloWorld()" asynchronously, in a constant rate each 200 milliseconds, again like the last one, we're gonna use a lambda.
	Multithreading::RunUpdateThread([](){ SayHelloWorld(); }, 200);

	// Now let's run "Say()", this time at 60fps.
	// Because it needs a parameter, we're gonna use std::bind.
	std::string saySmth = "Hello from another thread! [at 60FPS ;)]";
	Multithreading::RunUpdateThread(std::bind(Say, saySmth), 16);
}

... // Bottom code
```

# Thread

The Thread struct/class is basically the thread in the form of an object, if you want to manipulate it in the code, you can do this:

```cpp
Thread* t = Multithreading::RunUpdateThread([](){ SayHelloWorld(); }, 16);
```

And you'll keep the thread in form of a pointer for later use.

The Thread type can be used for changing the milliseconds, setting it to a Hybernation State, changing the execution speed, etc.

## Functions:

### void ChangeMilliseconds(int change)

**Requires**: One integer.

This function allows you to change the speed of the thread execution in milliseconds. You can do this while the thread is executing without any problems.

**Short Example**:

```cpp
... // Top code

// In the beginning i summoned this update thread at 60fps, but i want to slow it down later on.
Thread* t = Multithreading::RunUpdateThread([](){ SayHelloWorld(); }, 16);

... // More code

// Now i'll slow down the thread to 200 ms.
t->ChangeMilliseconds(200);

... // Bottom code
```

### void SetHybernationState()

This function sets the Thread to its Hybernation State.

**Short Example**:

```cpp
... // Top code

// I summoned this thread, but at one point
// i would like to put it to sleep so it 
// doesn't use a lot of CPU power.
// I'll wake it up later when i need it.
Thread* t = Multithreading::RunUpdateThread([](){ SayHelloWorld(); }, 16);

... // More code

// Now i'll set it to a Hybernation State.
t->SetHybernationState();

... // Bottom code
```