# Rigidbody

**Inherits from ScriptBehaviour**

**Is added to an object in order to work**:
```cpp
object->AddScript<Rigidbody>();
```


The Rigidbody class/struct is a Physics-related script. When applied to a model, it becomes affected by gravity. Although to be able to detect collisions, you need to apply a type of collider. For example: a **BoxCollider**.

## Functions:

### Transform& GetRigidbodyTransform()

**Returns**: The Rigidbody's Transform, containing position, rotation and scale of the body affected to physics.

This function is used to move the object while its being affected by physics, for example, teleporting to another location while not affecting its momentum.

This is useful because the moment the Rigidbody class is applied, it takes control over the GetTransform() function, so if you want to change one of the axis while they're being constantly changed, you can use this function.

**Short Example**:

```cpp
... // Top code
Vector3 move = Vector3(1, 0, 0) // Move one to the right.
rigidbody->GetRigidbodyTransform().position = move;
... // Bottom code
```

### void SetVelocity(Vector3 add)

**Requires**: One Vector3.

This function sets the velocity of the Rigidbody.

This can be used to change or stop the momentum of the current body that you're trying to control, and can be used for character movement, along other stuff.

**Short Example**:

```cpp
... // Top code
if(Input::GetKey(GLFW_KEY_D)) // Check if "D" is pressed.
{
	rigidbody->SetVelocity(Vector3(16 * Graphics::DeltaTime, 0, 0)); // Move to the right.
}
... // Bottom code
```

### Vector3 GetVelocity()

**Returns**: The current velocity of the Rigidbody.

This is used to get the velocity of a Rigidbody, and can be used to print it for statistics, check for a certain speed limit, and more.

**Short Example**:

```cpp
... // Top code

// Let's print the current speed of the body.
std::cout << rigidbody->GetVelocity().ToString() << std::endl;

... // Bottom code
```

## Variables:

### bool freezePositionX

If true, the Rigidbody is going to stop changing the X position coordinate.

**Short Example**:

```cpp
... // Top code

// Can't change the X position via GetTransform() :(.
rigidbody->GetTransform().position = Vector3(1, 0, 0);

// Let's freeze the X position.
rigidbody->freezePositionX = true;

// Now we can change it via GetTransform() :D.
rigidbody->GetTransform().position = Vector3(1, 0, 0);

... // Bottom code
```

### bool freezePositionY

If true, the Rigidbody is going to stop changing the Y position coordinate.

**Short Example**:

```cpp
... // Top code

// I want the object to stop falling.
rigidbody->freezePositionY = true;

// Now it stopped :D

... // Bottom code
```

### bool freezePositionZ

If true, the Rigidbody is going to stop changing the Z position coordinate.

This is usually used to make the collisions and overall physics of the body "2D only".

**Short Example**:

```cpp
... // Top code

// I want the collisions of this body to only be 2D.
rigidbody->freezePositionZ = true;

// Now the physics are not going to be affected in a 3D space.

... // Bottom code
```