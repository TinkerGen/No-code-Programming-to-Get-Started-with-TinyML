## 理论知识
### 机器学习和深度学习
机器学习是人工智能 (AI - Artificial Intelligence) 的一个分支，主要是从数据中学习进而能输出分类并随着时间的推移、算法的增强、数据的增多提高其准确性的一个多领域交叉学科，它的编程方式并不适用于有规则的传统的编程。机器学习使机器能够像人类一样通过观察、分类数据来工作，并从错误中不断学习进步；而深度学习是机器学习的一个子集，它依靠深度人工神经网络（因此得名）使得机器可以从更加庞大的数据中学习。
![L1 a.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631778213130-d996b3d7-b061-4f5a-aeb9-df381604552a.png#clientId=ua315f22e-dec3-4&from=drop&height=427&id=u8f93c457&margin=%5Bobject%20Object%5D&name=L1%20a.png&originHeight=853&originWidth=882&originalType=binary&ratio=1&size=347675&status=done&style=none&taskId=uab95cad2-6efa-437e-bfcf-5d0d46a6ab0&width=441)
人工神经网络 (ANN——Artificial Neural Network) 是人类试图模拟组成人类大脑的神经元网络所提出的一个方法，它是由计算机编程创建的，其行为方式就像相互连接的脑细胞一样，为了学习深度学习，人工神经网络是您所需要的必备的一个技能。
学习人工神经网络，首先您需要准备大量称为“训练集”的数据。当您尝试教人工神经网络如何区分猫和狗时，训练集将提供数千张标记狗和猫的图像供神经网络学习。一旦人工神经网络接受了大量数据的训练，它将能够根据它认为在不同单元中“看到或听到”（取决于训练集）的内容来对未来“看到或听到”的数据进行分类。在训练期间，机器的输出结果会与人类提供的对观察内容的描述进行比较，当它们相同时，机器验证为正确，而如果不正确，它会使用反向传播（Backpropagation）来调整其学习模式。反向传播的意思是不正确的信息会通过层（layer）返回从而调整数学方程（即算法）的过程，这可以称作“深度学习”的过程，这也是使网络智能化的原因。
![L1 b.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1630912853347-6b55b9f2-6bad-4ee6-a2ed-2084e8376c35.png#clientId=uc9939136-7b1c-4&from=drop&id=u32c53928&margin=%5Bobject%20Object%5D&name=L1%20b.png&originHeight=461&originWidth=906&originalType=binary&ratio=1&size=514639&status=done&style=none&taskId=u7efd357f-a70b-4357-b6d1-35666b3f406) 
> 需要美术绘制插图
> How supervised Machine Learning Works
> 监督学习是如何运作的
> Step 1                                                                                          Step2
> 第一步                                                                                           第二步
> 给机器提供带有“标记”的训练集数据加以训练              给机器提供未标记的测试集数据看能否判断正确
> 猫          机器                     机器                       猫（上） 非猫（下）

#### 什么是 TinyML（嵌入式机器学习），为什么它如此重要？
通常来说，深度神经网络需要相当强大的计算资源来训练和部署。 然而，最近出现了一个名为 TinyML （嵌入式机器学习）的分支， 它代表了机器学习和嵌入式系统中的一项技术（或研究领域），用来探索哪些机器学习应用程序（经过简化、优化和集成）可以在微控制器这类小型设备上运行。其常见的Logo如下图所示。
![L1 c.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1630916889978-3b11aa52-e5e4-4675-9d5a-e926e629a8da.png#clientId=uc9939136-7b1c-4&from=drop&height=130&id=u0928290e&margin=%5Bobject%20Object%5D&name=L1%20c.png&originHeight=491&originWidth=500&originalType=binary&ratio=1&size=48459&status=done&style=none&taskId=uc56947a9-1817-4834-b3e4-a3872e02c26&width=132)
**ML（Machine Learning）**表示机器学习，而 TinyML 中的 Tiny 是“微小”的意思，意味着 ML 模型经过优化，可以在极低功耗和小尺寸设备上运行，例如各种微型控制器 (MCU)。嵌入式设备有着各种形状和大小，他可以大到从“嵌入式超级计算机”NVIDIA Jetson Xavier AGX 到最小的微控制器 ESP32 或者 Cortex M0。
![L1 d.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1630917064245-d45f2c66-726a-4f79-9cbf-c63bda38a37c.png#clientId=uc9939136-7b1c-4&from=drop&height=302&id=u0ce040a8&margin=%5Bobject%20Object%5D&name=L1%20d.png&originHeight=389&originWidth=740&originalType=binary&ratio=1&size=308505&status=done&style=none&taskId=u93b2537e-4968-4175-a8d7-12ca6ea2c75&width=575)


下图是 GeeekNET ESP 32 的开发板：
![L1 e.jpg](https://cdn.nlark.com/yuque/0/2021/jpeg/22391310/1630917087795-54d1c38b-7464-4f8b-8292-e9f69b17049d.jpeg#clientId=uc9939136-7b1c-4&from=drop&height=347&id=u2d145ff0&name=L1%20e.jpg&originHeight=525&originWidth=700&originalType=binary&ratio=1&size=44130&status=done&style=none&taskId=u596230dc-3a6d-48fb-b316-516d7fabb92&width=463)
#### 为什么使用微型控制器的嵌入式机器学习被归入一个特殊类别，甚至有着自己的名字？
答案是它有着自己独特的优点以及特点。嵌入式机器学习的吸引力实际上在于 MCU 体积小可以无处不在，耗能少又相对便宜。 以 ARM Cortex M0+ 和围绕它构造的小型 Seeeduino XIAO 板为例——该板只有拇指大小（20×17.5 毫米），仅消耗 1.33 毫安每时的电量，这意味着它可以连接 150 mA 电池之后可以连续工作112个小时（如果设备进入深度睡眠，这个时间还可以进一步增加）。做到这些，而它的成本仅为 5 美元。
![L1 l.jpg](https://cdn.nlark.com/yuque/0/2021/jpeg/22391310/1631787026970-282dd0a2-d37a-4e09-81ed-a3bfa31c0819.jpeg#clientId=ua315f22e-dec3-4&from=drop&height=355&id=ud744a96f&name=L1%20l.jpg&originHeight=1050&originWidth=1400&originalType=binary&ratio=1&size=73670&status=done&style=none&taskId=u2d5536d3-f3ab-43af-b310-965fc5199bc&width=473)
由于最近模型优化的改进以及专门为在微控制器上运行机器学习模型而创建的框架的出现， 为这些微型设备提供更多智能已经成为可能。 我们现在可以在微控制器上部署神经网络，用于**音频场景识别**（例如，大象活动或玻璃破碎的声音）、**热词检测**（使用特定短语激活设备），甚至用于简单的**图像识别**任务。 带有嵌入式微控制器的设备可为旧传感器赋予新的生命和意义。
借助 Codecraft 和 Wio Terminal，您现在就可以体验嵌入式机器学习的整个过程，而无需处理复杂的编程环境和丰富的编程知识。
## 做好准备
### Wio Terminal
Wio Terminal 对新手来说是学习物联网和嵌入式机器学习的一个完美的工具。它由矽递科技设计的并且支持多种嵌入式机器学习框架。
![L1 m.jpg](https://cdn.nlark.com/yuque/0/2021/jpeg/22391310/1631787141298-72b3cba3-591b-445b-a6e8-81caf5f34586.jpeg#clientId=ua315f22e-dec3-4&from=drop&height=289&id=u48856537&name=L1%20m.jpg&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&size=185394&status=done&style=none&taskId=u181290d6-1bab-4762-b511-473c7ae1060&width=514)
Wio Terminal 使用 ATSAMD51P19 微控制器和 ARM Cortex-M4F，运行频率为 120MHz（提升至 200MHz），它包含4MB 外部闪存和 192kb RAM，并且支持 Realtek RTL8720DN 的无线连接， 同时与 Arduino 和 MicroPython 兼容，支持蓝牙和 Wi-Fi，这为其物联网功能奠定了坚实的基础。Wio Terminal 有2.4英寸液晶屏、板载加速度计（LIS3DHTR）、麦克风、蜂鸣器、microSD 卡槽、光传感器和红外发射器（IR 940nm）。 最重要的是，它有两个用于 Grove 生态系统的板载多功能 Grove 端口和与树莓派兼容的40针 GPIO 引脚，用来提供额外的附加支持。![L1 n.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631787182776-ecf3f1b6-f03b-4cf2-8536-9bd1635449d5.png#clientId=ua315f22e-dec3-4&from=drop&id=ue4341bc1&margin=%5Bobject%20Object%5D&name=L1%20n.png&originHeight=716&originWidth=1161&originalType=binary&ratio=1&size=223670&status=done&style=none&taskId=u87913bf9-8c60-46f6-b47c-52e062061cc)
> 需要美术绘制插图
> FPC | FPC 柔性线路板接口
> DC-DC | DC-DC 转换器
> 2.4G&5G Antenna | 2.4G&5G 天线
> LIS3DHTR | 三轴加速度计
> 5-way switch（Behind）|  五向摇杆（位于背面）
> light sensor | 光线传感器
> IR emitter |  IR 红外线发射器
> ATSAMD51P19 |  ATSAMD51P19 微控制器
> microSD Card Slot | microSD 卡槽
> Microphone & Buzzer | 麦克风与蜂鸣器（位于背面）
> USB TYPE C | USB Type-C 接口 

### Codecraft
在软件方面，我们将使用图形化编程平台 Codecraft，由 Edge Impulse 为 Codecraft 提供机器学习的服务端技术支持，使用 Codecraft 的初学者可以轻松使用嵌入式机器学习。 它为初学者从数据采集一直到模型部署到设备的整个过程都提供了支持，同时对整个 TinyML 的使用过程提供了友好又功能强大的 Web 界面和工具包。它是一个用户友好的开发平台，可以用于在嵌入式设备上进行机器学习。
​

**所以，让我们快速了解如何使用并开始我们的机器学习之旅吧。**


在 Codecraft 的主页点击 Wio Terminal 的图标，进入到 Wio Terminal 的嵌入式机器学习页面
![image.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631934746215-d29d6d5d-74cc-4340-813f-a66951477c22.png#clientId=u0ee1cff9-a7a6-4&from=paste&height=966&id=ua4a9efdd&margin=%5Bobject%20Object%5D&name=image.png&originHeight=966&originWidth=1920&originalType=binary&ratio=1&size=568367&status=done&style=none&taskId=uc534ff65-2e2c-4e6b-8bfc-d916056d807&width=1920)
#### 一、 创建与选择模型
![L1 a1.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631933533842-f879fa01-f68b-4637-b941-796ba2ebbf7f.png#clientId=u0ee1cff9-a7a6-4&from=drop&height=569&id=u2b680312&margin=%5Bobject%20Object%5D&name=L1%20a1.png&originHeight=1143&originWidth=1970&originalType=binary&ratio=1&size=263260&status=done&style=none&taskId=u6520335c-38ad-4ebf-ac4a-4cd2ea7ffcb&width=981)

1. 创建与选择模型：**嵌入式机器学习的第一步**。点击“创建与选择模型”就可以看见“为嵌入式机器学习创建新模型”的页面。
1. 返回 Codecraft 主页：点击以返回 Codecraft 主页，如果您还没有保存当前程序，它会在您离开之前提示保存。
1. 语言：点击后会出现语言选项，您可以在此处更改语言。
1. 文件：您可以创建一个新的在线项目或打开一个本地项目，您也可以按照屏幕上的说明将项目从计算机保存到云端。
1. 教程：在这里您可以看到 Codecraft 的相关例程。
1. 保存：您可以修改项目名称并将其保存到云端（ Codecraft 应该连接到互联网并且您应该使用您的 Codecraft 账户登录）。
1. 模块/代码：您可以在模块和代码之间切换，这里使用的编程语言是 C。
1. 帮助：我们始终感谢您对 Codecraft 的建议，有您的参与，我们会做得更好
1. 登录：您可以看到您的云项目、账户设置、我的邀请码还有退出键，如果您还没有登录，它会提示您进行登录
1. 根据传感器选择模型框架：您可以根据您要使用的传感器在此处创建模型。 单击相应的图标以使用对应的传感器创建模型，创建新模型后，界面会自动跳转到“数据采集”界面
1. 我的模型：您可以单击此处查看您创建的所有模型
#### 二、数据采集
![L1 a2.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631932632698-cf8e7d9e-d3b3-4d22-817d-c5e436f04db3.png#clientId=u0ee1cff9-a7a6-4&from=drop&id=u464f16af&margin=%5Bobject%20Object%5D&name=L1%20a2.png&originHeight=1080&originWidth=2111&originalType=binary&ratio=1&size=322103&status=done&style=none&taskId=uf8426663-b7df-4a53-97ba-3cd886289e8)

1. 连接设备：您可以在这里连接您的设备
1. 上传：点击这里来上传您的程序
1. 数据采集：**嵌入式机器学习的第二步**
1. 模块类别：您可以在这里选择您的模块分类
1. 数据采集：您可以获取“默认数据采集程序”以及与样本数据相关的模块
1. 默认数据采集程序：您可以上传默认数据采集程序以快速开始您的数据采集
1. 模块上的命令：在这里您可以重命名模块或者删除模块和它的数据
1. 数据采集步骤介绍：单击此处将显示一个弹出窗口，其中包含数据收集过程的详细信息
1. 标签：数据采集界面右侧有默认标签， 您在这里可以添加和删除标签。 添加自定义标签：单击“+”， 删除标签：将鼠标悬停在标签上，标签左上角会出现一个“x”，点击“x”则可以将其删除，修改标签：点击出现的标签就会弹出修改标签窗口
1. 数据上的命令：在这里你可以删除，重命名和下载数据
#### 三、训练与部署
![L1 a3.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631931065292-54706d66-04d5-40db-a03e-7a3c30885e77.png#clientId=u0ee1cff9-a7a6-4&from=drop&id=u9fdc7a30&margin=%5Bobject%20Object%5D&name=L1%20a3.png&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&size=258862&status=done&style=none&taskId=uc2a1d4dc-168d-4ee8-9043-a3d5f5cf2f2)
![L1 b3.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631931381081-11ca2977-97cb-4639-ac9b-ed4cd3447b08.png#clientId=u0ee1cff9-a7a6-4&from=drop&id=u62042914&margin=%5Bobject%20Object%5D&name=L1%20b3.png&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&size=180738&status=done&style=none&taskId=u2fb07122-4f67-44bb-a3af-7eec4f7385f)

1. 训练与部署：**嵌入式机器学习的第三步**
1. 选择神经网络规模：您可以选择合适的神经网络规模：小型、中型、大型
1. 训练周期数：Codecraft 为模型的每个比例提供默认参数值。 您也可以自行设置训练周期数（正整数）、学习率（0~1 小数）和最低置信度（0~1 小数）
1. 开始训练：点击“开始训练”来训练模型
1. 样本数据：在这里可以观察收集到的数据样本
1. 模型训练报告：您可以在 Wio Terminal 上观察模型的准确率、损失和性能等训练结果。 如果训练结果不理想，您可以回到第一步的训练模型，选择另一个规模大小的神经网络或调整参数设置来重新训练，直到得到一个结果满意的模型
1. 日志输出：在训练过程中，“日志”屏幕会显示训练的日志。通过观察“日志”即可推断模型的性能
1. 模型部署：点击这里来部署理想的模型
#### 四、使用与编程
![test.png](https://cdn.nlark.com/yuque/0/2021/png/22391310/1631930545631-fc3281ea-bd40-4a05-98c8-b40a64cc7354.png#clientId=u0ee1cff9-a7a6-4&from=drop&id=u3583d45b&margin=%5Bobject%20Object%5D&name=test.png&originHeight=1080&originWidth=1745&originalType=binary&ratio=1&size=167272&status=done&style=none&taskId=u2888da74-b9f1-4301-9c58-7bbbe5482b2)
使用与编程：**嵌入式机器学习的第四步，**您可以通过拖动模块来编写程序，课程还提供了最简洁的示例代码， 您可以根据颜色来找到相对应的模块。
### 示例教程
为了帮助理解嵌入式机器学习的使用，我们提供7个模板项目。您可以根据这些模型示例来学习如何使用  Codecraft 进行嵌入式机器学习。 我们希望这些示例可以帮助您构建更多更有趣的应用程序。