# Velocity Manipulation

Welcome to this next chapter of this incredible Physics tutorial!

This is going to the last section before we bundle up everything we learned into a **little game**! :D

But before jumping straight into it, you must've be asking yourself...

## What is "Velocity Manipulation"?

"Velocity Manipulation" is the concept of controlling the speed of a Physics Object inside the Physics world.

This can be used to control characters or objects and being able to react to physics at the same time.

## Let me show you an example in form of a drawing!

We have a little **Cube** and this **Wall** in a nice dark grey canvas:

![Velocity 1](./resources/velocity-1.png)

In here, our goal is to **SMASH THE WALL** and **destroy it** with the cube:

![Velocity 2](./resources/velocity-2.png)

But there's a problem, we don't have a physical tool like a craine that can help us attach the cube to it and tear down that wall, and we can't build one either:

![Velocity 3](./resources/velocity-3.png)

So how do we do it?

**Well, this is a virtual world, so let's manipulate the velocity of the object!**

By applying a certain speed, we can move it to a certain direction:

![Velocity 4](./resources/velocity-4.png)

And once we execute that function with an **extremely high** speed, it'll push itself so fast that it'll knock down the wall!

![Velocity 5](./resources/velocity-5.png)

This is one example of the many things you can do with Velocity Manipulation!

From pushing objects without a physical mechanism, to bring characters and simulations to life!

Now that you learned the concept of "Velocity Manipulation"...

## Its time to apply this in the code!

Remember the **Player** script we've been using to teleport?

Well, this time, we're going to change the mechanic and manipulate its velocity to make the square **jump**!

But first let's set up something that is going to be important.

## From 3D to 2D Physics.

You may notice sometimes that when we press "R" constantly without any patience the square falls through the floor.

**That is because we're in a 3D World**, so the square is going to move not only in the X and Y axis, but in the Z axis aswell.

So how can we use only the X and Y axis, but not the Z one?

## Introducing the "Freeze Position" booleans!

The "Freeze Position" booleans are variables inside of the [Rigidbody](/api/Physics/Rigidbody.md) that can be used to freeze specific position axises.

For the position there is the ```freezePositionX```, the ```freezePositionY``` and the ```freezePositionZ``` variables.

By default, both of them are set to ```false``` so to prevent the square from moving forwards and backwards in the scene, we're going to set ```freezePositionZ``` to true.

To do that, let's head to GameMain.h and set the Rigidbody's value we mentioned earlier to true:

```cpp
rigidBody->AddScript<Rigidbody>();
rigidBody->GetScript<Rigidbody>()->freezePositionZ = true;
```

This is a quick approach, if you want a more optimized aproach you can store the Rigidbody script inside of a pointer and use it to change the boolean's status:

```cpp
Rigidbody* rBScript = rigidBody->AddScript<Rigidbody>();
rBScript->freezePositionZ = true;
```

Now the Physics of our Rigidbody are going to be affected in the X and Y axis of the position, but not in the Z.

> [!TIP]
> You can now change the Z position with GetTransform() instead of GetRigidbodyTransform() since the Rigidbody stopped having control in that axis :D

Now that we coded this, we can go and code our jump mechanic!

## Let's go to the "Player" script.

Back in "The Basics of Raycasting", the final result of the "OnUpdate()" script probably looks similar to this:

```cpp
... // Top code

RaycastBuffer rBuffer;
PhysicsManager::Raycast(GetTransform().position, Vector3::down(), 1, rBuffer);

if(rBuffer.HitAnythingExcept(GetScript<BoxCollider>()))
{
	rb->GetRigidbodyTransform().position = Vector3(0, 2, -5);
}
... // Bottom code
```

Now, let's change the functionality. Instead of teleporting, we're going to set the Rigidbodies velocity, and for that we're going to use the...

## SetVelocity() function.

```SetVelocity()``` is pretty straight-forward, it a void that is part of the [Rigidbody](/api/Physics/Rigidbody.md) script, that allows you to set the current velocity of it.

Like always, i'm going to show you two ways: the quick approach and the optimized approach.

For the quick approach, you can just use ```GetScript<Rigidbody>()```.

Since we can shoot it at any direction, you set the values in form of a Vector3(), but since i want to only jump in the Y axis, i'll only set that to something like "10":

```cpp
if(rBuffer.HitAnythingExcept(GetScript<BoxCollider>()))
{
	GetScript<Rigidbody>()->SetVelocity(Vector3(0, 10, 0));
}
```

And if you did the optimized apporach in the Raycasting tutorial, you can use the Rigidbody you stored in the pointer to set the velocity:

```cpp
if(rBuffer.HitAnythingExcept(GetScript<BoxCollider>()))
{
	rb->SetVelocity(Vector3(0, 10, 0));
}
```

## Final Result.

If we compile and run it, we're gonna see that if we press "R", the square jumps! :D

![Velocity Result 1](./resources/velocity-result-1.png)

![Velocity Result 2](./resources/velocity-result-2.png)

![Velocity Result 3](./resources/velocity-result-3.png)

## Congratulations!

You learned about Velocity and made your **first Jump mechanic!**, now for the last chapter we're gonna [**Bundle Up Everything**](/physics/bundle-up-everything.md) we've learned so far and do something incredible with it, see you there! :D