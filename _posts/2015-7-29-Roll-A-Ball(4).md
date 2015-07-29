---
layout: post
title: Unity官方教程学习笔记之Roll A Ball篇---（四）移动照相机并跟踪小球的运动
---

我们想要在小球运动的时候，照相机可以实时跟踪小球的位置，不至于让小球出了我们的视线，这该如何实现呢？  

我们知道，小球和照相机之间有一段偏移量，这个偏移量我们很容易算出来，当小球在不断的运动时，我们通过小球运动后的位置加上这个偏移量，就可以得到照相机当前应该在的位置。基于这个思路，我们就可以移动照相机并跟踪小球的运动了。  

##1.首先，我们为照相机添加脚本，命名为CameraController。  
我们移除默认的代码，在其中添加如下代码：  

    public GameObject player;                                            (1)

    private Vector3 offset;
    void Start()
    {
        offset = transform.position - player.transform.position;         (2)
    }

    void LateUpdate()                                                    (3)
    {
        transform.position = offset + player.transform.position;         (4)
    }


对以上代码的解释：  
(1)小球对象的引用  
(2)计算小球和相机之间的偏移量  
(3)此处，我们使用LateUpdate()， 而不用Update()，LateUpdate()在所有的Update()执行完之后调用，因此，可以确保小球的位置已经得到了更新。  
(4)小球移动后的位置加上其与相机之间的偏移量即可得相机新的位置  

##2.调整相机的位置和角度  
我们选中MainCamera，更改其Position中的Y值为10，更改其Rotation中的X值为45。  

![1.png]({{ site.baseurl }}/images/Roll-A-Ball/part4/1.png "set camera")

这样，照相机就可以以比较好的角度对准场景。  

![2.png]({{ site.baseurl }}/images/Roll-A-Ball/part4/2.png "camera has been set")

##3.将小球Player赋值给CameraController中变量的Player  
我们在Hierarchy中选中MainCamera，然后将Player拖动到CameraController脚本的Player变量上，这样小球就与照相机关联起来了。 

![3.png]({{ site.baseurl }}/images/Roll-A-Ball/part4/3.png "associate player with camera")

点击播放，我们会发现，照相机已经可以跟随小球一起移动了！

![4.png]({{ site.baseurl }}/images/Roll-A-Ball/part4/4.png "camera move with player")


----
****