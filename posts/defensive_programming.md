# Why being so defensive about programming ?

Programming style is often categorised on the architecture of the code itself but the code style also can differ a lot within the same kind of architecture. Defensive Programming is derivated from the notion that very few things can be trusted when running a program and adding more checks are helping to improve the stability of it.
It's a clear defense against Murphy’s famous law which states that whatever you do, everything will go wrong anyway.
Defensive programming as everything else is not always black or white and the code style can be defensive in some critical parts and have fewer checks in other parts.
Let's stop the theory for now and have a look at some common defensive patterns.

## Null Checks

The most common trait of defensive programming is to add null checks for just about everything.
Here is a small example in Javascript:

```javascript
 if (product
 	 && product.groups
 	 && product.groups.length
 	 && product.groups[0]
 	 && typeof product.groups[0].id === 'number'
 	 && product.groups[0].name) {
 	  // do something with the product group
 	}
```

I'm sure this code looks familiar to you in one way or another ! The conventional wisdom here is basically that we should check everything because it's difficult to know what we expect.

Here are probably some of the things going in your head when you wrote that code:
 - What about if the product is not formed properly ?
 - What about if the group on the product does not exist ?
 - How the code will behave if another kind of object is passed ? (Welcome to Javascript !).

These reason are all valid reasons to write the code above but unknown scenarios still need to be dealt with. Maybe the product itself is just invalid and if the code does not crash, you might never know about it.

Consider the following product being sent to this method :

```json
{
	"name": "Red Carpet",
	"Groups": [
		{
			"id":3,
			"name":"carpet"
		}
	]
}
```

Here we can see that this particular product lacks a proper "groups" property and instead has a "Groups" property with a capital G. This error which was introduced by another system which likely never be discovered and raised properly. The user probably just won't see any group associated in the interface and these data errors might never be fixed.

## Checks which are always true

Sometimes, we just want to be sure that EVERYTHING is in order and the world still works as it should so we add checks directly inside the classes on the private variables.
Here is another example in JavaScript :

```javascript
User.prototype.getGroup() {
  'use strict';
  // this should never happen...
  if (this !== null && typeof this !== 'undefined') {
    return this.group;
  }
  return null;
}
``

I obviously wrote here a terrible example to illustrate my point but examples in real life can also be really similar to this one. What is the point to check for the **this** keyword here ? It's obviously all going to be defined there since the function should be called with the context from the object itself. If someone is trying to execute something like:

```javascript
User.prototype.getGroup.call(null) // this usless call only works in strict mode
```

And if someone is trying to call your code like that, what is even the point of trying to check anything ? Since the code is not called with a User object, nothing is going to work in any of the User calls anyway.

## Main issues with Defensive programming

### Maintainability

Maintainting code with every function starting with a ten line null check on every object is not an easy task. Every time any object is changing, the code needs to be updated everywhere on every method.
Because of all the checks, even if some part of the code is not updated, nobody might know about it until it's too late.

Because errors are hidden and not being raised properly, it becomes difficult to know if the software is working as intended and testing also becomes harder. Unit tests are exploiting the fact that the program will raise errors if a problem occurs to cancel the tests. In some Unit tests, it's difficult to make the difference between "no data returned" or "no data returned because the data is invalid".
Proper error tracebacks are also difficult to get since no errors are actually raised, debugging becomes then a harder task where every piece of code need to be checked.


### Readability

Defensive programming makes much harder to read the actual logic of the code. The checks themselves are taking a lot of space on every part of the program and it might become complicated to figure out what was the actual goal the programmer had in mind when writing the functions.

