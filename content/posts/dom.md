---
title: DOM -- Document Object Model
date: 2023-12-25
tags: 
- javascript
- web api
---
## DOM query

### Slect first match element
``` javascript
document.querySelector('css selector')
```

### Slect all match element
``` javascript
document.querySelectorAll('css selector')
```

>return is fake array which no work with `push` and `pop` method 


## Modification using DOM

### modify text content
``` html
<body>
    <div class="box">content</div>
    <script>
        const box = document.querySelector('.box')
        box.innerText = 'content changed'
        box.innerHTML =  '<strong>content changed</strong>'
    </script>
</body>
```
> innerText method will not parse tags, exp: `<strong>hello</strong>` will return `<strong>hello</strong>` rather **hello**


