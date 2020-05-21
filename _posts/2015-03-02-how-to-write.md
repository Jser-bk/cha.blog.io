---
layout: post
title: 这是一篇博客文章模板
date: 2015-3-02
categories: blog
tags: [标签一,标签二]
description: 文章金句。
---

jquery 实现购物车的价格计算和商品件数计算

html代码如下
```
<ul>
    <li>
        <input type="checkbox">商品一 单价 <span>100</span> <button>-</button>
        <input type="text" value="1"> <button>+</button> 小计 : <span>100</span>
    </li>
    <li>
        <input type="checkbox">商品二 单价 <span>150</span> <button>-</button>
        <input type="text" value="1"> <button>+</button> 小计 : <span>150</span>
    </li>
    <li>
        <input type="checkbox">商品三 单价 <span>200</span> <button>-</button>
        <input type="text" value="1"> <button>+</button> 小计 : <span>200</span>
    </li>
</ul>
<p>
    一共 <span id="count">0</span> 件商品，共计 <span id="countMoney">0</span> 元
</p>
```
js代码如下
```
<script src="jquery-3.4.1.js"></script>
<script>
    //点击减号
    $("li button:nth-of-type(1)").click(function () {
        //判断输入框输入框的值是否小于0
        if($(":text").attr("value")>0){
            $(this).next("input").attr("value",$(this).next("input").attr("value")-1)
        }else {
            $(this).next("input").attr("value",0)
        }
        $(this).next("input").next("button").next("span").html($(this).prev("span").html()*$(this).next("input").val())
    });
    //点击加号
    $("li button:nth-of-type(2)").click(function (){
        $(this).prev("input").attr("value",parseInt($(this).prev("input").attr("value"))+1);
        $(this).next("span").html($(this).prev("input").val()*$(this).prev("input").prev("button").prev("span").html());
    });
    //点击多选按钮
    $(":checkbox").click(function () {
        var n = 0;
        var m = 0;
        $.each($(":checkbox:checked"),function (index,item) {
            n += parseInt($(item).siblings("input").val());
            m += parseInt($($(item).siblings("span")[1]).html());
        });
        $("#count").html(n);
        $("#countMoney").html(m);
    })
</script>
```

下图所示：
![上图所示](https://img-blog.csdnimg.cn/20190923213335781.png)











