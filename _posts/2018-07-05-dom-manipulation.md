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

