# CSS 基础

## 选择器

>选择器可以将样式与元素绑定

### 属性选择器
* E[foo] 选择匹配E的元素,并且该元素定义了foo属性值
* E[foo='bar'] 选择匹配E的元素，并且该元素定义了foo属性值为'bar'
* E[foo~='bar'] 选择匹配E的元素，并且该元素滴定义了foo属性值是一个以空格符号隔的列表，其中一个列表值为'var'
* E[foo|='bar] 选择匹配E的元素，并且该元素定义foo属性值是一个以连字符(-)分割的列表，值开头是‘bar’
* E[foo^='bar'] 选择匹配E的元素，并且该元素定义foo属性值包含‘bar’前缀的子字符串
* E[foo$='bar'] 选择匹配E的元素，并且该元素定义foo属性值包含'bar'后缀的子字符串
* E[foo*='bar'] 选择匹配E的元素，并且该元素定义foo属性值包含'bar'的字符串

### 结构伪类选择器
* E:nth-child(n) 选择所有在其父元素中第n个位置的匹配E的子元素
* E:nth-last-child(n)
* E:nth-of-type(n) 选择所有在其父元素中同类型第n个位置的匹配E的子元素
* E:nth-last-of-type(n)
* E:last-child 选择位于父元素中最后一个位置，且匹配E的子元素
* E:first-of-type == E:nth-of-type(1)
* E:last-of-type == E:nth-last-of-type(1)
* E:only-child 选择其父元素只包含一个E元素
* E:only-of-type 选择其父元素只包含一类E元素
* E:empty 选择匹配E的元素，且该元素不包含子节点

### UI伪类选择器

> UI:User Interface,UI状态一般包括可用、不可用、选中、未选中、获取焦点、失去焦点、锁定和待机等。
> 在网页中UI元素指包含在form元素内的表单元素:input

* E:enabled 选择匹配E的所有可用UI元素
* E:disabled 选择匹配E的所有不可用UI元素
* E:checked 选择匹配所有选中的UI元素

### 其他选择器
* E~F 选择匹配F的所有元素，并且匹配元素位于匹配E的元素后面（E,F在一级结构）
* E：not(s) 选择匹配E的所有元素，并且过滤S选择符的任意元素

```language
<div>
  <p class="red">1</p>
</div>
<div>
  <p>2</p>
</div>
<p>3</p>

div p :not(.red) 匹配<p>2</p>
```

* E:target 选择匹配E所有元素，并且匹配元素被相关URL指向

```language
localhost:8080/index.html#red

<div id="red">1</div>

div target {color:red;} 匹配<div id="red">1</div>
```

## 文本、字体、颜色

### 文本阴影

#### text-shadow: xem yem zem color
* x 水平位移 正为偏右
* y 垂直位移 正为偏下
* z 模糊半径
* color 阴影颜色

### 颜色

#### rgba(r,g,b,a) 支持透明

#### hsl(length,percentage,percentage)
* length 色调 0红色 60黄色 120绿色 180青色 240蓝色 300洋红
* percentage 饱和度
* percentage 亮度 0最暗 50%均值 100%最亮（白色）

#### hsla(length,percentage,percentage,opacity)
* length 色调 0红色 60黄色 120绿色 180青色 240蓝色 300洋红
* percentage 饱和度
* percentage 亮度 0最暗 50%均值 100%最亮（白色）
* opacity 不透明度

## 背景和边框

### 多色边框
* border-color 边框颜色
* border-top-color 顶部边框颜色
* border-bottom-color 底部边框颜色
* border-left-color 左侧边框颜色
* border-right-color 右侧边框颜色

### 圆角边框
* border-radius 边框颜色
* border-top-right-radius 右上角圆角
* border-bottom-right-radius 右下角圆角
* border-bottom-left-radius 左下角圆角
* border-top-left-radius 左上角圆角

### 元素阴影

#### box-shadow 1(可选),2（X轴位移）,3（Y轴位移）,4（可选）,5（可选）,6（可选）
* 1 阴影类型 模型是投影 inset(内阴影)
* 2 X轴位移
* 3 Y轴位移
* 4 阴影大小
* 5 阴影扩展
* 6 阴影颜色

### 设计背景
* background-origin 指定背景显示区域 border|padding|conteng
* background-clip 指定背景裁剪区域
* background-size 定义背景图片的大小 cover 保持背景图像本身的宽高比例  contain 保持图像本身的宽高比例

## 2D变形

### 旋转
rotate(90deg)

### 缩放
scale(x)
scale(x,y)

### 移动
translate(x,0px)
translate(x,y)

### 倾斜
第一个参数相对于X倾斜 正数为与X轴正方向成60deg
第二个参数相对于Y倾斜 正数为与Y轴正方向成60deg
skew(60deg,0deg)
skew(60deg,60deg)

### 变形动画
matrix(1,2,3,4,5,6)

### 自定义变形
transform-origin: x y x和y支持百分比和left、center等

## 设计动画

### 定义过渡属性
transition-property 定义转换动画的CSS属性名称
默认为all
none 表示没有元素
all 针对所有元素
IDENT 指定CSS属性列表

### 定义过渡时间
transition-duration 2s

### 定义过渡延时时间
transition-delay 2s

### 定义过渡效果
transition-timing-function
* ease 缓解效果 默认
* linear 线性效果
* ease-in 渐显效果
* ease-out 渐隐效果
* ease-in-out 渐显-渐隐效果
* cubic-bezier 特殊的立方体贝塞尔曲线效果

## 网页布局
### 多列布局
columns:250px 3 3栏显示 每栏250px
column-width:300px|auto 每个栏目最打宽度为300像素，未设置为自动
column-count:3|auto 最大列数
column-gap:normal|3em 列间距 normal（1em） 3em




































