---
title: Timer
date: 2023-12-26
tags: 
- javascript
- css
- html
- web api
---

Javascript timer function can make some code be excueted repeatedly over time.

Syntax: 
``` javascript
// open
setInterval(function,interaval-time)
// close
let t = setInterval(function,interaval-time)
clearInterval(t)
```

`t`: variable

`interaval-time` unit: ms

-----------------

Example: 

``` html
<body>
    <button class="btn" disabled>aggree(5)</button>
    <script>
        const btn = document.querySelector('.btn')
        let i = 5
        let timer = setInterval(function(){
            i--
            btn.innerHTML = `aggree(${i})`
            if (i === 0){
                clearInterval(timer)
                btn.disabled = false
                btn.innerHTML = 'aggree'
            }
        },1000)
        
    </script>
</body>
```