# Introduction to Physics.

Welcome to the second tutorial of the engine's documentation!

In here you're going to learn about physics, and at the final chapter you're gonna be able to make your first "platformer character movement"!

But first, let's take a closer look at the basics and start slowly before jumping to the end. Don't worry! This will be pretty straight-forward like the "Hello World" tutorial!

## Introducing the components.

When it comes to Physics, we have **two key components** that are extremely useful, the [**Rigidbody**](/api/Physics/Rigidbody.md) and the **Collisions**.

The most basic one of them all is the [**BoxCollider**](/api/Physics/BoxCollider.md), so let's start from there.

## What is the Box Collider?

The Box Collider is basically an invisible box that is going to be used for overall collisions. If you play a lot of games, you're gonna see sometimes some furtniture or a player that has something similar, this is because of two reasons:

- First, its the most basic shape of them all.
- Second, because of the first reason, its much easier to compute in the background.

Let me demonstrate in detail, with basic drawings!

Let's imagine the basic scene with a square, like in the previous tutorials.

![Box Collider Demonstration 1](./resources/box-collider-1.png)

And as a game developer, i want this to be interactable with the physics world. That's where the Box Collider (or any kind of collider) comes into play.

By adding this component, the model becomes part of the physics world.

*(The Green Lines showed in there are actually invisible, its just to give a representation of the physical object's shape)*

![Box Collider Demonstration 2](./resources/box-collider-2.png)

Now, this object can interact with anything related to physics, like objects falling from the sky, bullets shooting straight to it, objects being on top of it, etcetera.

Since it doesn't have anything other than the Box Collider, this becomes a static model in this physics world, so it can make different roles such as:

- An immovable object.
- A floor.
- Simple furniture like a little table.
- And more stuff!

For example, if we have two objects, one being a table, and the other one being a flower inside a vase. Both objects being internally, models with a texture on them.

![Box Collider Demonstration 3](./resources/box-collider-3.png)

If we want to get them into the physical world as static objects, we simply create two Box Collider scripts, one for each object!

![Box Collider Demonstration 4](./resources/box-collider-4.png)

Now that i told you all of this.

## Let's put it to the test...