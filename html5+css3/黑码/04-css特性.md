# CSS 特性

- 继承性

- 层叠性
- 优先级

## 继承性 inherited

（1）子元素有默认继承父元素样式的特点 (子承父业)

可继承的常见属性（<span style="color:red">文字属性都可以继承</span>）

```html
color 
font-style font-weight font-size font-family 
text-align text-indent
line-height
...
```

<span style="color:red">控制文字的属性都能继承，不是控制文字的属性都不能继承</span>

**注意:** 可以通过调试工具判断样式是否可继承

（2）继承失效的特殊情况

如果元素有浏览器默认样式，就不继承父元素属性

- a 标签的 color 会继承时效
- h 系列标签的 font-size 会继承失效

示例 ：

```html
<style>
    div {
        color: green;
        font-size: 16px;
    }
</style>

<div>
    <h1>将进酒</h1>
    <a href="#">李白 〔唐代〕</a>
    <p>君不见黄河之水天上来，奔流到海不复回。</p>
</div>
```

![image-20230302125729226](./assets/3af64cb4f2b519fb5ae9bfaa027d76d0c64935da.png)

## 层叠性

同一个标签设置`不同`的样式

- 样式`层叠叠加`，共同作用在标签上

同一个标签设置`相同`的样式

- 样式会`层叠覆盖`，最终写在最后的样式生效

**特性:** 

- 给同一个标签设置不同的样式 -> 此时样式会重叠叠加 -> 会共同作用在标签上
- 给同一个标签设置相同的样式 -> 此时样式会层叠覆盖 -> 最终写在最后的样式会生效

**注意:**  当样式冲突时，只有**当选择器优先级相同时**，才能通过层叠性判断结果

> 技巧: 编辑器多行输入

示例 ：

```html
<style>
    .color--red {
        color: red;
    }

    /* 绿色的定义位置在红色之后 */
    .color--green {
        color: green;
    }

    .font-size--20 {
        font-size: 20px;
    }
</style>

<div class="color--green color--red font-size--20">
    君不见黄河之水天上来，奔流到海不复回。
</div>
```

![image-20230302125801977](./assets/8ebf3b1f0c5d79aa7e8bf7f5788f1059837a335a.png)

## 优先级

> 不同选择器具有不同的优先级，优先级高的选择器样式会覆盖优先级低的选择器样式

### 优先级公式（由低到高）

- 继承
- 通配符选择器 (*)
- 标签选择器
- 类选择器
- id 选择器
- 行内样式
- !important（慎重使用）
- 继承 < 通配符选择器(*) < 标签选择器 < 类选择器 < id选择器 < 行内样式 < !important

总结：选择范围越小，优先级越高

**注意:**

- !important写在属性值的后面，分号的前面!
- !important不能提升继承的优先级，<span style="color:red">只要是继承优先级最低!</span>
- 实际开发中不建议使用 !important



### 复合选择器权重叠加

> 场景: 如果是复合选择器，此时需要通过权重叠加计算方法，判断最终哪个选择器优先级最高会生效

**权重叠加计算公式:** (每级之间不存在进位)

```
(第一级,第二级,第三级,第四级)
(0, 0, 0, 0)

复合选择器中: (行内, ID, 类, 标签)
```

- 第一级 行内样式的个数
- 第二级 id 选择器的个数
- 第三级 类选择器的个数
- 第四级 标签选择器的个数

**比较规则:**

1. 先比较第一级数字，如果比较出来了，之后的通通不看
2. 如果第一级数字相同，此时再去比较第二级数字，如果比较出来了，之后的通通不看
3. ... 以此类推
4. 如果最终所有数字都相同，表示优先级相同，则比较层叠性 (谁在下面，谁说了算!)

**需要注意：**

- <span style="color:red">!important 如果不是继承，则权重最高，天下第一!</span> 
- 继承权重最低

> chrome 调试: 元素右键 -> 检查元素

示例 1：

```html
<style>
    /* (行内，id, 类，标签) */
    /* (0, 2, 0, 0) */
    #father #son {
        color: blue;
    }

    /* (0, 1, 1, 1) */
    #father p.c2 {
        color: black;
    }

    /* (0, 0, 2, 2) */
    div.c1 p.c2 {
        color: red;
    }

    /* 继承 */
    #father {
        color: green !important;
    }

    /* 继承 */
    div#father.c1 {
        color: yellow;
    }
</style>

<div id="father" class="c1">
    <p id="son" class="c2">白日依山尽，黄河入海流。</p>
</div>
```

![image-20230302125851392](./assets/df5e221f32cde166c9df71b438da2d4a210bce1f.png)

示例 2：

```html
<style>
    /* (行内，id, 类，标签) */
    /* (0, 0, 0, 2) */
    div div {
        color: skyblue;
    }

    /* (0, 0, 0, 1) */
    div {
        color: red;
    }
</style>

<div>
    <div>
        <div>白日依山尽，黄河入海流。</div>
    </div>
</div>
```

![image-20230302125953300](./assets/0851b79fc0c90527f7e3a3ead3d233f6247508c6.png)

示例 3：

```html
<style>
    /* (行内，id, 类，标签) */
    /* (0, 0, 0, 7) */
    div div div div div div div {
        color: red;
    }

    /* (0, 0, 1, 0) */
    .one {
        color: green;
    }
</style>

<div>
    <div>
        <div>
            <div>
                <div>
                    <div>
                        <div class="one">白日依山尽，黄河入海流。</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

![image-20230302130013109](./assets/0d8be35c401e8dbc12214816c1ef7d2e7144a9f3.png)

示例 4：

```html
<style>
    /* (行内，id, 类，标签) */
    /* (0, 0, 2, 1) */
    .c1 .c2 div {
        color: red;
    }

    /* (0, 1, 0, 1) */
    div #box3 {
        color: green;
    }

    /* (0, 1, 0, 1) */
    #box1 div {
        color: blue;
    }
</style>


<div id="box1" class="c1">
    <div id="box2" class="c2">
        <div id="box3" class="c3">白日依山尽，黄河入海流。</div>
    </div>
</div>
```

![image-20230302130040691](./assets/397e781f4b77cd1bf8e81fc5be9e211ef4049072.png)

示例 5：

```html
<style>
    /* (行内，id, 类，标签) */
    /* 都是继承，继承里面谁高，看继承哪个父级，哪个父级高，哪个选择器生效 */
    /* 都是继承，最近的父级生效 */
    /* 继承 */
    div p {
        color: red;
    }


    /* 继承 */
    .father {
        color: green;
    }
</style>


<div class="father">
    <p class="son">
        <span>白日依山尽，黄河入海流。</span>
    </p>
</div>
```

![image-20230302130103028](./assets/9a015495200665d638fa682028967590c12957de.png)