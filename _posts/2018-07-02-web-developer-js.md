---
layout: post
title: Javascript
catogery: web-developer-bootcamp
tags: web javascript
---
# Intro to Javascript 
## Variables

1. Null: explicitly nothing
2. Undefined: never assign value to a variable

## Built-in Methods

1. alert: pop up a message
2. prompt: get input from user
3. console.log: print things to the js console
4. Clear(): clear the console

# Javascript Basics: Control Flow
## Unit Objectives

1. Boolean logic:  
===: equal value and type (strict)
2. logical operators

## Logical Operations

AND, OR, NOT e.g.  

|	Operator	|	Name	|	Example	|	Result	|
|---|---|---|---|
|&&|AND|x < 10 && x !== 5|false|
|\|\||OR|y < 9 ``||`` x === 5|true|
|!|NOT|!(x === y)|true|

1. AND: &&
2. OR: OR
3. NOT: !
4. Truthy and Falsy values:  
Values that aren’t actually true of false, are still inherently “truthy” or “falsy” when evaluated in a boolean context  
e.g. !”hello” = False

Falsy values:

- false
- 0
- ""
- null
- undefined
- NaN

Everything else is truthy

## JS Conditionals (logical) and Loops

### Conditionals
- if
- else if
- else

### While
```
while() {

}
```
### For
```
for(var count = 0; count < 10; count++) {

}
```

# Javascript Basics: Functions
## Unit Objectives
```
function doSomething() {
	// do something
}
```

## Arguments
```
function square(argu) {
	// do something with argu
}
```

When using fewer arguments than the function expects, it won't return error message but use _undefined_ as the argument instead.

## the return keyword
Every function returns something (possible undefined).
```
function square(x) {
	return x * x;
]
```

## Function Declaration vs. Function Expression
```
// function declaration
function capitalize(str) {
	return str.charAt(0).toUpperCase() + str.slice(1);
}

// function expression
var capitalize = function(str) {
	return str.charAt(0).toUpperCase() + str.slice(1);
}
```

## Higher Order Functions
Pass function to another function

### Anonymous function
```
setInterval(functino() {
	console.log("This is an anonymous function")
}, 2000);
```

# Javascript Basics: Array
## Intro
```
var friends = ["Charlie", "Liz", "David", "Mattias"];

var length = friends.length
```

## Built-in Methods
### push/pop
Just like a Stack  
push(): put sth. at the very end of an array  
pop(): remove last element in an array  

### shift/unshift
Just like a queue  

### indexOf

### slice
slice(start, end) 

### splice
splice(index, number)

## Array Iteration
arr.forEach(someFunction(element, index) {
	// something about element 
})  
OR  
arr.forEach(someFunction)

# Javascript Basics: Object