# Fall Hard. Fall Fast
Or, how to know what the heck went wrong. 
Ever been told to 'Nip it in the bud'? The old addage applies to programming as well. 

> "It is better for a function to fail immediately and predictably when passed bad values than to begin executing and fail later with an error message that is likely to be unclear" -Definitive Guide to Javascript

example of try catch.... 


example of error class. What is it??
```javascript
throw new Error ('what had happened was...')
```

move into asynchronous implementation...

The good ol' Try/ Catch doesnt work as well in node.js. Why? Because of the nature of node as a nonblocking, asynchronous thing and event queues. Remember our talk about stacks and queues? (insert link) How about closures? (insert link yet to be made)
These both come into play. (insert lots of explaining Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation)

### A New Era 
(A New Error, get it?)

Enter callback functions.

Why do we use them? What do they do?

Structure of a callback:
Callback functions always have at least one parameter: the success or failure of the last operation, then other things. 
Err can become null or an instance of the error class.

The node way.

Lead into Testing/TDD teaser for future post on predictable failures.
