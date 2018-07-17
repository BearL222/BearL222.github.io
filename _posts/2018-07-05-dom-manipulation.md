---
layout: post
title: DOM Manipulation
category: web-developer-bootcamp
tags: dom, web
---

# Intro to the DOM
JS meets HTML + CSS

# Defining the DOM
DOM is the interface between HTML + CSS

# Select and Manipulate
## Select
```
var h1 = document.querySelector("h1");
```
Select the <h1> 

## Manipulate
```
var h1 = document.querySelector("h1");
h1.style.color = "pink";
```
change color of &lt;h1&gt; to pink  

Another example  

```
var body = document.querySelector("body");
var isBlue = false;

setInterval(functino() {
  if(isBlue) {
  	body.style.background = "white";
  } else {
  	body.style.background = "#3498db";
  }
  isBlue = !isBlue;
), 1000);
```
Select the <body> and change its color every second

# Important Selector Methods

- document.URL
- document.links
- document.body
- document.head

## Methods
### document.getElementById()
Takes a string argument and returns the one element with a matching ID
```
var tag = document.getElementById("highlight");
```

### document.getElementsByClassName()
Takes a string argument and returns a list of elements that have a matching class
```
var tags = document.getElementsByClassName("bolded");
console.log(tags[0]);
```

### document.getElementsByTagName
Returns a list of all elements of a given tag name, like <li> or <h1>
```
var tags = document.getElementsByTagName("li");
console.log(tags[0]);
```

### querySelector
Returns the first element that matches a given CSS-style selector
```
//select by ID
var tag = document.querySelector("#highlight");
```

### querySelectorAll
Returns a list of elements that matches a given CSS-style selector
```
//select by tag
var tags = document.querySelectorAll("h1");
```

# DOM Manipulation
## Style
```
tag.style.color = "yellow"
```

Alternative:  
Rather than directly manipulating style with JS, we can define a CSS class and then toggle it on or off with JS  
//INSTEAD OF THIS:  
```
var tag = document.getElementById("highlight");
tag.style.color = "blue";
tag.style.border = "10px solid red";
```

/*DEFINE A CLASS IN CSS*/
```
.some-class {
  color: blue;
  border: 10px solid red;
}
```

//ADD THE NEW CLASS TO THE SELECTED ELEMENT
```
var tag = document.getElementById("highlight");
tag.classList.add("some-class");
```

## classList
A read-only list that contains the classes for a given element.  It is not an array.


```
/*DEFINE A CLASS IN CSS*/ 
.another-class {
  color: purple;
  fontSize: 76px;
}
```

```
var tag = document.querySelector("h1");

//ADD A CLASS TO THE SELECTED ELEMENT
tag.classList.add("another-class");

//REMOVE A CLASS
tag.classList.remove("another-class");

//TOGGLE A CLASS
tag.classList.toggle("another-class");
```

# Manipulating text, context, attributes

## textContent
Returns a string of all the text contained in a given element  
It treats everything as string.

## innerHTML
Similar to textContent, except it returns a string of all the HTML contained in a given element  
It treats everything as HTML

## Attributes
Use getAttribute() and setAttribute() to read and write attributes like src or href
```
<a href="www.google.com">I am a link</a>
<img src="logo.png">
```

```
var link = document.querySelector("a");
link.getAttribute("href");  //"www.google.com"
//CHANGE HREF ATTRIBUTE
link.setAttribute("href","www.dogs.com"); 
///<a href="www.dogs.com">I am a link</a>

//TO CHANGE THE IMAGE SRC
var img = document.querySelector("img");
img.setAttribute("src", "corgi.png");
//<img src="corgi.png">
```