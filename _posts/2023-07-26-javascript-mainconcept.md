---
layout: post
categories: JavaScript
title: (JavaScript) 자바스크립트 주요 개념
date: 2023-07-27
permalink: /js/02
tags:
---
*content
{:toc}




# this
| 호출 위치                         | 지칭 객체                               |
| ----------------------------- | ----------------------------------- |
| in an object method           | the "owner" of the object           |
| alone                         | the global object                   |
| in a funciton                 | global object                       |
| in a function, in strict mode | undefied                            |
| in an event                   | the element that received the event |

---
# Events
- "things" that happen to HTML elements
- "react" to HTML elements's action
	- onchange 
	- onclick  
	- onmouseover 
	- onmouseout  
	- onkeydown   
	- onload           
## Event Handlers
- every time a page loads
- whe the page is closed
- when a user clicks a button
- when a user inputs data
---

# Modules
- to break up your code into separate files
- Modules are imported from external files with the **import** statement.
```html
<script type="module">
//import from named export
import {name, age} from "./person.js"; 
//import from default export
import personalInfo from "./personalInfo.js"; 
</script>
```
## Export
### Named Exports
- individually
```js
//person.js
export const name = "Mina";
export const age = 22;
```
- all at once at the bottom
```js
const name = "Mina";
const age = 22;

export {name, age};
```
### Default Exports
```js
const personalInfo = () => {
	const name = "Mina";
	const age = 22;
	return name + ' is ' + age + "years old";
};

export default personalInfo;
```