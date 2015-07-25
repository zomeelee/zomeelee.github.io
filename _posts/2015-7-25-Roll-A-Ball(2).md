---
layout: post
title: Unity官方教程学习笔记之Roll A Ball篇---（二）创建地面
---


本节我们会创建一个平面用作地面，小球可以在上面任意滚动。  

1.首先，我们选择GameObject-3D Object-Plane 创建一个平面，  

![1.png]({{ site.baseurl }}/images/Roll-A-Ball/part2/1.png "create plane")


当然，我们也可以通过另一种方式来创建平面， 在Hierarchy标签页下，选择Create-3D Object-Plane

![2.png]({{ site.baseurl }}/images/Roll-A-Ball/part2/2.png "create plane2")  


平面创建完成后，我们更改其名字为Ground（在Hierarchy下选中Plane，然后按下return即可修改）。然后，我们更改Ground的尺寸大小，我们选中Ground，在Inspector标签页下，我们可以看到有一个叫Transform的Component, 它有三个属性Position、Rotation、Scale，分别表示对象的位置、旋转角度、缩放比例。我们将Scale中的X、Z值修改为2，这意味着我们将Ground沿X、Z方向均拉伸到了原来的两倍。  

![3.png]({{ site.baseurl }}/images/Roll-A-Ball/part2/3.png "scale ground")



2.接下来，我们为Ground添加材质

在Project标签页下，选择Create-Folder，我们先新建一个文件夹，取名为Materials，用来管理材质。然后，在Materials被选中的情况下，我们继续选择Project下的Create-Material，创建一个新材质，我们将新材质命名为Ground。  

![4.png]({{ site.baseurl  }}/images/Roll-A-Ball/part2/4.png "add material")


选中Ground材质，我们在右边的Inspector中找到Albedo，更改其颜色为R:0, G:32, B:64。

![5.png]({{ site.baseurl }}/images/Roll-A-Ball/part2/5.png "set color")

然后，我们在Project标签页下，选中Ground，将其直接拖拽到Scene View中Ground平面上，这样，材质Ground就被添加到了平面Ground上了。

![6.png]({{ site.baseurl }}/images/Roll-A-Ball/part2/6.png "assign material")

这样，地面就创建好了，接下来该小球出场了！


----
****