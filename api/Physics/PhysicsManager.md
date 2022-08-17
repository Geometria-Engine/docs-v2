# PhysicsManager

**Inherits from ScriptBehaviour.**

**Is a Static class, a global manager.**

The Physics Manager is the global manager that keeps the physics alive, and can be used to either set up different configurations of it, checking and doing raycasting and mouse picking, etc.

This is the heart of the entire Physics API, and the moment you add anything that is related to it, this will boot up instantly.

## Functions:

### void SetGravity(Vector3 g)