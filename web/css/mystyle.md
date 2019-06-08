- 加载中的图片:在屏幕正中央显示
```
.loading {
  position: fixed; //位置被设置为 fixed 的元素，可定位于相对于浏览器窗口的指定坐标
  display: none;  // 默认不显示,可以使用jquery显示或隐藏$(.loading).show()/hide()
  top: 0; // 指定位置
  left: 0;
  width: 100%; // 占据屏幕的大小百分比
  height: 100%;
  z-index: 100; // z-index 属性设置元素的堆叠顺序。拥有更高堆叠顺序的元素总是会处于堆叠顺序较低的元素的前面。
  transition: all .8s; // 变化速度,每种变化(显示\缩放\隐藏)的时间
  background: rgba(0, 0, 0, .6) url(../img/loading.gif) no-repeat; //指定背景颜色\透明度\图片url\是否使用重复填充
  background-position: center center; // 背景在正中央
  background-size: 100px auto;  // 背景大小:指定宽度,高度自动调整,即原比例缩放
}
```

- 开关 switch
```
<div class="" data-control="BOX" id="Box_points_switch">
    <label><input class="mui-switch mui-switch-anim" type="checkbox" id="switch"></label>
</div>

/*switch开关*/
.mui-switch {
    width: 5em;
    height: 3.2em;
    position: relative;
    border: 1px solid #dfdfdf;
    background-color: #fdfdfd;
    box-shadow: #dfdfdf 0 0 0 0 inset;
    border-radius: 3em;
    background-clip: content-box;
    display: inline-block;
    -webkit-appearance: none;
    user-select: none;
    outline: none;
}
.mui-switch:before {
    content: '';
    width: 3em;
    height: 3em;
    position: absolute;
    top: 0px;
    left: 0;
    border-radius: 3em;
    background-color: #fff;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.4);
}
.mui-switch:checked:before {
    left: 2em;
}
.mui-switch.mui-switch-anim {
    transition: border cubic-bezier(0, 0, 0, 1) 0.4s, box-shadow cubic-bezier(0, 0, 0, 1) 0.4s;
}
.mui-switch.mui-switch-anim:before {
    transition: left 0.3s;
}
.mui-switch.mui-switch-anim:checked {
    box-shadow: #64bd63 0 0 0 16px inset;
    background-color: #64bd63;
    transition: border ease 0.4s, box-shadow ease 0.4s, background-color ease 1.2s;
}
.mui-switch.mui-switch-anim:checked:before {
    transition: left 0.3s;
}


$("#switch").change(function() {
    if ($("input[type='checkbox']").is(':checked') == true) {
        alert("ON");
    } else {
        alert("OFF");
    }
});

```
