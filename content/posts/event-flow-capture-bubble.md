---
title: Event flow , capture, bubble and how to stop bubbling
date: 2023-12-30
tags: 
- javascript
- css
- html
- web api
showToc: true
---

## Event Bubbling in JavaScript

Event capturing is an event handling mechanism in JavaScript, contrasting with event bubbling. During the capturing phase, an event starts at the root node (usually the `document` object) and propagates down the DOM tree to the target element, where the event actually took place.

The process of event capturing is as follows:


1. **Capturing Phase**: When an event occurs, it is first captured at the topmost node of the DOM tree, then propagates downwards, level by level, until it reaches the target element. During this phase, only those event listeners set to use capturing mode are triggered.

2. **Target Phase**: When the event reaches the target element, event listeners set for both capturing and bubbling modes are triggered.

3. **Bubbling Phase**: After the target phase, if the event is defined as a bubbling event (not all events bubble), it travels back up the DOM tree in the reverse direction, eventually reaching the root node.

When adding event listeners, you can specify whether the listener is triggered during the capturing or bubbling phase. This is controlled by the third parameter of the `addEventListener` method. If this parameter is `true`, the listener is triggered during the capturing phase; if `false` (or omitted), it is triggered during the bubbling phase.

for example:
``` html
<body>
    <div class="father">
        <div class="son"></div>
    </div>
    <script>
        const father = document.querySelector('.father')
        const son = document.querySelector('.son')


        document.addEventListener('click',function(){
            alert('grandpa')
        }, true)

        father.addEventListener('click',function(){
            alert('father')
        }, true)

        son.addEventListener('click',function(){
            alert('son')
        }, true)
    </script>
</body>
```

## Event Bubbling in JavaScript

In JavaScript, event bubbling is another event-handling mechanism where an event on a specific element propagates upwards through the DOM tree. This means the event doesn't only trigger on the element it's directly bound to, but also on its parent elements, grandparents, all the way up to the root element (usually the `document` object).

This mechanism allows us to set up an event listener on a parent element to catch and handle events occurring on multiple child elements, instead of setting up individual event listeners on each child element. This approach is known as event delegation.

For instance, if you have a list, you can set up a click event listener on the entire list rather than setting it up on each list item individually. When any item in the list is clicked, the event will first trigger on the clicked item and then bubble up the DOM tree, eventually triggering the listener set on the list.

Event bubbling can be stopped by calling the `stopPropagation()` method on the event object. This prevents the event from continuing to bubble up the DOM tree, restricting it to the element where it was initially triggered.

for example:

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .father {
            width: 500px;
            height: 500px;
            background-color: yellow;
        }

        .son {
            width: 200px;
            height: 200px;
            background-color: red;
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="son"></div>
    </div>
    <script>
        const father = document.querySelector('.father')
        const son = document.querySelector('.son')


        document.addEventListener('click',function(){
            alert('grandpa')
        })

        father.addEventListener('click',function(){
            alert('father')
        })

        son.addEventListener('click',function(obj){
            alert('son')
            obj.stopPropagation()
        })

    </script>
</body>
</html>
```