# Physics in Geometria

## Welcome to the second tutorial of Geometria!

Now, we're gonna learn how to add physics to your game!

Physics reside on mainly **two** built-in scripts, that you can directly import in your `GameMain.h` by typing in `#include "geometria/physics.h"` before the `struct GameMain`, called `BoxCollider` and `Rigidbody`.

The first one, `BoxCollider`, is self-explanatory. It defines a box hitbox around your model. Every model that needs an hitbox *needs* this script.<br/>
To demonstrate how this works, we need to introduce another script, `Rigidbody`.<br/>
`Rigidbody` will basically add gravity to the object it is attached to. It needs a BoxCollider to properly function, otherwise your model would just fall through the ground.

## So, we have two new scripts to use, how do we use them?
First up, let's bring back our project from [our previous tutorial](/hello-world/hello-world.md), which may look something like this:

```text
.
├── Game
|	├── GameMain.h
|   ├── SquareScript.h
|   ├── SquareScript.cpp (optional)
|	├── billy.png
|	└── ...
└── ...
```

Open the `GameMain.h`, and like mentioned a bit more above, add `#include "geometria/physics.h"` below the include of geometria and your ScriptBehaviour.<br/>
And now, before adding the `SquareScript`, add two lines like this: <br/>
```cpp
        ...
        model->AddScript<BoxCollider>();
        model->AddScript<Rigidbody>();
        ...
```
<br/>
These two lines will add the needed scripts for physics to work on our good ol' friend Billy. Let's compile and see what happens.

> [!TIP|style:flat|label:REMINDER]
> To compile your project, open your local command prompt in the root folder of your project, and type `geo --compile` (or, if using powershell, `.\geo.exe --compile`)

![Billy is gone :'(](./resources/no-more-billy.png)

## Where did Billy go? :(

Fairly simple, he's falling, far out of reach for us to find out where he is... Let's fix that!<br/>
To do that, we need to add another object to the scene, let's add a rectangle for example!<br/>
```cpp
        ... // Above is the Billy initialisation

        //Platform setup
        Model* platform = new Model(Model::Primitives::SQUARE, Vector3(0,-1, 0), Vector3(0), Vector3(3,1,1));
        platform->AddScript<BoxCollider>();

        //Add platform to our draw call
        RendererCore::AddModel(*platform, d->Target());
```

Now, if you re-compile the game, you should see our good ol' friend Billy standing on the newly created platform!

![Billy is back! :D](./resources/billy-is-back.png)