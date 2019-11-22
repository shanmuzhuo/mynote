# 微信读书的前端Dom乱序

逛论坛上说微信的读书的pc版出来后，dom完全是乱的，但是文档确实正常排列。然后有人复现了简单的实现模式。代码如下,做摘抄以记录。

```javascript
var container = document.querySelector('#container')
var font = 16
var lineHeight = 20
var text = '这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字'
function main() {
  var width = container.getBoundingClientRect().width
  var numPerLine = Math.floor(width/font)
  container.style.height = Math.ceil(text.length/numPerLine) * lineHeight + 'px'
  var html = text
  .split('')
  .map((s, i) => {
    var n = i + 1
    var line = Math.ceil(n/numPerLine)
    var indent = n % numPerLine || numPerLine
    return `<span style="left: ${font*(indent-1)}px;top: ${lineHeight*(line-1)}px">${s}</span>`
  })
  .sort(() => Math.random() - 0.5)
  .join('')

  container.innerHTML = html
}

main()

window.onresize = function() {
  main()
}
```

```css
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
  <style>
    #container {
      position: relative;
      height: 20px;
      line-height: 20px;
      border: 1px solid #bdbdbd;
      font-size: 16px;
    }
    #container > span {
      position: absolute;
    }
  </style>
</head>
<body>
  <div id="container">
    
  </div>
</body>
</html>
```

