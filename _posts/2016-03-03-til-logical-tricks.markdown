---
layout: post
title:  "TIL: Tricks with Logical Operators"
date:   2016-03-03 10:01:36 -0600
categories: post
---

  &nbsp;  &nbsp;**Today I learned...**

  &nbsp; &nbsp;  &nbsp;  &nbsp;  &nbsp;  &nbsp; **logical operators (&&, &#124; &#124; ) return the _value_ of one of their operands.**



Most often, I've seen logical operators used in conjunction with relational expressions to control the flow of program execution in `if` , `while`, and `for` statements, like so:

```javascript
if ( length > 0 && status === false){
 return somethingCool;
 }
```

Relational operators ( like == , <, and >) test for a given relationship between two values, and return `true` or `false` depending on whether that relationship exists. The AND operator (`&&`) returns `true` if and only if both it's first _and_ it's second operand are `true`. The OR operator (`||`), on the other hand, returns `true` if _one or both_ operands is `true`.  It returns `false` only if both operands are `false`.  


While often used together, this `true`/`false` return dichotomy is passed in through the relational operator and is not actually the prescribed return values of the `&&` and `||` logical operators.
Turns out, logical operators return the _value_ of one of their operands. If these operands are non-boolean values a non-boolean value will be returned. Surprise! But how do logical operators get evaluated if not with booleans? JavaScript utilizes type coercion to evaluate the operands within a boolean context. It considers them either "truthy" or "falsy". If this is unfamiliar, reference this type conversion [refresher](http://www.w3schools.com/js/js_type_conversion.asp). 

Check it:

```javascript
foo = false || true; //returns true
bar = 3 || 5; //returns 3
```

You know what this means? We can use logical operators for conditional variable assignment. Remember, `undefined`'s are falsy, so this is handy for not overwriting existing values.

```javascript
foo = foo || 1; //returns 1 if foo is falsy
```

Or we could even chain them together.

```javascript
var smarty = 0;
var pants = undefined;
var foo = smarty || pants && "bar";
//returns "bar"
```

Or use them to assign a default callback function object when the expected parameter is undefined

```javascript
function guard(item, callback) {
    callback = callback || function(item) { return item;};
    callback(item); 
}
```
But which value can we expect to return from a chain? Let's dig a little deeper; logical operators return their _last touched_ operand. That's either the expression that terminated the evaluation, or the last expression in the evaluation chain. To anticipate and employ this behavior, we must understand how logical evaluation differs between && and ||.

# &&

The && operator begins by evaluating the expression on it's left. It's a test. _Are you truthy or falsy?_ 
If this value is falsy, `&&` stops and returns this value. We don't even consider the value on the right. Why? Because it's value won't change the expression's evaluation. If one is false, the whole thing is false.

```javascript
0 && "bar"; // returns 0
```

However, if the left value is truthy, `&&` returns the value on the right regardless of it's value. Why? Because it's value _is_ the expression's evaluation. It's the deal maker/breaker. At this point, an evaluation isn't needed to know this operand will accurately represent the expression's overall evaluation, we can just send it right along. 
    

```javascript
3 && null; // returns null
```

# OR

The ```||``` also begins evaluation with the expression on it's left. If the value is truthy, it stops and returns. We gathered all the information we needed, the entire expression is now true. If lefty is a falsy value, `||` returns the operand to the right. The value of this operand accurately represents the expression's overall evaluation. 

```javascript
3 || null // returns 3
0 || null || "bar" || undefined; // returns "bar"
```

Here's the kicker. When used to control the flow of program execution, values are coerced to boolean for evaluation and typically* result in the expected flow. (*Looking at you, `String` `"false"`, you trickster!)  That's why the nuances of logical operators have gone unnoticed til now in my code. I hadn't yet thought to take advantage of their `return` values for something more than its "truthiness".

Silly me.

## Inspiration

So what inspired this post? What opened my eyes? A brief 'wtf'-to-"how coooool" moment running into this nifty tidbit from John Resig's [Pretty Date](http://ejohn.org/files/pretty.js "source") for displaying JavaScript dates in human-friendly formats. 

```javascript
  return day_diff == 0 && (
      diff < 60 && "just now" ||
      diff < 120 && "1 minute ago" ||
      diff < 3600 && Math.floor( diff / 60 ) + " minutes ago" ||
      diff < 7200 && "1 hour ago" ||
      diff < 86400 && Math.floor( diff / 3600 ) + " hours ago") ||
    day_diff == 1 && "Yesterday" ||
    day_diff < 7 && day_diff + " days ago" ||
    day_diff < 31 && Math.ceil( day_diff / 7 ) + " weeks ago";
```
 Without understanding all the behaviors of logical operators, this code looks confusing. But with a more complete understanding of the JavaScript language, it's a handsome shorthand for two dozen lines of nested conditional statements with half as many return values. Compare. Enjoy. 

```
if (day_diff == 0){
  if (diff < 60){
    return "just now";
    }
  else if (diff < 120){
    return "1 minute ago";
  }
  else if (diff < 3600){
    return Math.floor( diff / 60 ) + " minutes ago";
  }
  else if (diff < 7200){
    return "1 hour ago";
  }
  else if (diff < 86400){
    return Math.floor( diff / 3600 ) + " hours ago");
  }
}
else if (day_diff == 1){
  return "Yesterday";
} 
else if (day_diff < 7){
  return day_diff + " days ago";
} 
else if (day_diff < 31){
  return Math.ceil( day_diff / 7 ) + " weeks ago";
}
```

Pretty neat, huh? Now we know. 

Thoughts to consider:

- Err on the side of caution when using logical operators to execute conditional code. Similar to `if` or `switch`, some variables and functions may never execute or initialize if type coercion or evaluation chains are misunderstood.

- Consider the question of readibiliy. As with any shorthand, ask if is it safe to assume your readers are familiar with an idiomatic use of logical operators. In some audiences, a longer but more 'spelled out' approach may be more acceptable and accessible.

And remember,

>Despite the somewhat complex way that this operator actually works, it is most commonly used as a simple Boolean algebra operator that works on truthy and falsy values. - JavaScript, The Definitive Guide

---

---
<br>

### TL;DR:
* logical operators return the value of their _last touched_ operand
  * `&&`'s terminate with the first falsy value encountered
  * `||`'s terminate with the first truthy value encountered
  * `||`'s continue evaluating falsy values until they run out of values
* using logical operators to [short-circuit evaluate](https://en.wikipedia.org/wiki/Short-circuit_evaluation) conditions is a common, but alternative approach to statement branching.





