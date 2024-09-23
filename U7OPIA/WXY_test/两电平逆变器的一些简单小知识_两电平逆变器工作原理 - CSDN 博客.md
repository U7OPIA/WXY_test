> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_45603496/article/details/124236544)

今天讨论一点小 “姿势”，解决一些小白的入门问题，欢迎有问题互相交流。

经常有人问，“哎，两电平[逆变器](https://so.csdn.net/so/search?q=%E9%80%86%E5%8F%98%E5%99%A8&spm=1001.2101.3001.7020)为什么叫两电平，体现在哪里？”“为什么相电压又是五电平？”“线电压又是三电平呢？”  下面就一一进行讲解。

本文采用的是两电平逆变器，O 点为虚拟的直流侧电压中点，N 点为 [PMSM](https://so.csdn.net/so/search?q=PMSM&spm=1001.2101.3001.7020) 的中性点，实际中可能 O 点无法给出。这里取了一个 G 点，为地。

![](https://i-blog.csdnimg.cn/blog_migrate/69e2dbd82acf35fe109f3b356549c377.png)

何为 “两电平” 呢？其实是指，逆变器的输出端电压 Uao、Ubo、Uco 的电平变化只有两种，要么是 + Udc/2，要么为 - Udc/2。如果看作 Uag、Ubg、Ucg 呢，就是输出要么为 + Udc，要么为 0。把逆变器输出端的电平变化数量称作几电平，同理有 “三电平”、“五电平” 等等。

#### 那么为什么相电压和线电压的电平数又不一样了呢？

对于相电压电平数不一样的原因，是由于 Ung 不为 0，也就是负载中性点 N 与大地 G 之间有电势差。接下来对其进行[数学分析](https://so.csdn.net/so/search?q=%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90&spm=1001.2101.3001.7020)

我们采用公式推导出 Ung 的大小

![](https://i-blog.csdnimg.cn/blog_migrate/f9ecba4295d342b2e0f528b8f7209725.png)

 ![](https://i-blog.csdnimg.cn/blog_migrate/f2056cd1d63c9ab52bf93af25cc66109.png)

![](https://i-blog.csdnimg.cn/blog_migrate/6dd64a709f13e6bde5f70e8be3c63342.png)

 即可推出

![](https://i-blog.csdnimg.cn/blog_migrate/382814df9ef411eb7bea18096771a263.png)

可以看出，Ung 的大小就是跟逆变器的输出端电压有关系，为其平均值。这里的 Ung 还称为逆变器的共模电压。

 我们搭建 simlink 仿真验证一下

Uag 为两电平

![](https://i-blog.csdnimg.cn/blog_migrate/9b071f5429e4af7c72c1462d9e1ef8e6.png)

 Ung 为四电平，通过上面推导的 Ung 公式可以直接计算出对应的四电平的电压值

![](https://i-blog.csdnimg.cn/blog_migrate/37600d3f4d24219830fdf64f331ac794.png)

   Uan=Uag-Ung，组合过后相电压为五电平

 ![](https://i-blog.csdnimg.cn/blog_migrate/257b575f820c6e213f231ef5c57db29f.png)

而对应的线电压的电平数为 3，就更简单了，直接数学的组合关系。Uag 电压值存在两种可能，Udc 和 0；Ubg 的电压值也一样，Udc 和 0。两两组合可得，共有 3 种可能：Udc，0，-Udc。

![](https://i-blog.csdnimg.cn/blog_migrate/902feb64863355b4e0f373153db41fa0.png)

 以上就是解释了 “两电平” 逆变器的一些相关小问题。