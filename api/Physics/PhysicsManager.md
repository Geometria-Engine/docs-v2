# PhysicsManager

**Inherits from ScriptBehaviour.**

**Is a Global Manager**

The Physics Manager is the global manager that keeps the physics alive, and can be used to either set up different configurations of it, checking and doing raycasting and mouse picking, etc.

This is the heart of the entire Physics API, and the moment you add anything that is related to it, this will boot up instantly.

## Functions:

### void SetGravity(Vector3 g)

**Requires**: One Vector3.

This function allows you to change the global gravity of the game's current scene. This can be used to apply moon gravity to the whole scene, change the gravity's axis, and more.

By default, the gravity is set to ```Vector3(0, -9.81, 0)```, which is almost the same gravity the Earth currently has.

**Short Example**:

```cpp
... // Top code

// Change to Moon gravity.
PhysicsManager::SetGravity(Vector3(0, -1.62, 0));

... // Bottom code
```

### bool Raycast(Vector3 origin, Vector3 direction, int maxDistance)

**Requires**: Two Vector3s and one integer.
**Returns**: One boolean.

#### What is a Raycast?

A Raycast is basically an invisible beam/lazer that travels across in a specific direction, with a maximum distance that can be from 0 to Infinity.

This can be used for checking what objects collided with this beam, like a bullet checking how many objects it hit from a specific point, for example.

**Short Example**:

```cpp
... // Top code

// Check from the center of the world if we hit something.
// This Raycast will face to the front, up to a maximum distance of 1000.
if(PhysicsManager::Raycast(Vector3(0, 0, 0), Vector3::front(), 1000))
{
	std::cout << "We hitted something!" << std::endl;
}

... // Bottom code
```

### bool Raycast(Vector3 origin, Vector3 direction, int maxDistance, RaycastBuffer& buffer)

**Requires**: Two Vector3s, one integer and one RaycastBuffer.
**Returns**: One boolean.

The same as before, but we store the data into a RaycastBuffer for further analysis.

**Short Example**:

```cpp
... // Top code

// Check from the center of the world if we hit something.
// This Raycast will face to the front, up to a maximum distance of 1000.
// All of this data is going to be saved in a RaycastBuffer for more
// extended analysis.
RaycastBuffer buff;
PhysicsManager::Raycast(Vector3(0, 0, 0), Vector3::front(), 1000, buff)

// Let's supposed that we have a reference of a BoxCollider
// that we've got via "someObject->GetScript<BoxCollider>()".
// We can use this to check if it hitted everything
// except for that particular box.
if(buff.HittedAnythingExcept(someBoxCollider))
{
	std::cout << "Hit!" << std::endl;
}

... // Bottom code
```

### bool ScreenCameraRaycast(Camera& cam, Vector2 point, int maxDistance)

**Requires**: One Camera, one Vector2 and one integer.
**Returns**: One boolean.

The same as a Raycast, but the point of origin is a camera and the direction is set by coordinates of your screen, with a maximum distance that can be from 0 to Infinity.

Used frequently for picking objects with a mouse, along other things.

**Short Example**:

```cpp
... // Top code

// Check from a point of the screen if we hit something
// with a maximum distance of 1000.
if(PhysicsManager::Raycast(*Graphics::MainCamera(), Vector2(Graphics::GetMainWindow().Mouse.X, Graphics::GetMainWindow().Mouse.Y), 1000))
{
	std::cout << "We hitted something!" << std::endl;
}

... // Bottom code
```

### bool ScreenCameraRaycast(Camera& cam, Vector2 point, int maxDistance, RaycastBuffer& buff)

**Requires**: One Camera, one Vector2, one integer and one RaycastBuffer.
**Returns**: One boolean.

The same as before, but we store the data into a RaycastBuffer for further analysis.

```cpp
... // Top code

// Check from a point of the screen if we hit something
// with a maximum distance of 1000.
// All of this data is going to be saved in a RaycastBuffer for more
// extended analysis.
RaycastBuffer buff;
PhysicsManager::Raycast(*Graphics::MainCamera(), Vector2(Graphics::GetMainWindow().Mouse.X, Graphics::GetMainWindow().Mouse.Y), 1000, buff)

// Let's supposed that we have a reference of a BoxCollider
// that we've got via "someObject->GetScript<BoxCollider>()".
// We can use this to check if it hitted everything
// except for that particular box.
if(buff.HittedAnythingExcept(someBoxCollider))
{
	std::cout << "Hit!" << std::endl;
}

... // Bottom code
```

# RaycastBuffer

The RaycastBuffer is an object that stores an extensive amount of data about a Raycast.

This can be used for extensive analysis, like checking what kind of objects it hit, if it hit one specific object or a group of objects, etc.

## Functions:

### bool HittedAnythingExcept(ScriptBehaviour* s)

**Requires**: One ScriptBehaviour.
**Returns**: One boolean.

This function is used to check if anything has collided with the stored Raycast except for a specific object.