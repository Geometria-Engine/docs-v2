# Introducing Triggers

Welcome to a new chapter of the Physics tutorial!

This time, we're going to take a look at **Triggers**!

You *might* be asking yourself...

## What is a Trigger?

Well, a Trigger is basically a collision, which only goal is to check if other collisions are inside it.

**Other collisions can't collide with it, they only go through it**, meaning that can't act as something like a wall or a floor.

***But...*** it can act as an invisible activator, like an invisible cube that opens a door, or something that activates a trap!

## Let's see a situation in form of a comic!

**This is "Bob", say hi to Bob! :D**. **Bob** needs to go through the door, because he needs to go to work:

![Triggers Comic 1](./resources/triggers-comic-1.png)

Bob, walks to the door...

![Triggers Comic 2](./resources/triggers-comic-2.png)

When all of the sudden... **A BIG TRAP IS ACTIVATED! 20 TONS OF STEEL COMING STRAIGHT TO BOB'S BODY!!!**

**LOOK OUT BOB!**

![Triggers Comic 3](./resources/triggers-comic-3.png)

![Triggers Comic 4](./resources/triggers-comic-4.png)

***Phew...*** that was a close one!

Thank god Bob is safe :)

## But what caused this situation to happen?

Well, let's go back to the 1st panel and make all collisions visible:

![Triggers Explanation 1](./resources/trigger-explanation-1.png)

**A-ha!** There was an invisible trigger in there!

So when Bob walked to the middle, he activated it causing it to make a trap fall!

![Triggers Explanation 2](./resources/trigger-explanation-2.png)

**So this is basically the power of triggers, showed visually!**

You can use this method to activate or execute anything you want by just checking for a collision!

So, now that we went through this...

## Let's get back to coding!

Go back to the scene we made in the last chapter...

First, let's push both the floor and the rigidbody a bit further, and set the rigidbody's Y position a bit higher:

```cpp
Model* floor = new Model(Model::Primitives::SQUARE, Vector3(0, -2, -10), Vector3(0), Vector3(5, 2, 1));
Model* rigidBody = new Model(Model::Primitives::SQUARE, Vector3(0, 4, -10), Vector3(0), Vector3(1));
```

And remember in the script we made earlier (*in the last tutorial, it was called the "Player" script*), we need to change the origin aswell:

```cpp
if(rBuffer.HittedAnythingExcept(GetScript<BoxCollider>()))
{
	GetScript<Rigidbody>()->GetRigidbodyTransform().position = Vector3(0, 4, -10);
}
```

Great! Now if we compile and run, the scene is going to have much more space, which is great for our trigger implementation:

![Trigger Code 1](./resources/trigger-code-1.png)

## Now, let's add the Trigger!

To demonstrate it a bit visually, we're going to use a "Model" instead to see where the trigger is going to be:

- First, we add it in the scene and change its initial color to green:

 	```cpp
 	 Model* trigger = new Model(Model::Primitives::SQUARE, Vector3(0, 2, -10.1), Vector3(0), Vector3(5, 2, 1));
	  trigger->color = Color::green();
 	```

- Second, add a Rigidbody and a Box Collider, and use the ```SetTrigger()``` function to change it from a normal collision, to a trigger, this by adding a boolean parameter, which in this case is going to be "true":

 	```cpp
 	 trigger->AddScript<Rigidbody>();
	  BoxCollider* triggerBC = trigger->AddScript<BoxCollider>();
	  triggerBC->SetTrigger(true);
 	```

 	To prevent using the ```GetScript<>()``` and save the engine from having to look for it, we save it in a pointer. But you can do this other implementation, which is much quicker, whatever fits best for you:

 	```cpp
 	 trigger->AddScript<Rigidbody>();
	  trigger->AddScript<BoxCollider>();
	  trigger->GetScript<BoxCollider>()->SetTrigger(true);
 	```

- And finally, for visual purposes, we send the trigger model to our Main Draw Call:

 	```cpp
	 RendererCore::AddModel(*trigger, d->Target());
 	```

### Why do we need to set a Rigidbody if the Trigger is not going to move?

Because Triggers ***HAVE*** to be dynamic in order to work.

Triggers need to constantly look if something touches it/its inside of the trigger, even if it is a Rigidbody or isn't, which is something a static model can't do on its own (*atleast not internally*).

## 1st Result.

If we compile and run it, you're gonna see this scene:

![Trigger Code 2](./resources/trigger-code-2.png)

And if we press "R", you can see that it goes through the trigger successfully!

## But... a wild issue appears!

You can see that if we're inside the Trigger, we can still teleport back up, meaning that **the RaycastBuffer thinks the Trigger is a type of floor**.

**So how do we fix this?**

## Introducing "DiscardTriggers()"

The "DiscardTriggers()" function which is part of the Raycast Buffer, can set if you want to discard all triggers it touches, or not if you want to do further analysis.

In this case, we don't want to check or analyze them, so let's use this function to completely disable trigger detection.

**So let's go to our "Player" script...**

And between the RaycastBuffer object initialization and the Raycast, we add the function.

```cpp
RaycastBuffer rBuffer;
rBuffer.DiscardTriggers(true);
PhysicsManager::Raycast(GetTransform().position, Vector3::down(), 1, rBuffer);
```

This will basically set that instruction before it does the Raycast, if you do this after its not going to take effect unless you launch the Raycast again.

## 2nd Result.

If we compile and run it, you can see clearly that when i press "R" inside the Trigger, its not going to teleport the Rigidbody to the top.

**Problem Solved! YAY! :D**