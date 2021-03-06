---
layout: post
title:  "Stacks and Queues in Plain Language"
date:   2016-03-17 10:01:36 -0600
categories: post
---
# Now with more talking emoji! Thanks, [jemoji](https://rubygems.org/gems/jemoji)!
  

>:monkey_face: : *Hey, Sam, what's a stack?*

>:alien: : A stack is a limited access data structure where objects can only be inserted and removed from the top. 

>:hear_no_evil: : *Wait. Hold up, whaddoyamean the top? I didn't even know we had a top!*

>:alien: : Uh-huh! That's part of a stack's structure. Here, let's start with the basics... 


A stack is made up of two parts: 

* the "top" 
* the "rest" 

You can interact with it in two* ways: 

* add item to top
* remove item from top.

These methods and properties are what make it a limited access data structure. Our interaction with the structure is only with the top-most element, we never interact with the 'rest.' One often used analogy is a stack of books or plates because you can remove and add only from the top. But I grab plates and books from the middle all the time. *Rebellion! Favorites!* A more relatable example would be books on your desk **in the dark.** Let's say you're on you're way out the door in a hurry. You're gonna grab the one on top because it's probably the last one you set there, right? Plus, it's dark so you can't even *see* the rest. Now *that's* a stack. This is why stacks are often explained as Last In First Out. 

But, why on earth would we want to model a data structure after grabbing for books in the dark? You got me. Fear not, I also got you. But first, let's take a look at Queues.

A queue is made of two parts:

* front
* back

You can interact with it in two ways: 

* insert an item into the back
* remove the front item

We call these methods enqueue and dequeue, respectively. Sounding familiar yet? No? What about a ticket line at a theater? It's first come, first served. Or as a queue would say, First In First Out. The difference between stacks and queues is in removing. In a stack we remove the most recently added item; in a queue, we remove the item that's been there the longest. 

Do you feel pretty comfortable with the concept of a queue? You might. It's part of our social structure. We've found it to be a pretty efficient, systematic way to organize ourselves and our social processes. And, as a friend recently told me, "the more we've encountered something that can be modeled with a structure, the more familiar the structure will feel." 

A few examples:

* That back button on your browser? Stack. The undo button? Same.
* Playing Rummy. That discard pile? Totally a stack.
* Boarding an airplane? Queue.
* Shipping containers on a boat? Boxes under your bed? Stacks.


>:monkey_face: : *How about cartons of milk in the fridge?*

>:alien: : Should be a queue. 

>:monkey_face: : Why? 

>:alien: : You finish the oldest one first or toss it out if it's expired. When you bring new milk home you put the newest ones in the back. If your fridge is operated like a stack, you're doing it wrong.

>:speak_no_evil: : ...


>:monkey_face: : Line at the department store? That's a queue, right? 

>:alien: : You got it, but what if there's an erratic customer? Then it's a **priority queue** and their request is elevated while the rest of the queue waits.Customer service, you are *so* backwards.

Back to stacks. I told you not to fear. Why on earth would we want to model a data structure last in first out? It's not all grabbing books in the dark. Computers are really good with stacks. Why? Because of *processes*. Stacks are a well-suited data structure for picking up where you left off. 

Stacks are like books and plates, right? Ever set a dinner plate on top of a book you were reading? Of course not. You're civilized. But *if you did*, when you finished eating and removed your plate you could pick right back up reading where you left off. Cue the Call Stack! The call stack, or execution stack, keeps track of the point to which each active subroutine should *return control* when it finishes executing. Right back on top. This is great for backtracking, recursion, nested function calls, and many other proccesses we ask of our computers. After eating remove the plate and finish reading. After reading, remove the book and find a half-finished drawing underneath. After coloring, remove the paper and find a newspaper underneath. And on and on. Your desk has now become a limited access data structure where objects can only be inserted and removed from the top. Check it:

```javascript
var x = 1 + 4 + 5 
// Evaluate this arithmatic expression 
// before assigning it to x
```

>:alien: : That's the call stack in action. 

>:monkey_face: : :bulb:

>:alien: : *Plus, pallindromes and stacks... totally best friends.* 

>:monkey_face: : Hey, Sam. All of these examples are existing structures, some with physical limitations. How do you know when to use stacks or queues **in** your software? 

>:alien: : If you need stack, you know it. Otherwise use a queue. 

>:monkey_face::grey_question: ...

There are many factors to consider when creating or implementing a data structure. Stacks and queues are structures that help you deal with things coming at you at a faster speed than you can process them. Like with milk or your email, the significance of an expiration date or expected response time might change how we process our data. For example, if a new coffee house implemented their morning line as a stack that wouldn't go over too well, would it? No. People have limited patience. 

With a project, maybe you turn one thing into three more. Or maybe the user is click-click-clicking and now there's a line of tasks to complete. Like at the theater, if you just need a place to put everyone because they are coming faster than you can sell tickets, use a queue.

*If for some reason processing items in the same order is not what you want, use a stack.*

This might be because in order to finish dealing with your current problem, you first need to take care of something else. Or you might need a return value from a newer task to complete the previous one - like the energy from dinner, a response from a newer email, or an evaluation of an expression. These are all good signifiers that you'll want to use a stack. 

>:monkey_face: :  **If I need stack, I'll know it. Otherwise use a queue.**
