# Less

> less 是一个 <span style="color:red">css 预处理器</span>，Less文件后缀是`.less`

网站：

- https://lesscss.org/
- https://less.bootcss.com/

作用：

- 更简单的完成 css
- 扩充 css 语言，使 CSS 具备一定的逻辑性、计算能力
- <span style="color:red">浏览器不识别 Less 代码，目前阶段，网页要引入对应的 CSS 文件</span>

VS Code 插件： `Easy Less`

Easy Less 用途：

- 保存 less 文件<span style="color:red">自动生成</span> css 文件
- less 运算写法完成 px 单位到 rem 单位

## 注释

```
// 单行注释  快捷键 ctrl + /，单行注释不会出现在css中 

/* 快注释 快捷键 shift + alt + A */
```

## 运算

- 加、减、乘直接书写计算表达式
- <span style="color:red">除法</span>需要添加小括号或`.`

```less
.box {
  width: 100 + 10px; // 110px;
  width: 100 - 20px; // 80px;
  width: 100 * 2px; // 200px;

  // 除法
  // 推荐小括号写法
  width: (100 / 4px); // 25px;
  // 不支持 height: 100 ./ 4px; // 25px;
}
```

输出

```css
.box {
  width: 110px;
  width: 80px;
  width: 200px;
  width: 25px;
}
```

## 嵌套

> 使用嵌套写法生成<span style="color:red">后代选择器</span>

**作用: **快速生成后代选择器

**语法: **

```less
.父级选择器 {
    // 父级样式
    .子级选择器 {
        // 子级样式
    }
}
```

**例子**:

```less
.father {
  color: red;

  .son {
    width: 100px;
  }
}
```

输出

```css
.father {
  color: red;
}

.father .son {
  width: 100px;
}
```

`&` <span style="color:red">不</span>生成后代选择器，表示<span style="color:red">当前选择器</span>，通常配合<span style="color:red">伪类或伪类元素</span>使用

## 变量

> 存储数据，方便使用和修改

**语法**

```
// 定义变量
@变量名：值;

// 使用变量
CSS属性：@变量名;
```

**示例**

```less
@color: red;

.box {
  color: @color;
}
```

输出

```css
.box {
  color: red;
}
```

## 导入 less 文件

```less
// 可以省略后缀.less
@import './other.less';
```

## 导出 css 文件

> less 文件夹输出到 css 文件夹

**方法一:**

- 配置 `EasyLess` 插件，实现所有 Less 有相同的导出路径
- 配置插件: 设置 -> 搜索 EasyLess -> 在 setting.json 中编辑 -> 添加代码 (注意，必须是<span style="color:red">双引号</span>)

VS Code 插件 Easy Less 设置 settings.json

```json
{
  "less.compile": {
    "out": "../css/"
  }
}
```

**方法二: **控制单个文件导出路径，`less` 第一行指定输出路径

```css
// out: ./css/
```

<span style="color:red">禁止导出: </span> 在 less 文件<span style="color:red">第一行</span>添加

```css
// out: false
```

https://www.bilibili.com/video/BV1xq4y1q7jZ?p=130&spm_id_from=pageDriver