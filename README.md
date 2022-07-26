# Unity_study_mms🎏

unity项目长时间跑CPU+内存+GPU会挂满，调试完后记得按暂停键关闭调试！！！！！



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

教程跟的[【新手小白C#和Unity入门】01__小球运动（1）](https://www.bilibili.com/video/BV1EB4y1p7ti?vd_source=8368ed6f218b06921448305928410b44)和[【新手小白C#和Unity入门】02__小球碰撞，关于碰撞触发onTriggerEnter（2）](https://www.bilibili.com/video/BV1FS4y1n7cB?vd_source=8368ed6f218b06921448305928410b44)

unity里复制某个东西是CTRL+D

确定摄像视角：层级-点击main camera，调整角度后CTRL+shift+F

小球的代码部分如下：

```c#
using System.Collections;
using System.Collections.Generic;
using TMPro;//UI
using UnityEngine;  //引入命名空间

public class test : MonoBehaviour
{
    Rigidbody rb;//重力初始化，使用前：层级 - 小球  检查器拉到最下面 - 添加组件 - 搜索栏输入Rigidbody
    Vector3 move;
    public float speed = 3f;
    //public GameObject playerTest;//文字win。层级右键-UI-文本.写完后要记得小球的检查器-脚本-把对应文字的层级拉到Player Test
    public TextMeshProUGUI number;
    private int count = 0;//统计数据用
    void Start()    //开始调用
    {
        /*Destroy(gameObject, 4f);//4秒后消失*/
        rb = GetComponent<Rigidbody>(); //初始化
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))//如果按到空格键
        {
            rb.AddForce(Vector3.up * 150);//给它150向上的力，展现出“弹跳”的效果。Vector3是力的方向
        }
        //asdw上下左右控制
        move.x = Input.GetAxis("Horizontal");//水平Horizontal=a或s键，可以在unity项目-编辑-项目设置-输入管理器-轴线-水平查看
        move.z = Input.GetAxis("Vertical");//垂直Vertical=w或d键，可以在unity项目-编辑-项目设置-输入管理器-轴线-垂直查看
        move = new Vector3(move.x, 0, move.z);
        rb.AddForce(move * speed);
    }




    //碰撞
    //OnCollisionEnter方法是在两个物体都 不 勾选i"是触发器"的前提下才能进入
    //反之只要勾选一个isTrigger那么就能进入OnTriggerEnter方法
    //OnCollisionEnter和OnTriggerEnter是冲突的不能同时存在的。

    /*private void OnTriggerEnter(Collider collision)
    {
        if (collision.gameObject.tag == "emery")//中间多出来的一个小立方体已经如下设置：
                                                //检查器-新建标签名字为emery-box collider中心大小设置好，勾选上“是触发器”
        {
            Destroy(collision.gameObject);//方块消失
            //Destroy(gameObject);//小球消失
        }
    }*/
    private void OnTriggerEnter(Collider collision)//不勾选“是触发器”
    {
        if (collision.gameObject.CompareTag("emery"))
        //和上面collision.gameObject.tag == "emery"的写法是一样的
        //中间多出来的一个小立方体已经如下设置：
        //检查器-新建标签名字为emery-box collider中心大小设置好，取消“是触发器”
        {
            Destroy(collision.gameObject);//方块消失
            //Destroy(gameObject);//小球消失
            //playerTest.SetActive(true);//显示文字win。
                                       //要记得先把文字的检查器中，最上面检查器和标签之间有个√取消掉
            
            count++;
            show_of_number();
        }
    }

    //处理碰撞数据
    private void show_of_number()
    {
        number.text = "COUNT:" + count;
        if (count >= 3)
        {
            number.text = "COUNT has >= 3";
        }
    }

}
```

[CSDN_unity角色总掉到地面以下](https://blog.csdn.net/qq_34060370/article/details/124243699)

[为什么UI下的text文件无法拖动到脚本](https://tieba.baidu.com/p/7625369037)

