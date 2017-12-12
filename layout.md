### 圣杯
```css
        .wrap {
            width: 960px;
            padding: 0 200px;
            margin: 0 auto;
            box-sizing: border-box;
        }
        .wrap div {
            height: 600px;
        }
        .mid {
            width: 100%;
            background-color: aqua;
            float: left;
        }
        .left {
            width: 200px;
            background-color: #582;
            float: left;
            margin-left: -100%;
            transform: translateX(-100%);
        }
        .right {
            width: 200px;
            background-color: #333;
            float: left;
            margin-left: -200px;
            transform: translateX(100%);
        }
```
```html
<div class="wrap">
    <div class="mid"></div>
    <div class="left"></div>
    <div class="right"></div>
</div>
```

### 双飞翼
```css
        .wrap {
            width: 960px;
            margin: 0 auto;
        }
        .wrap div {
            height: 600px;
        }
        .mid {
            width: 100%;
            float: left;
            background-color: #222;
        }
        .left {
            width: 200px;
            float: left;
            background-color: #583;
            margin-left: -100%;
        }
        .right {
            width: 200px;
            float: left;
            background-color: #333;
            margin-left: -200px;
        }
        .main {
            margin:0 200px;
        }
```
```html
<div class="wrap">
    <div class="mid">
        <div class="main"></div>
    </div>
    <div class="left"></div>
    <div class="right"></div>
</div>
```
