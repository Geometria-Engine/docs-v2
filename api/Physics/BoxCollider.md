# BoxCollider

**Inherits from ScriptBehaviour**

**Is added to an object in order to work**:
```cpp
object->AddScript<BoxCollider>();
```

The Box Collider is a component that is added to an object. Once added, an invisible box is going to be attached to it, making the object have the collisions of a box. If you want this body to be affected by gravity, i would recommend checking out the [**Rigidbody**](/api/Physics/Rigidbody.md) struct.

This can be used for collision detection and used for triggers, like adding collisions to a player, static structure, a floor, or use it as a trigger to check if an object has passed in front of it.

## Functions:

### void SetScale(Vector3 size)

**Requires**: One Vector3.

This function is used to set the scale or size of the box collider, mostly used from situations like changing the player's collision size while chrowching or handling a complex set of collisions, to just simple scaling.

**Short Example**:

```cpp
... // Top code

// I want to shrink the size of the collision when i press F.
if(Input::GetKey(GLFW_KEY_F))
{
	boxCollider->SetScale(Vector3(1, 0.5, 1));
}

... // Bottom code
```

### void SetTrigger(bool t)

**Requires**: One boolean.

This turns the collision into a trigger. If the boolean is "true", it will automatically disable gravity and just focus on checking if the trigger has an object inside of it.

Objects don't collide with the trigger, so every checked object can pass through it without any issues.

**Short Example**:

```cpp
... // Top code

// Let's turn the collision into a trigger.
boxCollider->SetTrigger(true);

... // Bottom code
```