# RecyclerView-ItemDecoration使用
```
//设置对应列表项的padding
getItemOffsets(Rect outRect, View view, RecyclerView parent, State state)
//一般用来绘制分割线
onDraw(Canvas c, RecyclerView parent, State state)
//一般用来添加特殊信息
onDrawOver(Canvas c, RecyclerView parent, State state)

绘制顺序：onDraw（decoration）->onDraw(child view)->onDrawOver(decoration)

```

#### 更改对应列表项的padding
```
getItemOffsets(Rect outRect, View view, RecyclerView parent, RecyclerView.State state)

outRect：outRect的值将会被加到对应View的padding上
view：表示当前改变的列表项（parent.getChildAdapterPosition(view)获取对应的position）
parent：当前RecyclerView对象
state：滑动状态

//例子
Drawable mDivider = ContextCompat.getDrawable(context, resId)
if (mOrientation == VERTICAL_LIST) {
    outRect.set(0, 0, 0, mDivider.getIntrinsicHeight());
} else {
    outRect.set(0, 0, mDivider.getIntrinsicWidth(), 0);
}
```

#### 绘制分割线
```
onDraw(Canvas c, RecyclerView parent, State state)

c：RecyclerView画板，可以在RecyclerView范围内随意画画
parent：RecyclerView实例
state：滑动状态
```

#### 添加附加信息
```
onDrawOver(Canvas c, RecyclerView parent, State state)

c：RecyclerView画板，可以在RecyclerView范围内随意画画
parent：RecyclerView实例
state：滑动状态
```


