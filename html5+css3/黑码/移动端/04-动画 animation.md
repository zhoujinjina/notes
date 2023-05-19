# 动画 animation

过渡 vs 动画

- 过渡：用于2个状态变化过程
- 动画：实现<span style="color:red">多个状态</span>间的变化过程，动画<span style="color:red">过程可控</span>(重复播放、最终画面、是否暂停)

动画

- 动画的本质：快速切换大量图片时在人脑中行成的具有<span style="color:red">连续性的画面</span>
- 构成动画的最小单元：<span style="color:red">帧或动画帧</span>

实现步骤：

1. 定义动画

```css
/* 定义两种状态 */
@keyframes 动画名称 {
  from {
  }
  to {
  }
}

/* 定义多种状态 */
/* 百分比表示动画总时长的占比 */
@keyframes 动画名称 {
  0% {
  }
  10% {
  }
  50% {
  }
  100% {
  }
}
```

2. 使用动画

```css
animation: 动画名称 动画花费时长;
```

示例:

```html
<style>
    .box {
        width: 50px;
        height: 50px;
        background-color: skyblue;
    }

    .box:hover {
        /* 使用动画 */
        animation: change-width 2s;
    }

    /* 定义动画 */
    @keyframes change-width {
        from {
            width: 50px;
        }

        to {
            width: 200px;
        }
    }
</style>

<div class="box"></div>
```

<iframe src="https://mouday.github.io/coding-tree/blog/front-end-combat/demo/animation-1.html" height="70" style="-webkit-font-smoothing: antialiased; -webkit-tap-highlight-color: transparent; text-size-adjust: none; box-sizing: border-box; font-size: 16px; border: 1px solid rgb(238, 238, 238); width: 1px; min-width: 100%; margin: 1em 0px; color: rgb(52, 73, 94); font-family: &quot;Source Sans Pro&quot;, &quot;Helvetica Neue&quot;, Arial, sans-serif; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>

## 动画属性

```css
animation: 动画名称 动画时长 速度曲线 延迟时间 重复次数 动画方向 执行完毕时状态;
```

注意：

- 动画名称 和 动画时长必须赋值
- 取值不分先后顺序
- 如果有 2 个时间值，第一个时间表示动画时长，第二个时间表示延迟时间

示例:

```html
<style>
    .box {
        width: 50px;
        height: 50px;
        line-height: 50px;
        text-align: center;
        background-color: skyblue;
    }

    /* 基本动画 */
    .box-basic {
        animation: change-width 2s;
    }

    /* 匀速动画 */
    .box-linear {
        animation: change-width 2s linear;
    }

    /* 分步动画: steps(n) n表示多少步 */
    .box-steps {
        animation: change-width 2s steps(3);
    }

    /* 延迟动画 */
    .box-delay {
        animation: change-width 2s 2s;
    }

    /* 重复3次 */
    .box-repeat {
        animation: change-width 2s 3;
    }

    /* 无限循环 */
    .box-infinite {
        animation: change-width 2s infinite;
    }

    /* 反向效果动画 */
    .box-alternate {
        animation: change-width 2s infinite alternate;
    }

    /* 动画停留在最初状态 backwards(默认值) */
    /* 动画停留在最后状态 forwards */
    .box-forwards {
        animation: change-width 2s forwards;
    }

    /* 定义动画 */
    @keyframes change-width {
        from {
            width: 50px;
        }

        to {
            width: 200px;
        }
    }
</style>


<div class="box box-basic">basic</div>
<div class="box box-linear">linear</div>
<div class="box box-steps">steps</div>
<div class="box box-delay">delay</div>
<div class="box box-repeat">repeat</div>
<div class="box box-infinite">infinite</div>
<div class="box box-alternate">alternate</div>
<div class="box box-forwards">forwards</div>
```

<iframe src="https://mouday.github.io/coding-tree/blog/front-end-combat/demo/animation-2.html" height="420" style="-webkit-font-smoothing: antialiased; -webkit-tap-highlight-color: transparent; text-size-adjust: none; box-sizing: border-box; font-size: 16px; border: 1px solid rgb(238, 238, 238); width: 1px; min-width: 100%; margin: 1em 0px; color: rgb(52, 73, 94); font-family: &quot;Source Sans Pro&quot;, &quot;Helvetica Neue&quot;, Arial, sans-serif; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>

