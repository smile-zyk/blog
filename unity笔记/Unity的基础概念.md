# unity的基本概念

## 编辑器界面
![QQ截图20201020221453.png](https://i.loli.net/2020/10/20/VczryGMfatNQ7oH.png)
## Scene View的操作方法
### 移动自己
- 位移:MMB(Middle mouse button)
- 旋转:RMB
- 缩放:Scroll MMB
- fly mode:RMB+WASDQE
> - lock rotate(focus):f->alt+LMB

### 移动物体
- 检视模式:Q
- 位移:W
- 旋转:E
- 缩放:R

## Unity工作流程
- Assets(资源)+场景结构+节点属性  
Unity的工作流程实际上就是整合资源来构成多个场景(关卡)，美术提供美术资源来搭建场景，策划来具体搭建场景(关卡)并调整场景中物品(节点)的属性，程序员则为物品的属性写脚本来实现功能。  

### 如何导入导出资源
- 导入资源
    1. 方法一: 直接把需要的资源文件拖拽到Unity的资源管理器中
    2. 方法二: 把资源文件拖拽到项目文件夹中的Assets文件夹中，Unity会自动把该文件夹中的内容同步到资源管理器中。
- 导出资源   
Unity中的资源(例如:prefabs)很多都是和其他资源有着一些依赖关系的，因此如果要导出(export)资源，单纯的把该资源拖拽出去是不可以的，我们可以右击要导出的资源，选择Export package,弹出的窗口中会自动整合该资源所依赖的其他资源，选择Export即可导出。  
![QQ截图20201021135906.png](https://i.loli.net/2020/10/21/aRZjEH9h8VxA3rn.png)  
![QQ截图20201021135927.png](https://i.loli.net/2020/10/21/mDKUvEk24RfNMAG.png)
> 导出的资源后缀为.package

### 如何创建场景
Unity工作的一个重要概念是:**Unity制作的游戏都是由一个一个场景(关卡)构成的！**，所谓的游戏就是在一个一个场景(Scene)切换。  
在Unity中创建场景只需要点击工具栏(ToolBar)中的File，选择New Scene即可创建一个新的场景，并编辑这个场景。
![微信截图_20201021141133.png](https://i.loli.net/2020/10/21/sij4HD7ykFzmBgZ.png)
> 注意Unity中的场景文件后缀为.unity，这也侧面说明了场景在Unity制作游戏过程中的重要性！

## Unity的编程思想:组件化编程
### 什么是组件化编程
以Unity为例子，**Unity中的每个对象(GameObject)，都是由一个个组件(Component)构成的**，一个对象具有什么样的性质，就必须有对应的组件来实现这个性质。  
比如说游戏中的Main Camera对象之所以能称为一个摄像机是因为他有一个名为Camera的组件来实现相机的功能，并且使其具有一些相机应有的属性(这些属性可以在Inspector View中的对应组件修改)。  
![QQ截图20201021142917.png](https://i.loli.net/2020/10/21/RmiXqoMZtIhjdev.png)

### Transform组件
我们可以尝试创建一个空对象，右击Hierarchy(树状列表)，选择Create Empty，即可创建一个空的GameObject，但神奇的是，这个空的GameObject的组件并不是空的，而是拥有一个Transform组件。  
![QQ截图20201021144531.png](https://i.loli.net/2020/10/21/HUydkhGOZrTvmDP.png)  
Transform组件是每个对象中最重要的组件，我们可以把对象中所有的组件都删除(Remove),但是唯独不可以删除Transform组件。这是因为如果一个对象连位置都没有的话就没有任何意义了(也无法设置其父子对象)。

### 如何添加、编辑、禁用组件
- 添加组件，点击要添加组件的Inspector View末尾的Add Component，选择自己想要添加的组件(既可以添加Unity自带的组件，也可以添加自己编写的组件)
- 编辑组件，每个组件往往都有自己的属性，我们可以在Inspector View中的对应Component中修改
- 禁用组件，在Inspector View把组件前面的√去掉即可禁用该组件。

### 创建自己的组件
- Unity实际上自带了很多普适组件，但是如果要做出自己独一无二的游戏或者实现一些必要的逻辑，我们必须要自己编写属于自己的组件。
- 在资源管理器中右击选择Create->C# Script即可创建一个C# Script文件，打开后进入VS即可编写自己的逻辑。
> 注意脚本文件名(组件名)必须和文件内的class名一样，否则会无法通过编译。
- 关于如何编写Unity的C#脚本会在后续的笔记里补充。

## Unity的重要概念:预置(Prefabs)
具体参考:[为Unity3D创建素材（3）：预设物体（Prefab）-shimmery](https://www.jianshu.com/p/73f3d471d309).  
PS:这篇博客写的很详细很棒，我觉得就不用重复写了。(主要是觉得写的可能也没人家的好)

## Tag & Layer & Sorting Layer
用于标记GameObject，但用途各有不同。
### 如何添加
1. Edit->Project Settings->Tags and Layers  
![微信截图_20201027161823.png](https://i.loli.net/2020/10/27/tVQiNkEnKsRmTfP.png)
2. Inspector View->Tag/Layer->Add Tag/Layer  
![微信截图_20201027161622.png](https://i.loli.net/2020/10/27/RSnfDrWPIMUl3LJ.png)

### Tags 标签
**标签 (Tags)** 是标记值，可用于标识项目中的对象  
标签有助于识别游戏对象以便于编写脚本。通过使用标签，不需要使用拖放方式手动将游戏对象添加到脚本的公开属性，因此可以节省在多个游戏对象中使用相同脚本代码的时间。  
标签对碰撞体控制脚本中的触发器很有用；例如，需要通过标签确定玩家是否与敌人、道具或可收集物进行交互。  
通过设置 GameObject.FindWithTag() 函数，可以查找包含所需标签的游戏对象。  

### Sorting Layers 排序图层
渲染层序，在上面图层的先渲染但是会被下面的图层覆盖。多用于2d游戏

### Layers 图层
Layer的作用主要有三个
1. 控制相机的渲染物品(通过设置Camera中的Culling Mask属性来选择是否渲染该物品)
2. 控制光线的照射忽略某些层中的物体(通过设置Light中的Culling Mask 来实现)
3. 基于层的碰撞检测  
通过基于层的碰撞检测，可以让某个游戏对象与另一个设置为特定层或多个层的游戏对象发生碰撞。  
通过Edit->Project Seting->Physics中的Layer Collision Matrix来设置  
![微信截图_20201027165259.png](https://i.loli.net/2020/10/27/vAJG4ilra7OCdRL.png)

## Inspector View-如何在自己写的component里添加编辑属性
- 在脚本类中声明public变量，即可在Inspector View中查看该变量。
- 在脚本类中声明的private和protected变量，无法在inspector中查看和修改
- 在变量声明前加[HideInInspector]可以使public变量隐藏
- 在变量声明前加[SerializeField]可以使private和protected在inspector中暴露。
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class test : MonoBehaviour
{
    //public 可以在inspector中查看和设置
    public int a;
    public List<int> m;
    public string s;

    //private和protected不可以在inspector查看和设置
    private int b;
    protected int c;
    //在要定义的变量前加入[HideInInspector]可以隐藏public变量
    [HideInInspector]
    public int d;

    //在要定义的变量前加入[SerializeField]可以显示private和protected变量
    [SerializeField]
    private Color color;

    void Start() { }
    void Update() { }
}
```
![QQ截图20201027194919.png](https://i.loli.net/2020/10/27/ICvrxay16BWqGgf.png)