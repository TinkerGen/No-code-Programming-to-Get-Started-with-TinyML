## 项目概述

在这节课中，我们将要进行一个手势识别的任务，也就是尝试运用 Wio Terminal 的内置的三轴加速度计来识别三种手势，包括翻转，挥动以及静止。

![L02-image-01.png](/Lesson-02/images/L02-image-01.png)

如果使用基于算法的传统编程手段，这将会非常棘手。对于传统编程的机器来说，手势必须以完全相同的方式执行才能被识别，而这在现实当中几乎不可能，其中涉及众多因素，以运动因素为例：我们手势的摆动速度、转动角度以及静置方向，严格意义上来说都不会完全相同，而这些微小变化都需要使用传统编程来制订一套规则以减少识别错误。所以如果同样使用传统编程来解决这个手势识别问题时，就需要为每种操作模式制定数百条不同的规则。
值得庆幸的是，**机器学习**可以非常简单的处理这些变化，而不需要冗杂的规则程序。

### 预期结果

Wio Terminal 实时显示当前 Wio Terminal 动作的识别结果：翻转、挥动以及静止。

![L2 xinjia1.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631959918188-5bc10e1a-e15d-4660-92cc-9d3c3e3c4b4d.png#clientId=uc1db889d-9af8-4&from=drop&id=u6d7ee260&margin=%5Bobject%20Object%5D&name=L2%20xinjia1.png&originHeight=129&originWidth=204&originalType=binary&ratio=1&size=48450&status=done&style=none&taskId=u6d63cb36-ca18-4574-b932-889c3f94aaa)![L2 xinjia2.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631959923058-8fcca095-7c68-4b92-8d55-bbc6d9bb42c8.png#clientId=uc1db889d-9af8-4&from=drop&id=ue6a2f99a&margin=%5Bobject%20Object%5D&name=L2%20xinjia2.png&originHeight=129&originWidth=204&originalType=binary&ratio=1&size=45385&status=done&style=none&taskId=u8f01c406-1667-45bf-905d-27e277a6a45)![L2 xinjia3.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631959924769-37a19fd1-8e48-4c4a-b753-90e9e31d3781.png#clientId=uc1db889d-9af8-4&from=drop&id=uc9ea62f7&margin=%5Bobject%20Object%5D&name=L2%20xinjia3.png&originHeight=129&originWidth=204&originalType=binary&ratio=1&size=47354&status=done&style=none&taskId=uaec10d63-7eb0-490a-b7de-c5487740cdf)

### 准备工作

硬件需求：Wio Terminal
连接方法：
​

​

![L2 b.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631155437641-ed075382-2029-4baa-923c-89dde8ddd6d0.png#clientId=ub79295a2-fc7f-4&from=drop&height=308&id=u9ea89eff&margin=%5Bobject%20Object%5D&name=L2%20b.png&originHeight=1264&originWidth=2368&originalType=binary&ratio=1&size=310468&status=done&style=none&taskId=uc0cc46b4-d462-4c60-9431-fcc02afcbda&width=577)

## 背景知识

可能正如你想的那样，加速度计是用来测量一个物体加速度的传感器，它的输出结果来自物体的速度变化。加速度计可以测量速度随时间的变化，常见的加速度为重力加速度，一个重力加速度等于 9.8 米每平方秒（m/s2），表示每秒钟就有 9.8 米每秒（m/s）的速度在增加或减少。
世界上有很多种加速度的计算测量方法，最早的加速度是由一个机械建筑演变而来的。第一个加速度计是阿特伍德机，它是由英国物理学家乔治·阿特伍德发明的。
​

![L2 c.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631156259451-e5fd4139-8d65-4ac1-896a-47da59c80314.png#clientId=ub79295a2-fc7f-4&from=drop&height=501&id=u2abf4b0e&margin=%5Bobject%20Object%5D&name=L2%20c.png&originHeight=1024&originWidth=583&originalType=binary&ratio=1&size=126510&status=done&style=none&taskId=uc7ba45e1-0410-4d8b-861b-c769a2ad6bc&width=285)
> 下面标记 阿特伍德机

加速度计通常由质量块、阻尼器、弹性元件、敏感元件和适调电路等部分组成，根据传感器敏感元件的不同，加速度计可以分为电容式、压电式等；根据输入轴又可以分为单轴、双轴和三轴。一般使用在手机中的加速度计是微机电系统（Micro-electromechanical systems 简称  MEMS）加速度计，我们在 Wio Terminal 中使用的是就三轴数字加速度计（LIS3DHTR）。
加速度计的原理一般情况下是通过传感器感知受到力的作用，再经过内部电路（电容变化）将受到的力转换为电信号输出。比如 MEMS 加速度计，它的模型其实是一个由弹簧质量块组成的阻尼系统，当质量块由于惯性作用压缩弹簧的时候会产生一个弹性力，将弹簧与内部电路相连，电容会随着弹簧的移动而变化，通过胡克定律和电容变化我们可以知道弹性力与电信号的关系，而后用牛顿第二定律即可用电信号表示加速度。
![L2 g.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631862256939-ba02dc09-1528-4a7d-87c3-1d9d2d04ca40.png#clientId=ubdc1abc9-16b3-4&from=drop&id=u028d50de&margin=%5Bobject%20Object%5D&name=L2%20g.png&originHeight=135&originWidth=438&originalType=binary&ratio=1&size=6773&status=done&style=none&taskId=u891aa1c2-ebaa-4d36-92ab-5487d74e2b4)
>
> 1. 质量块与电极板静置
> 1. 质量块按压电极板使得电容变化，输出电信号

三轴数字加速度计在原理上与 MEMS 加速度计大同小异，另外可以让它测量更加精准的原因是它同时拥有三个传感器来识别三个轴向力的作用。

## 练习与实践

### 课程步骤

1. 创建与选择模型
1. 数据采集
1. 训练与部署
1. 使用与编程

### 步骤1、创建与选择模型

#### 1.1 建立“运动识别（内置加速度计）”模块

点击“创建与选择模型”，然后点击“内置加速度计识别动作”，如下面步骤 1 和步骤 2 所示
![L2 a0.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631936167537-6b7189f2-a92f-4992-9e5c-a17f8baa15f6.png#clientId=u52ce0c5c-b884-4&from=drop&height=474&id=u3d981141&margin=%5Bobject%20Object%5D&name=L2%20a0.png&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&size=252877&status=done&style=none&taskId=u04196e46-a398-4dd5-afb9-8f46ad97f55&width=842)
给新建的模型命名
![L2 b0.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631936335714-aa173179-4a6c-4638-913d-ee2694a699f7.png#clientId=u52ce0c5c-b884-4&from=drop&id=u59e5d4c0&margin=%5Bobject%20Object%5D&name=L2%20b0.png&originHeight=285&originWidth=519&originalType=binary&ratio=1&size=19064&status=done&style=none&taskId=ufbdebd13-72ac-47e9-8723-8d94ec2bb2a)

点击“确认”就会自动跳转到数据采集界面。
![L2 b1.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631936468661-3a0994bc-a554-496d-8fca-70490eda79c3.png#clientId=u52ce0c5c-b884-4&from=drop&id=u2dfe5434&margin=%5Bobject%20Object%5D&name=L2%20b1.png&originHeight=262&originWidth=519&originalType=binary&ratio=1&size=17560&status=done&style=none&taskId=u0f7d156b-9980-4fd0-9d07-cf39e4111eb)

### 步骤 2、 数据采集

#### 2.1 默认标签

![L2 c0.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631936752920-e2fa4ea6-476e-4827-bb93-52ea2a69b4d3.png#clientId=u52ce0c5c-b884-4&from=drop&height=149&id=ub387eb71&margin=%5Bobject%20Object%5D&name=L2%20c0.png&originHeight=296&originWidth=772&originalType=binary&ratio=1&size=13920&status=done&style=none&taskId=u21a8ea77-2d79-431a-aa4e-df388e33470&width=388)
![L2 a.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631960150949-360ac302-95b8-416e-85c0-e592ea99f06f.png#clientId=uc1db889d-9af8-4&from=drop&height=732&id=u38754876&margin=%5Bobject%20Object%5D&name=L2%20a.png&originHeight=935&originWidth=1920&originalType=binary&ratio=1&size=222287&status=done&style=none&taskId=ub76366f7-2f77-4043-919a-0cf4ee5ec01&width=1503)

#### 2.2 连接设备并上传 Codecraft 中的默认数据采集程序

Wio Terminal 连接后，在 Codecraft 界面，点击   ![L2 c2.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631938458699-e31d2bd7-ebd1-4cb3-b286-13639c9a6bf9.png#clientId=u50f391c6-f579-4&from=drop&height=37&id=u75f86823&margin=%5Bobject%20Object%5D&name=L2%20c2.png&originHeight=96&originWidth=413&originalType=binary&ratio=1&size=14854&status=done&style=none&taskId=u665d2c2f-8734-4d1a-839a-485e49e65bd&width=158)  即可上传默认数据采集程序。
![L2 b.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631960256566-8f3e3f28-f6db-4913-b1c1-db558bb78af4.png#clientId=uc1db889d-9af8-4&from=drop&id=ub7d0f3b6&margin=%5Bobject%20Object%5D&name=L2%20b.png&originHeight=935&originWidth=1920&originalType=binary&ratio=1&size=221889&status=done&style=none&taskId=u6785faf9-0903-4150-bf1d-290da18dd82)
如下图所示将出现一个“上传”弹出窗口。
选择与当前 Wio Terminal 对应的串口号（不一定为下图的 COM14），点击“确定”按钮。
![L2 d1.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631938852502-1732ef74-a9e0-4cc4-ab96-1bd0107a1e57.png#clientId=u50f391c6-f579-4&from=drop&id=uc512a8cd&margin=%5Bobject%20Object%5D&name=L2%20d1.png&originHeight=464&originWidth=716&originalType=binary&ratio=1&size=19759&status=done&style=none&taskId=u83f94da7-a88e-4c37-b8ae-9495c8de047)
弹窗会提示正在上传程序，请稍候...
![L2 d2.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631938871090-4b8619f4-ac5b-4bc6-a712-bfc8df3bb629.png#clientId=u50f391c6-f579-4&from=drop&id=ucd8390ec&margin=%5Bobject%20Object%5D&name=L2%20d2.png&originHeight=326&originWidth=398&originalType=binary&ratio=1&size=21802&status=done&style=none&taskId=uc64144f6-a0c0-45ff-ba4c-c70c20c8827)
通常上传需要 10 秒钟。 程序上传后，“上传成功”的窗口将出现在如下图所示的屏幕上
![L2 d3.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631938936345-02fde583-3ff3-465c-9b6d-50cb8fd3c0ef.png#clientId=u50f391c6-f579-4&from=drop&id=u2404f743&margin=%5Bobject%20Object%5D&name=L2%20d3.png&originHeight=262&originWidth=449&originalType=binary&ratio=1&size=16299&status=done&style=none&taskId=u76601d29-3142-4a85-bad9-be7eccd337a)
点击“我知道了”关闭上传成功弹窗，返回编程界面。
![L2e.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631585886827-625d0af8-8824-434b-9259-34fc56826673.png#clientId=ua986330f-4571-4&from=drop&height=36&id=ucbe488ab&margin=%5Bobject%20Object%5D&name=L2e.png&originHeight=35&originWidth=35&originalType=binary&ratio=1&size=1057&status=done&style=none&taskId=u9f4a5f4b-44c6-4f16-8655-08ed1c7d828&width=36)**警告**
在网页版 Codecraft 中，如果您没有安装或运行设备助手，您可能会收到下图中的消息。
![L2 d4.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631939026695-68233421-71c6-4783-be05-b55b8875daab.png#clientId=u50f391c6-f579-4&from=drop&id=u7d93a9ed&margin=%5Bobject%20Object%5D&name=L2%20d4.png&originHeight=533&originWidth=463&originalType=binary&ratio=1&size=72565&status=done&style=none&taskId=u5f6ec642-3ead-4c31-aef7-e35dc3c2d6e)
查看此页面以获取更多信息：[下载、安装和“设备助手”使用](https://www.yuque.com/tinkergen-help-en/codecraft/assistant)。

#### 2.3 数据采集

在右上角的超链接中，您将找到数据采集的分步介绍。请按照说明收集数据。
![L2 c.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631960297742-cbd6918c-2cb8-4fa3-8fcc-03397ad59eef.png#clientId=uc1db889d-9af8-4&from=drop&id=MFSfm&margin=%5Bobject%20Object%5D&name=L2%20c.png&originHeight=935&originWidth=1920&originalType=binary&ratio=1&size=221785&status=done&style=none&taskId=u1f9ac859-bf56-4ae6-88b5-edea6de266b)
注意：

- Wio Terminal 按钮位置。
- 动画是已经加速过的，实际动作可能有所缓慢。
- 请注意红色提示。
- 将光标指向描述文本以获得更详细的内容。

![L2 e0.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631939331914-8c3b1b2f-7fdb-4953-a91b-86d2a1626808.png#clientId=u50f391c6-f579-4&from=drop&height=693&id=u717c64ce&margin=%5Bobject%20Object%5D&name=L2%20e0.png&originHeight=888&originWidth=1172&originalType=binary&ratio=1&size=382057&status=done&style=none&taskId=uf6e39015-cbab-49a4-beaa-fe35baedea9&width=914)
​

![L2 e1.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631939913731-b06a2515-7a58-4b28-9e36-84dda9c36481.png#clientId=u50f391c6-f579-4&from=drop&height=693&id=uc12e5365&margin=%5Bobject%20Object%5D&name=L2%20e1.png&originHeight=888&originWidth=1172&originalType=binary&ratio=1&size=391512&status=done&style=none&taskId=u76db4911-cbd5-4655-b2a0-4eed10e1fe3&width=915)

让我们开始根据 Wio Terminal 显示图标来完成数据采集。

 ![L2f.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631586242194-b58a9a32-6a73-41a7-8738-42818e473162.png#clientId=ua986330f-4571-4&from=drop&height=38&id=u2233291f&margin=%5Bobject%20Object%5D&name=L2f.png&originHeight=151&originWidth=152&originalType=binary&ratio=1&size=62188&status=done&style=none&taskId=u37025d61-7cab-446d-9708-4dc81490786&width=38)这个信号表示正在 Wio Terminal 收集数据。
![L2 e2.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631940001938-a00bface-ae71-4616-8191-e4a0d1d69275.png#clientId=u50f391c6-f579-4&from=drop&height=265&id=u770d0800&margin=%5Bobject%20Object%5D&name=L2%20e2.png&originHeight=513&originWidth=659&originalType=binary&ratio=1&size=275823&status=done&style=none&taskId=u76b2d756-1688-42dc-b0f6-a1d16529cf9&width=340)
![L2g.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631586366412-8eb4ba87-c526-42ca-ae23-8f419fd711ef.png#clientId=ua986330f-4571-4&from=drop&height=43&id=ua1683d9b&margin=%5Bobject%20Object%5D&name=L2g.png&originHeight=88&originWidth=95&originalType=binary&ratio=1&size=23673&status=done&style=none&taskId=u1f53dcc1-16fd-492b-b05e-8c990b0d70f&width=46)OK表示数据收集完成。
![L2h.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631586384489-06237822-9e16-41d3-8180-27ad289e3818.png#clientId=ua986330f-4571-4&from=drop&id=u418b6c5a&margin=%5Bobject%20Object%5D&name=L2h.png&originHeight=257&originWidth=330&originalType=binary&ratio=1&size=47130&status=done&style=none&taskId=udf37c276-7b3c-4c87-8958-b3d602693bf)

Wio Terminal 虽然显示数据采集完成，但 CodeCraft 仍在上传数据，数据从 Wio Terminal 传输到 CodeCraft 需要 1~2s。
至此，数据全部采集完成。
![L2 f.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631940495219-c26fc360-601b-403d-adb7-0787fd9f5442.png#clientId=u50f391c6-f579-4&from=drop&height=462&id=u928eb451&margin=%5Bobject%20Object%5D&name=L2%20f.png&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&size=267609&status=done&style=none&taskId=ua66d3ee8-ba3a-4a42-845b-4851b5ae995&width=822)
单击“训练与部署”。
![L2 f0.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631940550216-95c8ffa9-df89-4450-b990-fd6f9ceb014d.png#clientId=u50f391c6-f579-4&from=drop&height=433&id=uf6a3e7ba&margin=%5Bobject%20Object%5D&name=L2%20f0.png&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&size=267248&status=done&style=none&taskId=ue1f489a9-e8cb-4f74-9b03-b3ec03dbb15&width=769)

### 步骤 3. 训练与部署

#### 3.1 设置神经网络和参数

选择你觉得合适的神经网络规模：小型、中型、大型。
接着设置参数、训练周期数（正整数）、学习率（从 0 到 1 的数字）和最小置信度（从 0 到 1 的数字）。初始页面已提供一些默认参数值。
![L2 f1.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631940753943-e4657604-1e0a-4436-aad5-d8f1316400d9.png#clientId=u50f391c6-f579-4&from=drop&height=409&id=u33fde180&margin=%5Bobject%20Object%5D&name=L2%20f1.png&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&size=243768&status=done&style=none&taskId=u9f470094-a193-44f4-a8e8-ae4bdc5001c&width=727)

#### 3.2 开始训练模型

点击“开始训练”。
![L2 f2.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631940830065-36d751d3-8930-4f21-8037-ae8cc9925b45.png#clientId=u50f391c6-f579-4&from=drop&height=398&id=u039ed909&margin=%5Bobject%20Object%5D&name=L2%20f2.png&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&size=242347&status=done&style=none&taskId=u16c37b76-05c8-4366-9f8d-88789a0b88e&width=708)
当您点击“开始训练”时，界面会显示“拼命加载中...”。
![L2 f3.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631940961840-4de6fe7a-926b-452d-aaa4-f5606c2765af.png#clientId=u50f391c6-f579-4&from=drop&height=395&id=u8be3e3a5&margin=%5Bobject%20Object%5D&name=L2%20f3.png&originHeight=1061&originWidth=1920&originalType=binary&ratio=1&size=214089&status=done&style=none&taskId=ueec381ae-156f-4a06-8cdd-990bb4ee4e4&width=714)
“拼命加载中...”的持续时间取决于所选神经网络的规模（小型、中型、大型）和训练周期数。通常来说，网络规模和训练周期数越大，所需的时间就越长。
您还可以通过观察“日志输出”来推断等待时间。下图中，“Epoch: 8/30”表示训练总轮数为30轮且已经训练了8轮。
![L2 f4.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631941316761-b114a5aa-6af4-47a0-bd5d-10188b0f78dd.png#clientId=u50f391c6-f579-4&from=drop&height=671&id=u46048db2&margin=%5Bobject%20Object%5D&name=L2%20f4.png&originHeight=935&originWidth=979&originalType=binary&ratio=1&size=124313&status=done&style=none&taskId=uf32b09b6-6435-4dc0-ae13-9d1d7ffd002&width=703)
等待加载完后，“日志输出”中会出现“TrainModel Job completed”表示训练完成，界面上会出现“模型训练报告”。
![L2 f5.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631942934105-82981bb2-2129-4ad4-aa63-ffe47267b058.png#clientId=u50f391c6-f579-4&from=drop&height=637&id=u582b72d9&margin=%5Bobject%20Object%5D&name=L2%20f5.png&originHeight=882&originWidth=909&originalType=binary&ratio=1&size=113111&status=done&style=none&taskId=u6ee603d2-786b-45fc-8f99-fca5aa41701&width=657)

#### 3.3 观察模型性能，选择理想模型

在“模型训练报告”窗口中，您可以观察训练结果，包括模型的准确率、损失和性能。
如果训练结果不理想，您随时可以回到第一步训练模型，选择另一个大小的神经网络，调整参数训练等，直到得到一个结果满意的模型。
![L2 g0.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631943150344-1667167f-0750-419a-9167-f780c1642172.png#clientId=u50f391c6-f579-4&from=drop&height=344&id=u8eb4a4ec&margin=%5Bobject%20Object%5D&name=L2%20g0.png&originHeight=802&originWidth=1508&originalType=binary&ratio=1&size=80509&status=done&style=none&taskId=u343bc747-2f2d-48fb-bff3-070c475b726&width=647)

#### 3.4 部署理想模型

在“模型训练报告”窗口中，点击“模型部署”。
![L2 g1.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631943224661-b5e24109-67f7-40ba-b118-9ce4626638e2.png#clientId=u50f391c6-f579-4&from=drop&height=348&id=ude715c0f&margin=%5Bobject%20Object%5D&name=L2%20g1.png&originHeight=802&originWidth=1508&originalType=binary&ratio=1&size=80264&status=done&style=none&taskId=u8a09d4bd-a75b-485f-bad0-fe2cad53fea&width=655)

![L2 g2.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631943423402-e2424a89-5ba1-436f-a5a9-6785a723d3c0.png#clientId=u8f4ff990-6b25-4&from=drop&height=331&id=cwNV8&margin=%5Bobject%20Object%5D&name=L2%20g2.png&originHeight=938&originWidth=1920&originalType=binary&ratio=1&size=157381&status=done&style=none&taskId=ue26eb89f-cbce-4a57-8ea5-35c0cacdd65&width=677)
等到部署完成后，点击“确认”即可跳转到“使用与编程”窗口
![L2 g3.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631943462624-17e0a593-a004-42a7-b7c1-bd7e228312d0.png#clientId=u8f4ff990-6b25-4&from=drop&id=l9vbh&margin=%5Bobject%20Object%5D&name=L2%20g3.png&originHeight=267&originWidth=592&originalType=binary&ratio=1&size=19752&status=done&style=none&taskId=u9fdaeaec-1941-4065-b9ca-f07c1a52632)

### 步骤 4. 使用与编程

#### 4.1 编写使用模型的程序

在“使用与编程”界面，点击“模型使用”以调用部署的模型。
![image.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631960966341-dd2bb394-d66b-4cd7-931c-d9102dc095e8.png#clientId=uc1db889d-9af8-4&from=paste&height=1080&id=ud69d7bbc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&size=222601&status=done&style=none&taskId=u867bc1a4-235f-4f12-943c-639fc75d16e&width=1920)
您可以尝试通过编写以下程序来调用您的模型。
![L2 k1.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631944098252-78c07a48-4423-498d-a9eb-07414e6470e3.png#clientId=u8f4ff990-6b25-4&from=drop&id=u5191b3d8&margin=%5Bobject%20Object%5D&name=L2%20k1.png&originHeight=355&originWidth=520&originalType=binary&ratio=1&size=33182&status=done&style=none&taskId=uf872714f-ab17-4675-befd-3deda3d29bc)

#### 4.2 将程序上传到 Wio Terminal

单击“上传”按钮。
![image.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1632277550355-b13f08db-e48b-4879-9bc9-1abfab08d6d5.png#clientId=u4d58bf46-3655-4&from=paste&height=540&id=u4eb0814e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&size=258539&status=done&style=none&taskId=u1ea2b2b8-b44c-4b8e-a420-cc85c93aa4f&width=960)

选择与当前 Wio Terminal 对应的串口（不一定如图所示的 COM14），点击“确定”按钮。
![L2 d1.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631938852502-1732ef74-a9e0-4cc4-ab96-1bd0107a1e57.png#clientId=u50f391c6-f579-4&from=drop&height=330&id=D39DG&margin=%5Bobject%20Object%5D&name=L2%20d1.png&originHeight=464&originWidth=716&originalType=binary&ratio=1&size=19759&status=done&style=none&taskId=u83f94da7-a88e-4c37-b8ae-9495c8de047&width=509)
第一次上传时间通常比较长，并且随着模型的复杂性时间会进一步增加。较小型号的上传时间约为 4 分钟，较大型号可能会消耗更长时间，这取决于您机器的性能。
![L2 d2.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631938871090-4b8619f4-ac5b-4bc6-a712-bfc8df3bb629.png#clientId=u50f391c6-f579-4&from=drop&id=VbHLW&margin=%5Bobject%20Object%5D&name=L2%20d2.png&originHeight=326&originWidth=398&originalType=binary&ratio=1&size=21802&status=done&style=none&taskId=uc64144f6-a0c0-45ff-ba4c-c70c20c8827)
![L2 d3.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631944381864-77239cc5-6315-441a-9ab9-4c1ff5115234.png#clientId=u8f4ff990-6b25-4&from=drop&height=234&id=ufdcfdb02&margin=%5Bobject%20Object%5D&name=L2%20d3.png&originHeight=262&originWidth=449&originalType=binary&ratio=1&size=16299&status=done&style=none&taskId=u5d4930ee-f1ce-47e6-9088-eae0985999e&width=401)

#### 4.3 Wio Terminal 测试模型

翻转您的 Wio Terminal，查看其屏幕是否显示“翻转”。可以再尝试其他的动作，看看 Wio Terminal 是否识别您的动作。

**恭喜！您已经完成了第一个嵌入式机器学习模型。相信你一定有兴趣了解自己做的每一个操作的意义，那么让我们首先来学习机器学习的基础理论知识，先看看我们的输入（input）。**

## 机器学习理论（输入，标签，数据集）

输入（input）：

- 标签
- 数据集
  - 训练集、验证集和测试集
  - 数据量
  - 获取数据的方式
  - 数据集的质量

 ![image.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631961086662-861093d7-19d6-4162-9ba1-4347d7572520.png#clientId=uc1db889d-9af8-4&from=paste&height=392&id=ubbbc6b6a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=471&originWidth=465&originalType=binary&ratio=1&size=33609&status=done&style=none&taskId=ub84bc5b4-1173-4236-acf4-500feea85dc&width=387)

### 输入

#### 1. 标签

**1.1 什么是标签：**
顾名思义，当您为数据添加有意义的标签或为您收集的原始数据分配类别时，数据将会被标记，这意味着您向数据设置了其对应目标， AI 会通过这些数据标签来学习。
现在，让我们看看这是如何做的。假设我们有一组标有“柠檬”、“橙子”或“香蕉”的水果，模型会通过这些标记的水果进行分类训练，当训练结束后，如果这时输入有新的水果且没有贴标签，则会被模型判断并贴上标签并归入这三组中的其中一组，注意输入元素有可能同时属于多个类别。
![L2 l0.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631944435407-8451900b-3f53-4d2f-b188-410d735bc118.png#clientId=u8f4ff990-6b25-4&from=drop&height=473&id=qkSij&margin=%5Bobject%20Object%5D&name=L2%20l0.png&originHeight=500&originWidth=750&originalType=binary&ratio=1&size=395021&status=done&style=none&taskId=u1a36a7ea-29fe-480e-b243-261cc482ec7&width=709)
> 柠檬              橙子               香蕉

#### 2. 数据集

**2.1 什么是数据集：**
如果您想要一个可运行且可靠的模型，则需要大量相关的高质量数据。这意味着您必须通过提供数万个示例来训练您的 ML 模型，并且让它记住您的数据片段之间的相关性。
完整数据集由训练集和测试集组成：
您提供给模型的数据称为训练数据集，而您提供给模型进行预测的数据则称为测试集。
![3.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1632474037102-d4176253-473b-43e3-9b36-44fc192a5219.png#clientId=ub70c3e5c-9a86-4&from=drop&height=193&id=uedc90483&margin=%5Bobject%20Object%5D&name=3.png&originHeight=436&originWidth=831&originalType=binary&ratio=1&size=43398&status=done&style=none&taskId=u4eb72d33-113a-4903-bf8c-ec11c93201c&width=367.2857666015625)
>                                                                        所有数据集
>                                   训练集                                                                                                    测试集
>          训练集                                            验证集                                                                       测试集

此外，训练集可以分为两组。我们可以在开始训练后观察日志，发现训练数据集会被拆分为训练集和验证集。

![L2 l2.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631944967864-7dd0b930-cadc-489c-8502-a01d90bada66.png#clientId=u8f4ff990-6b25-4&from=drop&height=211&id=u083533ab&margin=%5Bobject%20Object%5D&name=L2%20l2.png&originHeight=266&originWidth=833&originalType=binary&ratio=1&size=34076&status=done&style=none&taskId=u08fef062-a42c-4046-9a44-a5c89a65185&width=661)
这里的 Training inputs 即为 训练集，而 validating inputs 为验证集。

- **训练集：**训练集是模型用来学习的数据。
- **验证集：**使用训练集进行训练后，使用验证集中的点来计算分类器的准确率或误差。这里的关键是我们知道验证集中每个点的真实标签，但我们暂时假装不知道，也就是我们假装将验证集中的点以没有标签的形式输入到模型分类器，然后我们会收到该点的分类和标签。完成后我们可以查看验证点的真实标签是否与收到的标签一致，看看我们是否做对了。如果我们对验证集中的每个点都这样做，我们就可以计算验证错误！

​

**2.2 那多少训练数据才能够呢**
如果要一个简短的回答是，这没有准确的答案。如果要稍微长一点的答案的话，那就是每个特定项目都需要不同的特定数量的训练数据，而知道需要多少训练数据的唯一方法就是反复试验。
这里有一些指南可以帮助您了解为什么这个问题并没有准确答案：

- 通常来说，具有更多属性和更多连接网络且更复杂的模型（如人工神经网络）将需要更多数据才能正确训练。
- 模型的应用范围，以及模型接受训练之后用来预测的现实生活的复杂性也会影响所需训练数据的多少，特别是异常和盲点。
- 随着时间的推移，您可能需要重新训练或调整您的模型，因为它预测的趋势会发生变化，从长远来看，这将需要更多数据。

训练集的数据量取决于多种因素，对经验丰富的工程师来说，他们大体上对训练模型的数据量有一定的了解，你可以去论坛，科学社区等一些地方来找到他们向他们请教从而精进学习。
​

**2.3 如何获取数据**
![4.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1632474082101-02f8592c-b6ac-4cd1-b1c6-b6dfba555941.png#clientId=ub70c3e5c-9a86-4&from=drop&height=152&id=u3878231d&margin=%5Bobject%20Object%5D&name=4.png&originHeight=338&originWidth=809&originalType=binary&ratio=1&size=58290&status=done&style=none&taskId=u48172cbc-1330-45f0-9c53-38bd08dade5&width=363.2857666015625)
>                                                    收集训练数据的途径
> 自己动手                                              开源社区                                                   网络搜索

- 自己动手：将 Wio Terminal 与传感器或者其他设备一起使用。
- 开源社区：一些数据科学社区，如 Kaggle。
- 网络搜素：根据您的目标，在线搜索您想要的数据集。

**2.4 如何判断数据集的质量：**
**准确性：**准确性是指数据描述是否符合其在现实世界条件中的描述。如果您尝试教计算机识别猫，则需要将现实当中的猫标记为“猫”而不是“狗”。
**关联性：**您收集的数据也应该对您准备将其用于的模型中有用。如果它与您的目标不相关，则它对您并没有用处，应当舍弃。如果您想教电脑通过图片识别猫，则并不需要提供猫粮的照片。总的来说，为您的数据收集设定目标很重要，这样才知道要什么样的数据才是有用的。
**数据规模：**如果您尝试教计算机识别猫，则需要显示数千张大小、颜色和形状各不同的猫的图像，以使您的模型能够准确识别猫。
**平衡性：**平衡性是指训练集中的数据分类是否均衡，不平衡尤为常见：大多数分类数据集在每个类别中的实例数量并不相同，但微小的差异并不重要。
而当不平衡性足够大时，我们的模型会发生什么？
我们的模型通过学习数据并且“巧妙”地进行分类，得到的结果是预测“1 类”竟然达到 90% 的高准确度。
![5.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1632474133165-82a36278-1a91-49e9-83e0-de4479dbd077.png#clientId=ub70c3e5c-9a86-4&from=drop&height=196&id=ub6822503&margin=%5Bobject%20Object%5D&name=5.png&originHeight=596&originWidth=1183&originalType=binary&ratio=1&size=30829&status=done&style=none&taskId=u63da558d-87de-4334-a2a0-dde9c9a5859&width=388.2857208251953)
>                           关于平衡和不平衡数据的例子
>

**那么如何解决失衡呢？**
![6.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1632474170173-671f1f6c-d391-40cb-a90e-d06a49289bfa.png#clientId=ub70c3e5c-9a86-4&from=drop&height=200&id=u488b39cb&margin=%5Bobject%20Object%5D&name=6.png&originHeight=602&originWidth=1628&originalType=binary&ratio=1&size=263178&status=done&style=none&taskId=ue399c9ff-465a-4bc8-9169-5a72af733c8&width=540.2857360839844)
>           少数                                                                  多数
> 原始数据集                       最终数据集                      原始数据集                       最终数据集
>

**过采样（Up Sampling）**：增加训练集中少数分类的数量。
**欠采样（Down Sampling）**：减少多数样本的数量以平衡分类分布。

## 总结

1. 背景理论知识：

- 加速度计

2. 嵌入式机器学习实践：

![L2 l7.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631945837820-54425377-0d43-4c1e-a8be-d4e137bb8f21.png#clientId=ubafdcfc5-4745-4&from=drop&height=230&id=u32e5eb39&margin=%5Bobject%20Object%5D&name=L2%20l7.png&originHeight=351&originWidth=374&originalType=binary&ratio=1&size=26772&status=done&style=none&taskId=u29d73ff4-0bbd-48ec-a2d2-0c79d5c8c13&width=245)

3. 机器学习理论（输入）

- 标签：为您收集的原始数据贴上标签以分配类别。
- 数据集：
   1. 训练集、验证集和测试集：训练集来输入模型，验证集用于验证结果以改进模型，测试集用于预测。
   1. 所需数据量：合适的规模（一般情况下越多越好）。
   1. 数据获取方式：自己获取，开源社区，互联网搜索。
   1. 数据集的质量：准确性、关联性、数据规模、平衡性。

​
