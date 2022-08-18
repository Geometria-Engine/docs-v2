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
if(PhysicsManager::ScreenCameraRaycast(*Graphics::MainCamera(), Vector2(Graphics::GetMainWindow().Mouse.X, Graphics::GetMainWindow().Mouse.Y), 1000))
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
PhysicsManager::ScreenCameraRaycast(*Graphics::MainCamera(), Vector2(Graphics::GetMainWindow().Mouse.X, Graphics::GetMainWindow().Mouse.Y), 1000, buff)

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

This can be used for a Jump mechanic, to prevent checking the player and accidentally mistaking it with the ground.

**Short Example**:

```cpp
... // Top code

// Let's do a raycast to check the floor, and save that data to the buffer.
// Our player is a 1x1 square, so let's set the origin close to the center of its body.
RaycastBuffer buff;
PhysicsManager::Raycast(Vector3(GetTransform().position.x, GetTransform().position.y - 0.55f, GetTransform().position.z), Vector3::down(), 0.01, buff);

// Let's get the player's collision box and check it.
if(buff.HittedAnythingExcept(GetScript<BoxCollider>()))
{
	std::cout << "The player can now jump :D" << std::endl;
}

... // Bottom code
```

### bool HittedAnything()

**Returns**: One boolean.

This function is like the last one, but checks if anything hitted, regardless of the object.

**Short Example**:

```cpp
... // Top code

// Let's do mouse picking and check if we clicked a collider.
RaycastBuffer buff;
PhysicsManager::ScreenCameraRaycast(*Graphics::MainCamera(), Vector2(Graphics::GetMainWindow().Mouse.X, Graphics::GetMainWindow().Mouse.Y), 1000, buff)

if(buff.HittedAnything())
{
	std::cout << "Hit!" << std::endl;
}

... // Bottom code
```

### Vector3 GetPoint(float p)

**Requires**: One float.
**Returns**: One Vector3.

With this function, you can get a point in the raycast.

If we launch a ray with a distance of 1000, and we want to get the position of it, but in the middle (in the length 500), we use this function to get that result.

**Short Example**:

```cpp
... // Top code

// Let's do mouse picking, and get the ray's position in the length 10.
RaycastBuffer buff;
PhysicsManager::ScreenCameraRaycast(*Graphics::MainCamera(), Vector2(Graphics::GetMainWindow().Mouse.X, Graphics::GetMainWindow().Mouse.Y), 1000, buff)

std::cout << buff.GetPoint(10).ToString() << std::endl;

... // Bottom code
```

## Variables:

### Vector3 origin

Gets/Sets the origin of the raycast.

**Short Example**:

```cpp
... // Top code

// Let's do mouse picking...
RaycastBuffer buff;
PhysicsManager::ScreenCameraRaycast(*Graphics::MainCamera(), Vector2(Graphics::GetMainWindow().Mouse.X, Graphics::GetMainWindow().Mouse.Y), 1000, buff)

... // Some code...

// Oh no! There's too much code! I forgot the origin of the ray!

// Eh... I'll just print the origin from the RaycastBuffer...

std::cout << buff.origin.ToString() << std::endl;

... // Bottom code
```

### Vector3 end

Gets/Sets the end of the raycast.

**Short Example**:

```cpp
... // Top code

// Let's do mouse picking...
RaycastBuffer buff;
PhysicsManager::ScreenCameraRaycast(*Graphics::MainCamera(), Vector2(Graphics::GetMainWindow().Mouse.X, Graphics::GetMainWindow().Mouse.Y), 1000, buff)

// Let's get the end of the Ray and save it in a Vector3 for later.

Vector3 getEndRay = buff.end;

... // Bottom code
```

### Vector3 direction

Gets/Sets the direction of the raycast.

**Short Example**:

```cpp
... // Top code

// Let's do mouse picking...
RaycastBuffer buff;
PhysicsManager::ScreenCameraRaycast(*Graphics::MainCamera(), Vector2(Graphics::GetMainWindow().Mouse.X, Graphics::GetMainWindow().Mouse.Y), 1000, buff)

// I want to know the direction of the Raycast, since i don't have that kind of information and don't have time to accurately calculate it.

std::cout << buff.direction.ToString() << std::endl;

... // Bottom code
```

### std::vector<ScriptBehaviour* > hitScripts

Gets/Sets the amount of objects the raycast hitted.

**Short Example**:

```cpp
... // Top code

// Let's do mouse picking...
RaycastBuffer buff;
PhysicsManager::ScreenCameraRaycast(*Graphics::MainCamera(), Vector2(Graphics::GetMainWindow().Mouse.X, Graphics::GetMainWindow().Mouse.Y), 1000, buff)

// I want to know how many objects have the "EnemyAI" script
// that i recently created for my game.
for(auto i : buff.hitScripts)
{
	if(i->GetScript<EnemyAI>() != nullptr)
		std::cout << "Found an Enemy!" << std::endl;
}

... // Bottom code
```