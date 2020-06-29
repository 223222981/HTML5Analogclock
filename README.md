HTML5-模拟时钟  
经过上一个太阳系的例子，对canvas动画有了一定的了解，这次看这个模拟时钟的例子的时候感觉比较流畅，接下来对这个例子进行分析。
和上个太阳系的例子一样，HTML部分还是只有一个canvas,在 javascript部分，首先调用document.getElementById()方法获取canvas对象，然后调用getContext(“2d”)方法获得canvas在HTML5中的实体对象ctx。然后就开始绘制了。这一部分的代码看起来很复杂，原因是在draw方法里面只有一个方法，而且requestAnimationFrame调用了两次，于是我为了看起来舒服点，改了一下代码，将draw()方法里的requestAnimationFrame方法头去掉，只留下两个绘制的方法和再次调用requestAnimationFrame的方法，然后在获取了ctx对象之后直接调用requestAnimationFrame(draw),这样看起来就好多了。
然后我们来看一下draw()方法，draw()方法里面有三个方法，一个方法绘制表盘，一个方法绘制指针，一个方法用于重复调用draw()方法。首先来看绘制表盘的方法，首先调用clearRect()清空canvas内的所有内容，然后调用save方法保存当期那状态，然后调用translate()方法将坐标原点移到中心，并画一个圆，接下来开始绘制刻度，采用for循环依次绘制60个刻度，每次绘制前首先保存当前状态（坐标原点为表盘中心且没有旋转），然后根据度数进行旋转，每个刻度是6度，当刻度值可以被5整除的时候标红加粗，绘制完之后调用restore方法取出上一次保存的状态，也就是坐标原点为表盘中心且没有旋转的状态。绘制完60个刻度之后，再次调用restore()方法恢复状态为坐标原点为左上角的点的状态。绘制完棋盘，再来绘制指针，要想绘制指针，首先要知道只针的角度，我们可以通过new Date()获取当前时间，然后分别用getSeconds,getMinutes,getHours获取当前的时分秒的值，然后根据时分秒的值计算出时分秒针的角度，然后就可以画时分秒针了。在画时分秒针的时候，首先要调用save()方法保存当前状态，然后将坐标原点移至表盘中心，根据角度对坐标系进行旋转，然后就可以绘制指针了。画完一个指针后调用restore()恢复原来的状态，继续绘制下一个指针。大功告成。