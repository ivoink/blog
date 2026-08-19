---
title: JavaScript 数组，二维数组与对象
category: Web前端笔记
published: 2026-05-27
image: ./cover.png
---
相比其他的知识点，这个还是有点忘记了，甚至C语言上的写法也忘的差不多了。

## 数组

这个绝对忘不了，这个也是C上面最基本的存储单位，写法也和JavaScript上差不多

```javascript
var arr = [1, 2, 3]
```

根据这个做了这样的一个小球跑动的项目

```html
<!doctype html>
<html>
    <head>
        <title></title>
    </head>
    <body>
        <script src="./p5.min.js"></script>
        <script>
            let num = 5;
            let xPos = [];
            let yPos = [];
            let radius = [];
            let speedx = [];
            let speedy = [];

            function setup() {
                createCanvas(800, 600);
                background("blue");

                for (let i = 0; i < num; i++) {
                    xPos[i] = random(800);
                    yPos[i] = random(600);
                    radius[i] = random(20, 50);
                    speedx[i] = random(-8, 8);
                    speedy[i] = random(-8, 8);
                }
            }

            function draw() {
                background("blue");
                fill("pink");
                noStroke();
                for (let i = 0; i < num; i++) {
                    circle(xPos[i], yPos[i], radius[i] * 2);
                    xPos[i] += speedx[i];
                    yPos[i] += speedy[i];

                    if (xPos[i] < radius[i] || xPos[i] > 800 - radius[i]) {
                        speedx[i] = -speedx[i];
                    }
                    if (yPos[i] < radius[i] || yPos[i] > 600 - radius[i]) {
                        speedy[i] = -speedy[i];
                    }
                }
            }
        </script>
    </body>
</html>
```

## 二维数组

这个在C语言里面写法是这样的

```c
int arr[3][4] = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};

printf("%d", arr[1][1]);
```

JavaScript不知道能不能说理解上会更简单

```javascript
var arr = {
	[1, 2, 3],
	[4, 5, 6],
	[7, 8, 9]
};

console.log(arr[1][1]);
```

将刚刚的这个项目写成二维数组的形式

```html
<!doctype html>
<html>
    <head>
        <title></title>
    </head>
    <body>
        <script src="./p5.min.js"></script>
        <script>
            let num = 5;
            // 二维数组：[x, y, radius, speedX, speedY]
            let balls = [];

            function setup() {
                createCanvas(800, 600);
                background("blue");

                balls = Array.from({ length: num }, () => [
                    random(800), // [i][0] - x
                    random(600), // [i][1] - y
                    random(20, 50), // [i][2] - radius
                    random(-8, 8), // [i][3] - speedX
                    random(-8, 8), // [i][4] - speedY
                ]);
            }

            function draw() {
                background("blue");
                fill("pink");
                noStroke();
                for (let i = 0; i < num; i++) {
                    circle(balls[i][0], balls[i][1], balls[i][2] * 2);
                    balls[i][0] += balls[i][3];
                    balls[i][1] += balls[i][4];

                    if (
                        balls[i][0] < balls[i][2] ||
                        balls[i][0] > 800 - balls[i][2]
                    ) {
                        balls[i][3] = -balls[i][3];
                    }
                    if (
                        balls[i][1] < balls[i][2] ||
                        balls[i][1] > 600 - balls[i][2]
                    ) {
                        balls[i][4] = -balls[i][4];
                    }
                }
            }
        </script>
    </body>
</html>
```

## 对象

这个词似乎在C语言里面有一个很熟悉的东西 —— `结构体`。

可以简单理解就是给数组里面的东西取一个相对便于记忆的名字，方便直接进行读取

```javascript
var arr = {
	x: "apple",
	y: 17,
	z: "orange"
}

console.log(arr.x);
```

项目就可以改成这样：

```html
<!doctype html>
<html>
    <head>
        <title></title>
    </head>
    <body>
        <script src="./p5.min.js"></script>
        <script>
            let num = 5;
            let balls = [];

            function setup() {
                createCanvas(800, 600);
                background("blue");

                for (let i = 0; i < num; i++) {
                    balls[i] = {
                        x: random(800),
                        y: random(600),
                        radius: random(20, 50),
                        speedX: random(-8, 8),
                        speedY: random(-8, 8),
                    };
                }
            }

            function draw() {
                background("blue");
                fill("pink");
                noStroke();
                for (let i = 0; i < num; i++) {
                    circle(balls[i].x, balls[i].y, balls[i].radius * 2);
                    balls[i].x += balls[i].speedX;
                    balls[i].y += balls[i].speedY;

                    if (
                        balls[i].x < balls[i].radius ||
                        balls[i].x > 800 - balls[i].radius
                    ) {
                        balls[i].speedX = -balls[i].speedX;
                    }
                    if (
                        balls[i].y < balls[i].radius ||
                        balls[i].y > 600 - balls[i].radius
                    ) {
                        balls[i].speedY = -balls[i].speedY;
                    }
                }
            }
        </script>
    </body>
</html>
```

### 效果都是如下样式

<iframe srcdoc="<!DOCTYPE html><html lang=&quot;zh-CN&quot;><head><meta charset=&quot;UTF-8&quot;><title>弹跳球动画</title><script src=&quot;https://cdn.jsdelivr.net/npm/p5@1/lib/p5.min.js&quot;></script><style>body{display:flex;justify-content:center;align-items:center;min-height:100vh;margin:0;background:#f0f0f0;}</style></head><body><script>let num=5;let xPos=[];let yPos=[];let radius=[];let speedx=[];let speedy=[];function setup(){createCanvas(800,600);background('blue');for(let i=0;i&lt;num;i++){xPos[i]=random(800);yPos[i]=random(600);radius[i]=random(20,50);speedx[i]=random(-8,8);speedy[i]=random(-8,8);}}function draw(){background('blue');fill('pink');noStroke();for(let i=0;i&lt;num;i++){circle(xPos[i],yPos[i],radius[i]*2);xPos[i]+=speedx[i];yPos[i]+=speedy[i];if(xPos[i]&lt;radius[i]||xPos[i]>800-radius[i]){speedx[i]=-speedx[i];}if(yPos[i]&lt;radius[i]||yPos[i]>600-radius[i]){speedy[i]=-speedy[i];}}}</script></body></html>" width="840" height="640" style="border:none;"></iframe>
