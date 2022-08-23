# Introducing Triggers

Welcome to a new chapter of the Physics tutorial!

This time, we're going to take a look at **Triggers**!

You *might* be asking yourself...

## What is a Trigger?

Well, a Trigger is basically a collision, which only goal is to check if other collisions are inside it.

**Other collisions can't collide with it, they only go through it**, meaning that can't act as something like a wall or a floor.

***But...*** it can act as an invisible activator, like an invisible cube that opens a door, or something that activates a trap!

## Let's see a situation in form of a comic!

**This is "Bob", say hi to Bob! :D**. **Bob** needs to go through the door, because he needs to go to work:

![Triggers Comic 1](./resources/triggers-comic-1.png)

Bob, walks to the door...

![Triggers Comic 2](./resources/triggers-comic-2.png)

When all of the sudden... **A BIG TRAP IS ACTIVATED! 20 TONS OF STEEL COMING STRAIGHT TO BOB'S BODY!!!**

**LOOK OUT BOB!**

![Triggers Comic 3](./resources/triggers-comic-3.png)

![Triggers Comic 4](./resources/triggers-comic-4.png)

***Phew...*** that was a close one!

Thank god Bob is safe :)

## But what caused this situation to happen?

Well, let's go back to the 1st panel and make all collisions visible:

![Triggers Explanation 1](./resources/trigger-explanation-1.png)

**A-ha!** There was an invisible trigger in there!

So when Bob walked to the middle, he activated it causing it to make a trap fall!

![Triggers Explanation 2](./resources/trigger-explanation-2.png)

**So this is basically the power of triggers, showed visually!**

You can use this method to activate or execute anything you want by just checking for a collision!

So, now that we went through this...

## Let's get back to coding!