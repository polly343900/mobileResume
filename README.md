# mobileResume
---
[DEMO](http://polly343900.github.io/mobileResume/index.html)

1.zepto.fullpage.js
  使用了[颜海镜的zepto.fullpage.js](https://github.com/yanhaijing/zepto.fullpage)。
  但修改了部分代码。主要在touchend事件上，源代码：
  
  ```javascript
  $this.on('touchend', function (e) {
                e.preventDefault();
                if (that.movingFlag) {return 0;}
                
                var sub = e.changedTouches[0].pageY - that.startY;
                var der = (sub > 30 || sub < -30) ? sub > 0 ? -1 : 1 : 0;

                that.moveTo(that.curIndex + der, true);
            });
  ```
  `e.preventDefault();`是为了使能在安卓浏览器上流畅滑动。但同时也使得页面的链接无法跳转。
  奇怪的是，不把`e.preventDefault();`放在第一行的话，页面的链接可以通过双击（tap两次屏幕）跳转。这样交互就不好了。:(
  最后采取的办法是：去除了`touchend`事件。用`touchmove`事件代替。代码如下:
  
  ```javascript
  $this.on('touchmove', function (e) {
                e.preventDefault();
                if (that.movingFlag) {return 0;}
                
                var sub = e.changedTouches[0].pageY - that.startY;
                var der = (sub > 5 || sub < -5) ? sub > 0 ? -1 : 1 : 0;
                that.moveTo(that.curIndex + der, true);
            });
  ```
  我对`touchmove`的理解是“对屏幕按压的移动”行为，所以常用来监听“拖拽”。而当变化的距离比较小（大于或小于5）时，我感觉，就跟滑动页面的行为相似了。
  
  实践方面，几乎感觉不出差别，但偶尔有滑动不灵的时候。
  
2.canvas.js
  通过canvas来绘制技能表。本来想直接使用e-charts。后来想还是练练吧。感觉还行。哈哈哈哈。。。
  
  就是在canvas已经绘制好了时候翻转手机屏幕的话，页面就T_T..所以canvas的宽度设置成了300，这样在（手机屏幕分辨率宽度>=320)横屏的时候不至于太难看。

  因此在webview横屏查看时，就是个渣渣啊。。T_T
