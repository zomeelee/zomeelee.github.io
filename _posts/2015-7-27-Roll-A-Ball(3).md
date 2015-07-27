---
layout: post
title: Unity官方教程学习笔记之Roll A Ball篇---（三）创建并移动小球
---


小球准备出场了！  

1.我们在Hierarchy标签页下，选择Create-3D Object-Sphere，创建一个球体，更改其名称为Player。

![1.png]({{ site.baseurl }}/images/Roll-A-Ball/part3/1.png "create sphere")  

2.默认情况下，小球的球心在原点，为了能让小球在地面上完整的显示，我们应该适当的调高小球的Y值，选中Player，我们将其Position中的Y值修改为0.5。  

![2.png]({{ site.baseurl }}/images/Roll-A-Ball/part3/2.png "modify position")

   这样，小球就可以完整的显示在地面上。

![3.png]({{ site.baseurl }}/images/Roll-A-Ball/part3/3.png "modified position")

3.通过键盘控制小球的运动

 3.1 添加Rigidbody  
     什么是Rigidbody? 简言之，Rigidbody可以通过物理仿真来控制对象的位置变化，如果我们为一个对象添加了Rigidbody这个Component， 那么这个对象的运动将会受Unity的物理引擎的控制。我们选中Player，在Inspector中点击Add  Component， 然后选择Rigidbody，这样，我们就为Player添加好了Rigidbody。  

![4.png]({{ site.baseurl }}/images/Roll-A-Ball/part3/4.png "add rigidbody")

3.2 添加脚本  
大部分的控制行为都需要脚本来实现，因此，我们需要为Player添加一个脚本，实现通过键盘控制小球运动的功能。选中Player，在Inspector中点击Add Component，然后选择New Script，我们将新的脚本命名为PlayerController，Language选择C Sharp，点击Create And Add，这样，我们就为Player添加了一个叫做PlayerController的脚本。  

为了更好的管理脚本，我们在Project标签页下，选择Create-Folder，新建一个文件夹，命名为Scripts，专门用来放置脚本文件，然后，我们将刚刚创建的PlayerController脚本拖拽到Scripts文件夹下。  

![5.png]({{ site.baseurl }}/images/Roll-A-Ball/part3/5.png "add script")


3.3 实现通过键盘控制小球的运动  
双击PlayerController脚本，这会自动打开Mono Develop集成开发环境，接下来，我们就可以对PlayerController脚本进行编辑。  
首先，我们移除Unity默认为我们生成的两个方法，Start()和Update()。
然后，我们在其中添加如下代码：  

    private Rigidbody rb;
    // Use this for initialization
    void Start ()
    {
        rb = GetComponent<Rigidbody> ();                                   （1）
    }

    void  FixedUpdate()                                                    （6）
    {
        float moveHorizontal = Input.GetAxis ("Horizontal");               （2）
        float moveVertical = Input.GetAxis ("Vertical");                   （3）

        Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);（4）    

        rb.AddForce (movement);                                            （5）
    }


对以上代码稍作解释：  
(1)获取该对象所附加的Rigidbody，并存放在rb中  
(2)获取水平方向(x轴)上的值，返回值的范围为-1到1之间    
(3)获取垂直方向(z轴)上的值，返回值的范围为-1到1之间  
(4)将x、y、z轴上的值合成为一个三维向量，y轴方向上没有运动量，故为0.0  
(5)给三个坐标轴添加力的作用，以驱动小球运动  
(6)注意这里使用的是FixedUpdate()而不是Update()，这主要是因为物理更新会以固定的时间间隔来执行，这与每一帧都会执行的Update()并不一致，Update()更新的时间间隔不固定。因此，FixedUpdate()更适合于物理方面的更新。  


保存代码，回到Unity，点击播放按钮，我们按下方向键或WASD，你会发现小球在你的控制下左右来回运动了！Congratulations!  

不过，稍有欠缺的是，我们会发现小球运动的太慢了，我们想让它快点再快点，该怎么做？实际上，我们只需添加一个变量，控制小球运动的速度即可。 

    public float speed; 
    private Rigidbody rb;
    // Use this for initialization
    void Start ()
    {
        rb = GetComponent<Rigidbody> ();
    }

    void  FixedUpdate()
    {
        float moveHorizontal = Input.GetAxis ("Horizontal");
        float moveVertical = Input.GetAxis ("Vertical");

        Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);

        rb.AddForce (movement * speed);
    }


我们声明了一个public变量speed，该变量用来调节施加在小球上的力的大小。在Unity中，public类型的变量会自动出现在Inspector中，这样，我们就可以随时设置和更改该变量的值了。我们将speed的值设为10，重新点击播放，按下方向键，我们会发现，小球比之前运动的快多了！  

![6.png]({{ site.baseurl }}/images/Roll-A-Ball/part3/6.png "speed movement")  


至此，我们已经可以控制小球运动了！
----
****