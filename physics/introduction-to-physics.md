# Introduction to Physics.

Welcome to the second tutorial of the engine's documentation!

In here you're going to learn about physics, and at the final chapter you're gonna be able to make your first "platformer character movement"!

But first, let's take a closer look at the basics and start slowly before jumping to the end. Don't worry! This will be pretty straight-forward like the "Hello World" tutorial!

# Introducing the components.

When it comes to Physics, we have **two key components** that are extremely useful, the [**Rigidbody**](/api/Physics/Rigidbody.md) and the **Collisions**.

The most basic one of them all is the [**BoxCollider**](/api/Physics/BoxCollider.md), so let's start from there.

# What is the Box Collider?

The Box Collider is basically an invisible box that is going to be used for overall collisions. If you play a lot of games, you're gonna see sometimes some furtniture or a player that has something similar, this is because of two reasons:

- First, its the most basic shape of them all.
- Second, because of the first reason, its much easier to compute in the background.

Let me demonstrate in detail, with basic drawings!

Let's imagine the basic scene with a square, like in the previous tutorials.

![Box Collider Demonstration 1](./resources/box-collider-1.png)

And as a game developer, we want this to be interactable with the physics world. That's where the Box Collider (or any kind of collider) comes into play.

By adding this component, the model becomes part of the physics world.

*(The Green Lines showed in there are actually invisible, its just to give a representation of the physical object's shape)*

![Box Collider Demonstration 1](./resources/box-collider-2.png)