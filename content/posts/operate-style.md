---
title: Control CSS using classList
date: 2023-12-25
tags: 
- javascript
- css
- html
- web api
---

ClassList can help reduce the redundancy of .style method and resolve the ClassName overwrite risk.

------------
Sytax: 

```
// add a class
element.classList.add('className')
// delete a class 
element.classList.remove('className')
// switch a class
element.classList.toggle('className')
```

example:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box {
            width: 200px;
            height: 200px;
            color: #333;
        }
        .active {
            color: red;
            background-color: pink;
        }
    </style>
</head>
<body>
    <div class="box">text</div>
    <script>
        //get element
        const box = document.querySelector('.box')
        //change stylew by adding class
        box.classList.add('active')
        // delete class
        box.classList.remove('active')
        //switch class
        box.classList.toggle('active')
    </script>
</body>
</html>
```

>**keep in mind that the running logic of `toggle` is run the detect if the class existed in the element, if yes, delete, if no, add up**

