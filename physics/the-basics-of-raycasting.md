# The Basics of Raycasting.

Welcome to the third chapter of this physics tutorial!

In this episode, we're going to take a look at Raycasting, and how it can be extremely useful for a lot of things not only for physics, but also other interesting stuff such as tools and other stuff.

But first...

## What is Raycasting?

Raycasting is the concept of shooting an invisible ray/lazer/beam, and check if it hits something.

In this engine, that something is for example, a Collider or a Rigidbody, since those are the only ones that can be 

Let me demonstrate visually with drawings:

In this imaginary scene, have a point, and a wall:

![Raycasting Scene 1](./resources/raycasting-1.png)

The point wants to face *this* direction:

![Raycasting Scene 2](./resources/raycasting-2.png)

But the point, wants to know if there's something in there that can collide with its vision:

![Raycasting Scene 3](./resources/raycasting-3.png)

**How do we figure out if its something in the point's way?**

Well, that's what the raycasting is for!

We spawn a raycast and tell it, its origin, the direction is facing (in this case, the point's direction), and the maximum distance that can be from 0 to Infinity:

![Raycasting Scene 4](./resources/raycasting-4.png)

Thanks to this Ray, we can clearly determine that a wall is obstructing the point's view:

![Raycasting Scene 5](./resources/raycasting-5.png)

But you can do more with Raycasting, for instance, with the same example, we can determine if more than one object is hitting the ray:

![Raycasting Scene 6](./resources/raycasting-6.png)

Or what if we want to change the direction of the point instead?:

![Raycasting Scene 7](./resources/raycasting-7.png)

Or, change the distance to a small number so the point's view is limited:

![Raycasting Scene 8](./resources/raycasting-8.png)

**The posibilities are endless!**

So, now that you know all of this...

## Let's go back to coding!