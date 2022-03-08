### 常用img属性：

1.控制在父元素中垂直居中：
$$
vertical-align:middle
$$


### 常用块级元素对子元素：

- 块级元素内部的文本水平居中：

- $$
  text-align:center
  $$

- 设置内部除img元素的垂直居中：

- $$
  在块级元素中设置height 和对应的 line-height
  $$

- $$
  父元素display:flex;而子元素align-self:center
  $$

- 父元素添加伪元素实现子元素垂直居中：

- $$
  :beforecontent:"";display:inline-block;verticalalign:middle;height:100%}
  $$

- 

- $$
  给父元素display:table，子元素display：table-cell的方式实现CSS垂直居中
  $$

- 要垂直居中的：对于未知父元素高度的：

- $$
  在父元素中：position:relative 
  
  子元素：widht:50%;height:50%;position:absolute;top:50%;transform:translateY(-50%)
  $$



### span 常用属性：

- span内容超出部分以...显示：

overflow: hidden和white-space: nowrap都是必须的否则不会显示省略号；

```css
span {

   overflow: hidden; 

   text-overflow: ellipsis; 

   -o-text-overflow: ellipsis;

   white-space:nowrap;

   width:240px;

   height:24px;

   display:block;

}
```

- span超出部分使用滚动显示：将上面的 overflow: hidden; 替换为：overflow: scroll; 