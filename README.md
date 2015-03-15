# mobileResume
---
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
  e.preventDefault()是为了使能在安卓浏览器上流畅滑动。但同时也使得页面的链接无法跳转。
  奇怪的是，不把e.preventDefault()放在第一行的话，页面的链接可以通过双击（tap两次屏幕）跳转。这样交互就不好了。:(
  最后采取的办法是：去除了touchend事件。用touchmove事件代替。详情见代码。滑动方面，几乎感觉不出差别，但还是有滑动不灵的时候。
  
2.canvas.js
  通过canvas来绘制技能表。本来想直接使用e-charts。后来想还是练练吧。感觉还行。哈哈哈哈。。。
  就是在canvas已经绘制好了时候翻转手机屏幕的话，页面就T_T..所以canvas的宽度设置成了300，这样在（手机屏幕分辨率宽度>=320)横屏的时候不至于太难看。
