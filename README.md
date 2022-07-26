# Unity_study_mms🎏

==unity项目长时间跑CPU+内存+GPU会挂满，调试完后记得按暂停键关闭调试！！！！！==



## 安装

> 心理准备：安装过程特别烧CPU+内存+GPU，使用过程特别烧内存，很容易到2+GB，平时大概1-1.7GB，再开个VS和浏览器视频，内存直接升天

已有：VS2019，可以正常运行C家族的程序



去unity官网（我进的时候要挂梯子）下载personal版本（学生版本需要两天的检验，也可以尝试），下载前需要注册

语言：UnityHub - 安装 - 2021.3.6f1c1右边有个设置的图标 - 添加模板(如果已经有VS了就不要下载里面的VS了)

当跑unity的C#代码的时候，VS2019最上面一栏 - 工具 - 获取工具和功能 - 勾选unity - 点击右下角修改（大概几百MB）

unity项目 - 最上面一栏 - 第二个编辑 - preferences - language改成中文

unity项目 - 最上面一栏 - 第二个编辑 - preferences - 外部工具- 外部脚本编译器改成VS2019



[Unity 教程 | 10分钟入门三维旋转的多维数据集 | .NET (microsoft.com)](https://dotnet.microsoft.com/zh-cn/learn/games/unity-tutorial/intro)是Micorsoft官方的下载+小球教程，但会有一些奇奇怪怪的地方



## 小球运动

教程跟的[【新手小白C#和Unity入门】01__小球运动（1）](https://www.bilibili.com/video/BV1EB4y1p7ti?vd_source=8368ed6f218b06921448305928410b44)



unity里复制某个东西是CTRL+shift+D

确定摄像视角：层级-点击main camera，调整角度后CTRL+shift+F

小球的代码部分如下：

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;  //引入命名空间

public class test : MonoBehaviour
{
    Rigidbody rb;//重力初始化，使用前：层级 - 小球  检查器拉到最下面 - 添加组件 - 搜索栏输入Rigidbody
    Vector3 move;
    public float speed = 3f;
    void Start()    //开始调用
    {
        /*Destroy(gameObject, 4f);//4秒后消失*/
        rb = GetComponent<Rigidbody>(); //初始化
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))//如果按到空格键
        {
            /*Destroy(gameObject);//直接消失*/
            rb.AddForce(Vector3.up * 150);//给它150向上的力，展现出“弹跳”的效果。Vector3是力的方向
        }
        //asdw上下左右控制
        move.x = Input.GetAxis("Horizontal");//水平Horizontal=a或s键，可以在unity项目-编辑-项目设置-输入管理器-轴线-水平查看
        move.z = Input.GetAxis("Vertical");//垂直Vertical=w或d键，可以在unity项目-编辑-项目设置-输入管理器-轴线-垂直查看
        move = new Vector3(move.x, 0, move.z);
        rb.AddForce(move * speed);
    }

}
```

