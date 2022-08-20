# The Rigidbody

Welcome to the second chapter of this physics tutorial!

In this section, we're going to introduce **dynamic objects**. Objects that are affected by gravity, by force and other elements in the physics world.

The component that turns a static object into a dynamic one is known as the [**Rigidbody**](/api/Physics/Rigidbody.md).

## What is the Rigidbody?

A Rigidbody is a ScriptBehaviour component that adds the concept of gravity and force into any collider.

By combining a Collider component with the Rigidbody, you can turn any model into a dynamic prop.

It's pretty much easy and straight-forward, but the good thing about this component is that you can manipulate it via code.

You can set the velocity, apply forces and much more. Which can be used to make a controllable platformer character that can interact with static collisions around it, like walking on top of them, using it to jump from one platform to another and the list goes on...