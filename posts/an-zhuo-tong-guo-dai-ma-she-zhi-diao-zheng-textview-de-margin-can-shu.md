---
title: '安卓通过代码设置调整TextView的Margin参数'
date: 2020-07-02 14:55:09
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
  在调整安卓键盘机的简化版**launcher**时遇到了**设置大字体后图标和名称重合**的情况，非常不美观，文档上提供了这样的方法：
 
  

```
  setLayoutParams(ViewGroup.LayoutParams params)；
```

  
  
 后上网查，[链接](https://segmentfault.com/q/1010000004032766/a-1020000004034499)上看到教程，原来要动态改变TextView（或者其它View）的margin属性（==android:layout_marginTop==），尝试了动态添加view的方法，但是由于Textview是包裹在Framelayout里的，而Textview是在Convertview中生成的，所以选择直接调用`FrameLayout.LayoutParams`方法。
 
 但是一开始弄混了顺序，让Textview生成后才调用`setLayoutParams`方法，导致设置无效，更正后的代码：
 
 
```
    FrameLayout.LayoutParams layoutParams = new FrameLayout.LayoutParams(FrameLayout.LayoutParams.WRAP_CONTENT,
        FrameLayout.LayoutParams.WRAP_CONTENT);
    layoutParams.setMargins(0, 9, 0, 2);
    title = (TextView)convertView.findViewById(R.id.title);
    title.setLayoutParams(layoutParams);
```

成功后如图所示：
![image](https://github.com/Jackyhhh/Picbed_PicGo/blob/master/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20200702135718.png)