**background复合属性**

```css
background: color image repeat attachment position;
```

- background-color
- background-image
- background-repeat
- background-attachment: 设置背景图像是否固定或者随着页面的其余部分滚动
- background-position
- background-size: cover/contian
  - cover: 图片完全覆盖盒子，可能会导致图片显示不全
  - contian：最大边和盒子尺寸相等，就不进行缩放

animation复合属性（了解）

| 属性                        | 作用                                              | 取值                                                         |
| --------------------------- | ------------------------------------------------- | ------------------------------------------------------------ |
| animation-name              | 动画名称                                          |                                                              |
| animation-duration          | 动画时长                                          |                                                              |
| animation-delay             | 延迟时间                                          |                                                              |
| `animation-fill-mode`       | <span style="color:red">动画执行完毕时状态</span> | <span style="color:red">forwards 最后一帧状态/ backwards第一帧状态</span> |
| animation-timing-function   | 速度曲线                                          | <span style="color:red">steps(数字): 逐帧动画</span>         |
| `animation-iteration-count` | <span style="color:red">重复次数</span>           | <span style="color:red">infinite 无限循环</span>             |
| `animation-direction`       | <span style="color:red">动画执行方向</span>       | <span style="color:red">alternate 反方向</span>              |
| animation-play-state        | 暂停动画                                          | paused 暂停，通常配合hover使用                               |



- 补间动画：两个动画之间平滑动画
- 逐帧动画：两个动画之间状态不补全。开发中一般配合<span style="color:red">精灵图</span>实现动画效果
  - `animation-timing-function: steps(N);` 将动画过程<span style="color:red">等分</span>成N份
- 精灵动画制作步骤
  - 准备显示区域
    - 设置盒子尺寸是一张小图的尺寸，背景图为当前精灵图
  - 定义动画
    - 改变背景图的位置 (移动的距离就是<span style="color:red">精灵图的宽度</span>)
  - 使用动画
    - 添加速度曲线 `steps(N)`，N与精灵图上小图<span style="color:red">个数相同</span>
    - 添加无限重复效果

## 多组动画

```css
animation: 动画1, 动画2, ...动画N;
```

走马灯，无缝动画

```css
hmtl, body {
    height: 100%
}
```

示例: 无缝动画

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible"
          content="IE=edge">
    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            margin: 0 auto;
            width: 600px;
            height: 100px;
            background-color: skyblue;
            overflow: hidden;
        }

        .box ul {
            list-style: none;
            display: flex;
            width: 2600px;
            animation: move 5s infinite linear;
        }

        /* 鼠标经过，暂停动画 */
        .box:hover ul {
            animation-play-state: paused;
        }

        .box ul li {
            height: 100px;
            line-height: 100px;
            width: 200px;
            text-align: center;
            font-size: 30px;
            color: white;
            font-weight: 500;
        }

        /* 动画位移，向左移动10个元素 */
        @keyframes move {
            from {
                transform: translate(0);
            }

            to {
                transform: translate(-2000px);
            }
        }
    </style>

    <div class="box">
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
            <li>6</li>
            <li>7</li>
            <li>8</li>
            <li>9</li>
            <li>10</li>

            <!-- 复制出来，实现无缝衔接 -->
            <li>1</li>
            <li>2</li>
            <li>3</li>
        </ul>
    </div>
</body>

</html>
```

<iframe src="https://mouday.github.io/coding-tree/blog/front-end-combat/demo/animation-walking.html" height="120" style="-webkit-font-smoothing: antialiased; -webkit-tap-highlight-color: transparent; text-size-adjust: none; box-sizing: border-box; font-size: 16px; border: 1px solid rgb(238, 238, 238); width: 1px; min-width: 100%; margin: 1em 0px; color: rgb(52, 73, 94); font-family: &quot;Source Sans Pro&quot;, &quot;Helvetica Neue&quot;, Arial, sans-serif; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>

https://www.bilibili.com/video/BV1xq4y1q7jZ?p=55&spm_id_from=pageDriver