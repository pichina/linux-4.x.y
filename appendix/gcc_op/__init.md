__init
========================================

使用这个宏声明的函数，编译时就会把目标代码放到段.init.text里，这段都是放置初始化的代码。

```
#define __init		__section(.init.text) __cold notrace
```

这个宏定义主要用来标志这个函数编译出来的目标代码放在那一段里。对于应用程序的编译和连接，
不需要作这样的考虑，但是对于内核代码来说，就需要了，因为不同的段代码有着不同的作用，
比如初始化段的代码，当系统运行正常以后，这段代码就没有什么用了，聪明的做法就是回收这
段代码占用的内存，让内核的代码占最少的内存。还有另外一个作用，比如同一段的代码都是编译在一起，
让相关联的代码尽可能同在一片内存里，这样当CPU加载代码到缓存时，就可以一起命中，提高缓存的
命中率，这样就大大提高代码的执行速度。