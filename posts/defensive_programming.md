# Why being so defensive when programming ?

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
 - What about the the product is not formed properly ?
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

## Issues with Defensive programming

### Maintainability

### Readability

// Defensive programming makes harder to read the actual logic of the code.
// At the beginning of each function, a 10 line null check [...]