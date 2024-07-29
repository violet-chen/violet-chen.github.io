---
title: houdini
tags: houdini
categories: DCC软件
abbrlink: d1f700e2
date: 2024-07-21 13:40:00
---
<meta name="referrer" content="no-referrer" />

<a name="biomu"></a>
# Houdini的一些专业术语
<a name="yo3oF"></a>
## 不同网络的介绍
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689061156266-f97ffd6f-8523-4e9b-9881-5bc30905ad3e.png#averageHue=%23222222&clientId=u6ad503fa-7cfa-4&from=paste&height=1001&id=ltCBL&originHeight=1001&originWidth=2049&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1345247&status=done&style=none&taskId=u2413d157-4645-4ed0-a78c-4b5a5572c61&title=&width=2049)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689061605663-26354c46-c219-4ee1-832e-a075f297d2dd.png#averageHue=%23444241&clientId=u6ad503fa-7cfa-4&from=paste&height=232&id=pkx9H&originHeight=232&originWidth=116&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14937&status=done&style=none&taskId=u82469f77-6c15-4f0f-9397-9c69db01e7f&title=&width=116) <br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689061625011-6b95d11b-b34b-479b-aa72-7ab412e7e8f6.png#averageHue=%23424242&clientId=u6ad503fa-7cfa-4&from=paste&height=31&id=DGN3z&originHeight=31&originWidth=75&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1885&status=done&style=none&taskId=uc51dc965-3e6c-4697-b8f9-f1b34094ad5&title=&width=75) ch是控制动态和声音的<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689061761639-7c3deb25-2fa2-4b1e-89fc-5b17fe6155d5.png#averageHue=%23494040&clientId=u6ad503fa-7cfa-4&from=paste&height=30&id=rBWBv&originHeight=30&originWidth=78&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1866&status=done&style=none&taskId=u099bfccf-c732-442a-a5a6-1d6022a2753&title=&width=78)shop是旧的管理材质的，现在已经被mat代替了<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689062628883-6ae3c575-96bd-4b43-a1ac-d4473bdb749b.png#averageHue=%234c4640&clientId=u6ad503fa-7cfa-4&from=paste&height=30&id=bCOfh&originHeight=30&originWidth=86&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2081&status=done&style=none&taskId=u67346da3-5258-4085-a745-9a29c9a997d&title=&width=86)stage(solaris):适用于lookdev，布局和照明，以USD为核心，可以使用专门的节点定位对象，实例化几何体和管理镜头布局。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689062633114-c4c47694-9015-4be7-9e31-eb357d3c610a.png#averageHue=%233e3d3b&clientId=u6ad503fa-7cfa-4&from=paste&height=30&id=wK1fy&originHeight=30&originWidth=88&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1654&status=done&style=none&taskId=u317279d8-e9c9-42ab-8bb2-b5cdd007082&title=&width=88)tasks: 用于处理多线程任务和作业。它用于执行复杂的计算、模拟和渲染任务，并对其进行分析和管理
<a name="Yltcj"></a>
## particle与grains的区别
grains是颗粒，particles是粒子<br />grains模拟的是颗粒材料，如沙子、粉末等。它们具有质量、速度、位置等物理属性，并受到力的作用。grains的模拟通常涉及颗粒之间的聚集、流动、堆积和碰撞等行为。<br />particles一般用于模拟离散的小元素，例如火花、烟雾、爆炸碎片等。粒子可以表示各种物理属性，如速度、位置、颜色等。particle的模拟通常设计粒子之间的移动、发射、生命周期和相互作用等。
<a name="SGyGQ"></a>
## HDA（OTL）
HDA在旧版本中叫OTL，意思是Houdini Digital Asset 数字资产，当制作完一个程序化的模型或者动画或者效果等以后，可以将这些节点打包成一个HDA以便在不同的项目中进行共享和重复使用。<br />HDA不仅可以在Houdini中重复使用并且可以编辑，HDA也可以导出为独立的文件提供给其他DCC软件或者引擎来使用。<br />在houdini中这些带锁的节点都是HDA<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689320716023-6921b55b-1837-4d2a-bbd7-a2a00e41db9e.png#averageHue=%23383736&clientId=u85a49878-3118-4&from=paste&height=437&id=uab7062e4&originHeight=437&originWidth=864&originalType=binary&ratio=1&rotation=0&showTitle=false&size=45822&status=done&style=none&taskId=u7d7a7ce8-187a-4dcd-a2c4-f58c029d1be&title=&width=864)
<a name="ur7FM"></a>
### 制作HDA
首先将节点进行打包，并在打包节点中通过参数编辑器绑定对应的参数。<br />打包快捷键（shift+c）：选中节点后点击右上角图标![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689321623116-8160f13a-4721-4bd5-82f6-a1b21ec8c25f.png#averageHue=%233b3a39&clientId=u85a49878-3118-4&from=paste&height=267&id=u80b0cf0e&originHeight=267&originWidth=477&originalType=binary&ratio=1&rotation=0&showTitle=false&size=20582&status=done&style=none&taskId=u64d57096-1f2d-4037-8357-f1ccf7f63b1&title=&width=477)，<br />然后在打包的节点上右键选择创建HDA（这是18.5上面截的图，19.5上面没有，19.5版本需要在显示器左上角创建HDA）![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689322027591-a25ba17c-fff8-4d8f-ad81-58d2025ebf32.png#averageHue=%233e3c39&clientId=u85a49878-3118-4&from=paste&height=345&id=u33ec8d17&originHeight=345&originWidth=387&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25085&status=done&style=none&taskId=u61800548-abb0-4a76-bd45-e424522524b&title=&width=387)，![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689322101513-49ea9641-6e85-4063-b809-5592b3d2a38a.png#averageHue=%234c4a48&clientId=u85a49878-3118-4&from=paste&height=109&id=ue9c47823&originHeight=109&originWidth=531&originalType=binary&ratio=1&rotation=0&showTitle=false&size=24530&status=done&style=none&taskId=u4c360d63-6875-4f33-995c-c9391713f1e&title=&width=531)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689322276022-e99e4260-c070-492d-a865-764081ff20de.png#averageHue=%2350504f&clientId=u85a49878-3118-4&from=paste&height=212&id=u1c83773b&originHeight=212&originWidth=566&originalType=binary&ratio=1&rotation=0&showTitle=false&size=23866&status=done&style=none&taskId=u60db91a9-b047-46a7-9434-1ec7113138f&title=&width=566)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689322499588-4f49b052-e74d-498b-85cf-98e959991620.png#averageHue=%233f3e3e&clientId=u85a49878-3118-4&from=paste&height=855&id=u3ab13769&originHeight=855&originWidth=1224&originalType=binary&ratio=1&rotation=0&showTitle=false&size=84192&status=done&style=none&taskId=ub9a83e84-0be0-4443-9219-80461d43e5f&title=&width=1224)<br />保存以后在houdini的网络编辑器中输入HDA的名字来调用了，并且可以在houdini中再次调整HDA的默认参数。<br />并且在电脑里的houdini文档里面可以找到对应HDA文件：Documents\houdini19.5\otls
<a name="ikxeV"></a>
### 修改HDA默认参数
方法一：先解锁节点的锁定。右键点击 Type Properties... 即可再次修改默认参数<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689322626633-d7217860-126d-44f9-b3d1-aae687e0abc9.png#averageHue=%23484540&clientId=u85a49878-3118-4&from=paste&height=487&id=qIoJb&originHeight=487&originWidth=357&originalType=binary&ratio=1&rotation=0&showTitle=false&size=43289&status=done&style=none&taskId=u6224e910-98cf-485c-8da7-1bb2bee44fa&title=&width=357)<br />方法二：在节点本身的参数面板中修改参数然后右键节点选择Save Node Type然后选择Match Current Definition![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689326490636-afa265a3-794d-4024-b092-45ed221420e4.png#averageHue=%234d463f&clientId=u85a49878-3118-4&from=paste&height=418&id=u8886ac0e&originHeight=418&originWidth=222&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27589&status=done&style=none&taskId=u4b2d5c1d-ef71-4d78-9409-83c5abb320e&title=&width=222)


<a name="IBSWy"></a>
# 界面设置
<a name="brUG7"></a>
## UI设置
使用Ctrl + ,  进入界面设置![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689052670029-436cbe6e-4999-478d-8a63-3342240b5c54.png#averageHue=%234d473f&clientId=u6ad503fa-7cfa-4&from=paste&height=272&id=u9559eddf&originHeight=272&originWidth=620&originalType=binary&ratio=1&rotation=0&showTitle=false&size=54858&status=done&style=none&taskId=ue5a25b2d-b0c2-4ac0-a5e5-6a4f447a20a&title=&width=620)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689052678655-525899c5-c1bc-4e65-aa1f-cbcbfcaa3243.png#averageHue=%233b3a3a&clientId=u6ad503fa-7cfa-4&from=paste&height=820&id=u40ad350e&originHeight=820&originWidth=655&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63975&status=done&style=none&taskId=u46c7ad6f-8a15-4036-8868-37e693eca7c&title=&width=655)
<a name="kDDD4"></a>
## 视图还原
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689060593298-9d2ecce5-3592-4de9-b112-ee5403a555e9.png#averageHue=%23ac7624&clientId=u6ad503fa-7cfa-4&from=paste&height=549&id=uf0f9253f&originHeight=549&originWidth=588&originalType=binary&ratio=1&rotation=0&showTitle=false&size=183785&status=done&style=none&taskId=ub1631d02-cfd1-4564-b52f-14e6e2d99c1&title=&width=588)
<a name="aYSVn"></a>
## 扩展界面布局
在基础视窗的下面创建一个新的视窗alt+]<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689151251229-fda78af2-3c3d-4c38-bfcf-4b915c3e8ead.png#averageHue=%23b87c2f&clientId=u4909db3d-a257-4&from=paste&height=498&id=u7af9267e&originHeight=498&originWidth=1028&originalType=binary&ratio=1&rotation=0&showTitle=false&size=277488&status=done&style=none&taskId=u1cfd423c-107c-4f26-8d15-acc5a3358a1&title=&width=1028)<br />然后更改下面新创建的视窗的类型，这样就能够上面显示视窗，下面显示geometry的数据表格。![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689151406446-57d1695a-253a-4d4b-8fee-a7bcaa4dd4eb.png#averageHue=%236b6762&clientId=u4909db3d-a257-4&from=paste&height=398&id=ue83c3884&originHeight=398&originWidth=663&originalType=binary&ratio=1&rotation=0&showTitle=false&size=149134&status=done&style=none&taskId=u871c11dd-13ae-41c3-be17-5a30bf3ee8d&title=&width=663)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689151463706-695c1046-d36a-4dcd-b0ae-c27945f0598b.png#averageHue=%23979982&clientId=u4909db3d-a257-4&from=paste&height=1283&id=uc948b111&originHeight=1283&originWidth=2344&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1385059&status=done&style=none&taskId=u37308915-c697-49d0-9189-ccae57d8193&title=&width=2344)

<a name="fmM1d"></a>
# 工具架介绍
<a name="yam6V"></a>
## Lights and Cameras灯光和摄像机
这些工具用于在场景中创建和设置灯光和相机。灯光工具可以帮助您调整光源的属性和光照效果，而相机工具则用于设置场景的视角和渲染参数。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689048140387-e5ea0011-c3f5-47a1-b3fa-d694e655c195.png#averageHue=%23474541&clientId=u6ad503fa-7cfa-4&from=paste&height=44&id=u7e327302&originHeight=44&originWidth=496&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13828&status=done&style=none&taskId=udedd4f14-6057-4e81-b91e-94015c0a00c&title=&width=496)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689048146922-fa49bac9-e955-4d88-ae43-257a5c3b6f34.png#averageHue=%233f3f3f&clientId=u6ad503fa-7cfa-4&from=paste&height=55&id=u1d781436&originHeight=55&originWidth=468&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13691&status=done&style=none&taskId=u9cd29529-a9c9-43d4-8edc-ff4d132f683&title=&width=468)
<a name="pkNfH"></a>
## Collisions碰撞
这个工具集用于处理物体之间的碰撞效果。它可以模拟物体之间的碰撞和反应，并生成逼真的物理效果。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047487367-4f683cc9-a0f8-409a-b66e-d668864be23c.png#averageHue=%23403f3e&clientId=u6ad503fa-7cfa-4&from=paste&height=46&id=u1d10c55a&originHeight=46&originWidth=383&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9320&status=done&style=none&taskId=ua7540e2a-471e-4458-9044-22fac9a6a1e&title=&width=383)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689055021610-368a8881-109a-4fc2-97e6-353f0801322f.png#averageHue=%2343433f&clientId=u6ad503fa-7cfa-4&from=paste&height=65&id=u81009f92&originHeight=65&originWidth=73&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3311&status=done&style=none&taskId=u36acc161-a258-49ab-a290-a913237b121&title=&width=73) Deforming Object：令一个geo变成有形变的物体。也就是说这个物体能够影响其他带动力学的物体<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689052258133-5e2db26d-1ae8-4684-a625-28dcdd35c10b.png#averageHue=%233e3e3d&clientId=u6ad503fa-7cfa-4&from=paste&height=56&id=ub0e13744&originHeight=56&originWidth=85&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2715&status=done&style=none&taskId=uc004a5dd-a9bb-457b-ba96-f3adde51c4c&title=&width=85)GroundPlane：添加地面碰撞。

<a name="KELLH"></a>
## Particles粒子
粒子工具用于创建和模拟粒子效果。通过设置粒子的属性和行为，您可以模拟烟雾、火焰、爆炸等效果。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047879218-6a53f94a-13bb-4121-97ce-bea6c0c9eb0d.png#averageHue=%23424141&clientId=u6ad503fa-7cfa-4&from=paste&height=53&id=uc4df9c78&originHeight=53&originWidth=656&originalType=binary&ratio=1&rotation=0&showTitle=false&size=18063&status=done&style=none&taskId=u05216ddd-3f25-440c-9845-1b063ddef41&title=&width=656)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047886198-ab8edb21-ce80-4608-92d5-8c342e76efa2.png#averageHue=%23454342&clientId=u6ad503fa-7cfa-4&from=paste&height=44&id=ucec7dff4&originHeight=44&originWidth=682&originalType=binary&ratio=1&rotation=0&showTitle=false&size=15797&status=done&style=none&taskId=uf49cffd6-4ca3-4d71-9352-f33d839bc62&title=&width=682)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689056776565-2f42881e-6873-4f57-bdc3-51dcbc55cb46.png#averageHue=%233e3e3e&clientId=u6ad503fa-7cfa-4&from=paste&height=77&id=u531f0a6a&originHeight=77&originWidth=75&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3291&status=done&style=none&taskId=u626295c8-e989-4538-bd60-92c31884c77&title=&width=75)<br />SourceParticleEmitter：将所选择的物体变成粒子发射器。

<a name="SGYfR"></a>
## Grains颗粒
颗粒工具是一种更高级的粒子系统，用于模拟具有更多物理特性的颗粒，消耗资源更高，相比粒子，它会模拟颗粒与颗粒之间的物理效果，例如沙子、泥浆。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047527124-8ac8ff40-9f0e-41fe-bfa9-389c25357dd9.png#averageHue=%2342413e&clientId=u6ad503fa-7cfa-4&from=paste&height=48&id=u2242df1b&originHeight=48&originWidth=784&originalType=binary&ratio=1&rotation=0&showTitle=false&size=20197&status=done&style=none&taskId=ua2bb4ad8-7f94-40cd-a9f2-935a294853e&title=&width=784)
<a name="eXxuU"></a>
## Vellum布料
Vellum是一个用于模拟布料、软体和其他变形物体的工具集。它可以模拟布料的折叠、撕裂和变形，以及其他物体的动态行为。毛发，沙子，黏体也可以通过vellum来做<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047548326-79f19b27-8f6c-4a8d-a44e-de1592204d0f.png#averageHue=%23404040&clientId=u6ad503fa-7cfa-4&from=paste&height=46&id=uca4a8baf&originHeight=46&originWidth=493&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12531&status=done&style=none&taskId=u22872689-85f1-4e54-819c-12351164f5a&title=&width=493)
<a name="UQd1X"></a>
## Rigid Bodies刚体
刚体工具用于模拟刚体物体的物理行为，如碰撞、重力和动力学。您可以创建刚体对象，并模拟它们在场景中的运动和互动。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047900689-a56852dd-b649-439c-9f85-e4afbfdcab37.png#averageHue=%23434240&clientId=u6ad503fa-7cfa-4&from=paste&height=55&id=u49a12f79&originHeight=55&originWidth=643&originalType=binary&ratio=1&rotation=0&showTitle=false&size=19656&status=done&style=none&taskId=u3d641c3c-d4f9-436d-8334-e5decfb609c&title=&width=643)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047907390-25ac370c-e527-457d-a737-367c9d80abf8.png#averageHue=%2340403f&clientId=u6ad503fa-7cfa-4&from=paste&height=55&id=uabd33aa0&originHeight=55&originWidth=711&originalType=binary&ratio=1&rotation=0&showTitle=false&size=15676&status=done&style=none&taskId=u0df05b36-0ed9-4a2d-ada3-27d5369ef8c&title=&width=711)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689058013341-4b023cc6-573c-45d9-9d05-2a170be35594.png#averageHue=%23424242&clientId=u6ad503fa-7cfa-4&from=paste&height=51&id=ud84e1db5&originHeight=51&originWidth=71&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2647&status=done&style=none&taskId=ufda6611e-daf6-4432-8ad0-a1a4936934d&title=&width=71) MakeBreakable：为选择的刚体物体添加破碎<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689052205976-c8008265-ef72-4d82-9b4f-d23f97f9f434.png#averageHue=%233f3e3e&clientId=u6ad503fa-7cfa-4&from=paste&height=64&id=u820c4b47&originHeight=64&originWidth=81&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3329&status=done&style=none&taskId=u29c883f0-7f30-4deb-837b-1945db3798d&title=&width=81)RBD Instanced Objects： 先选择一个物体A，然后点击此工具，然后选择物体B再按回车，按完回车以后物体A的所有顶点都会被替换成物体B。

<a name="wzsal"></a>
## Particle Fluids 粒子流体
这个工具用于模拟流体的行为，通过将粒子和网格结合起来，可以生成逼真的流体效果，如水、烟雾或液体金属。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689048115292-48d50b41-7189-4ea2-b4b4-77685b619667.png#averageHue=%23404040&clientId=u6ad503fa-7cfa-4&from=paste&height=60&id=u78a5b5db&originHeight=60&originWidth=453&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14643&status=done&style=none&taskId=ud49459b3-ebf0-47f2-9596-dd1c16b0365&title=&width=453)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689048120527-2815f1ae-2b0d-4a25-b634-349a5fd27022.png#averageHue=%23403f3f&clientId=u6ad503fa-7cfa-4&from=paste&height=49&id=u5ccf93af&originHeight=49&originWidth=451&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13357&status=done&style=none&taskId=uacff56cd-92c0-4bce-b729-b5d148935af&title=&width=451)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689054951139-88cfcde0-da30-4684-948e-f28bcdd07aa6.png#averageHue=%233e3e3e&clientId=u6ad503fa-7cfa-4&from=paste&height=60&id=u6216d798&originHeight=60&originWidth=71&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2906&status=done&style=none&taskId=u75ef010d-6031-4416-a987-f76b45fe2d3&title=&width=71)FLIPTank 创建一个水缸![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689054977847-95c939ec-3808-4632-9bb5-d1618366c095.png#averageHue=%238f9bb2&clientId=u6ad503fa-7cfa-4&from=paste&height=208&id=ubdc2bc78&originHeight=550&originWidth=627&originalType=binary&ratio=1&rotation=0&showTitle=false&size=385350&status=done&style=none&taskId=u0759904d-00cd-47de-9f49-17edeb8622a&title=&width=237)

<a name="V9o6z"></a>
## Viscous Fluids粘性流体
粘性流体工具是Particle Fluids的扩展，可以模拟具有更高黏度或粘性特性的流体，如糖浆或蜂蜜。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047573158-250e80d2-ac5b-4b9a-92aa-bf7322c58b23.png#averageHue=%23444241&clientId=u6ad503fa-7cfa-4&from=paste&height=52&id=u7026d1aa&originHeight=52&originWidth=631&originalType=binary&ratio=1&rotation=0&showTitle=false&size=19936&status=done&style=none&taskId=ub322d555-b92c-48b2-be6d-e6b9edef758&title=&width=631)
<a name="YqqHB"></a>
## Oceans海洋
这个工具集用于创建逼真的海洋和水面效果。它可以模拟海浪、波纹、海浪翻滚等效果，并生成逼真的水体表面。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047580614-e0973059-2703-4ed6-be3a-4d0ac18d67e7.png#averageHue=%233d3d3d&clientId=u6ad503fa-7cfa-4&from=paste&height=51&id=u1466064c&originHeight=51&originWidth=490&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11344&status=done&style=none&taskId=u481c3039-a4e5-4948-8708-e367941d442&title=&width=490)
<a name="GqVX1"></a>
## PyroFX火焰和烟雾
PyroFX工具集用于创建逼真的火焰和烟雾效果。它可以模拟火焰的燃烧、烟雾的扩散和交互，并生成逼真的火焰和烟雾效果。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047589685-ca21bea0-df05-438a-9434-1b23c575f908.png#averageHue=%2344413e&clientId=u6ad503fa-7cfa-4&from=paste&height=49&id=u391cedc9&originHeight=49&originWidth=445&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10949&status=done&style=none&taskId=u51b3f215-0c9e-4bcb-b052-16e3a97cd0e&title=&width=445)

<a name="XNVAr"></a>
## FEM
FEM工具集用于模拟弹性和变形物体的行为。它可以模拟弹性体、变形物体的扭曲、弯曲和拉伸，并生成逼真的变形效果。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047965248-d4c249b6-97aa-44cb-bc35-9c0a86b6e14b.png#averageHue=%233e3e3e&clientId=u6ad503fa-7cfa-4&from=paste&height=59&id=u049ecf7a&originHeight=59&originWidth=450&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13132&status=done&style=none&taskId=u8db51c22-25f1-4761-b782-c55d081b3ba&title=&width=450)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047972860-f7619f70-6592-4103-9b93-395209c486ed.png#averageHue=%2341403f&clientId=u6ad503fa-7cfa-4&from=paste&height=53&id=uc4939793&originHeight=53&originWidth=502&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13498&status=done&style=none&taskId=ue01236f1-0b24-4333-b1bc-d36df87b5e5&title=&width=502)
<a name="osjid"></a>
## Wires线条
线条工具用于模拟线条和柔性物体的行为。它可以创建和模拟绳索、电线、海藻等柔性物体，并模拟它们的动态行为。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047988436-78a55797-e6b4-44a2-adb6-75d2ad514df7.png#averageHue=%233f3f3e&clientId=u6ad503fa-7cfa-4&from=paste&height=51&id=u1dbd512f&originHeight=51&originWidth=475&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11450&status=done&style=none&taskId=u01e11f09-8f8c-48e9-8fe4-42792a41ca6&title=&width=475)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689047998940-88a62b7b-56d1-480e-b15e-608dd37619b2.png#averageHue=%23414040&clientId=u6ad503fa-7cfa-4&from=paste&height=56&id=ue6f618c9&originHeight=56&originWidth=537&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13260&status=done&style=none&taskId=ua1b4d17a-8780-4ff9-b7e3-837bd5c2218&title=&width=537)
<a name="zhyXl"></a>
## Crowds群集
Crowds工具集用于创建和模拟大规模的人群效果。它可以模拟人群的移动、交互和行为，并生成逼真的人群场景。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689048015892-e454dfcb-9340-4226-9481-d6a620a85af9.png#averageHue=%23434140&clientId=u6ad503fa-7cfa-4&from=paste&height=51&id=u2285fc29&originHeight=51&originWidth=527&originalType=binary&ratio=1&rotation=0&showTitle=false&size=17578&status=done&style=none&taskId=u694c271d-9527-4b43-b7e6-ecd752294d1&title=&width=527)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689048022519-69084fc3-3785-453b-ade1-897a2828523b.png#averageHue=%23433f3f&clientId=u6ad503fa-7cfa-4&from=paste&height=52&id=u7a29d580&originHeight=52&originWidth=574&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10183&status=done&style=none&taskId=u4268e0eb-d80c-41e5-866b-2ad7471b965&title=&width=574)
<a name="W5wjh"></a>
## Drive Simulation驱动模拟
驱动模拟工具用于模拟和驱动复杂的物体和效果。它可以通过外部力、约束和动画数据来驱动模拟，并生成复杂的动态效果。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689048031676-7f9e6a43-d247-4874-924b-0e015b903151.png#averageHue=%23403f3e&clientId=u6ad503fa-7cfa-4&from=paste&height=59&id=u864e92fb&originHeight=59&originWidth=405&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12549&status=done&style=none&taskId=u2c909bad-3402-43dd-a203-36086cd37cf&title=&width=405)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689048039399-57213f07-079f-4b8f-80a4-52b623fc7eab.png#averageHue=%23414040&clientId=u6ad503fa-7cfa-4&from=paste&height=54&id=u8f8adacd&originHeight=54&originWidth=428&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13692&status=done&style=none&taskId=u255d73b6-ecfe-470b-86b1-b3e6a240239&title=&width=428)
<a name="CC9g8"></a>
# 快捷键与操作
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1688983296559-86b10eca-f3dc-434b-9ae9-f2c8528dae7b.png#averageHue=%23fcfaf8&clientId=u5c4fd87d-e6a3-4&from=paste&height=1161&id=aOdsm&originHeight=1161&originWidth=931&originalType=binary&ratio=1&rotation=0&showTitle=false&size=288455&status=done&style=none&taskId=u0b9afa62-31e9-410e-8065-6ca7f954adf&title=&width=931)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689058423850-c4fa95bc-f76f-47e2-a612-c4453c3f05af.png#averageHue=%2333211d&clientId=u6ad503fa-7cfa-4&from=paste&height=753&id=ua3c4fffe&originHeight=753&originWidth=1052&originalType=binary&ratio=1&rotation=0&showTitle=false&size=721267&status=done&style=none&taskId=u9426299a-ebed-464a-ba87-58254183db6&title=&width=1052)
<a name="N2PXA"></a>
## 视图操作快捷键
<a name="eKfwY"></a>
### 快捷键
空格+f键： 居中显示<br />w键：切换为网格显示<br />e键： 缩放<br />r键：旋转<br />t键： 位移<br />视图模式中按1，2，3，4，5切换透视图，顶视图，前视图，右视图，UV视图<br />9键： 显示geometry对应的group和连接的geometry。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689214808487-bd7725ac-d0c1-44c8-b943-ed61e40b700e.png#averageHue=%23949a8f&clientId=u0b51113a-ff6a-4&from=paste&height=430&id=ufc07a38b&originHeight=430&originWidth=502&originalType=binary&ratio=1&rotation=0&showTitle=false&size=155040&status=done&style=none&taskId=u4675deb6-5883-4286-81e1-f8f44bfb61c&title=&width=502)<br />空格键：切换view视窗模式和select选择编辑模式，如果切换不了就按s键也能进入选择编辑模式<br />ctrl+b：视图最大化，需要在对应视图处按<br />d键：设置选择视图的显示项![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663667735662-95f8016d-6a7f-49eb-81e5-561bb03c7bd3.png#averageHue=%23484848&clientId=u5015aa74-1ea4-4&errorMessage=unknown%20error&from=paste&height=495&id=u321afc6d&originHeight=495&originWidth=743&originalType=binary&ratio=1&rotation=0&showTitle=false&size=70072&status=error&style=none&taskId=ud20e9657-e103-4788-8610-8babf97f7ab&title=&width=743)<br />shift+G键：扩大选择的点边面区域<br />shift+s键：缩小选择的点边面区域<br />快速选择循环点边面：选中一个点边面以后，按a键配合鼠标中键快速选择循环点边面
<a name="VQNlt"></a>
### 操作
将某一窗口最小化：例如想要将属性编辑器缩小就点击图中图标![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663661983206-f83421db-62fa-4c61-bb93-bcae82435e97.png#averageHue=%23333333&clientId=u5c2a535c-7f3e-4&errorMessage=unknown%20error&from=paste&height=893&id=WBF8B&originHeight=893&originWidth=1137&originalType=binary&ratio=1&rotation=0&showTitle=false&size=84774&status=error&style=none&taskId=u5a2d8777-7221-4a81-8393-3890a88d57e&title=&width=1137)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663662030215-d4cfdbae-58fc-4872-8868-e59cd11a9cac.png#averageHue=%23323232&clientId=u5c2a535c-7f3e-4&errorMessage=unknown%20error&from=paste&height=683&id=IQhqE&originHeight=683&originWidth=1097&originalType=binary&ratio=1&rotation=0&showTitle=false&size=53207&status=error&style=none&taskId=u833d11db-d3fd-498f-a40f-3e477fe9c15&title=&width=1097)



<a name="npGdV"></a>
## 网络编辑器快捷键
g键：快速定位到选择的节点<br />h键：定位显示所有的节点<br />l键：一键快速排列<br />令节点对齐：选中要对齐的节点然后按shift+a+鼠标左键按住拖动（上下拖动为竖着对齐，左右拖动为横着对齐）<br />R键：显示与隐藏节点<br />复制节点：ctrl+cv或者alt+鼠标拖动<br />y键：按着不松开启剪刀模式剪断节点之间的连接<br />shift+o：添加注释<br />shift+w：显示大纲<br />shift+c： 打包节点<br />p键：在网络编辑器中快捷显示隐藏属性编辑器![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663662078906-6cb9d917-ced2-4e3c-a957-f6afa888e3f8.png#averageHue=%23333333&clientId=u5c2a535c-7f3e-4&errorMessage=unknown%20error&from=paste&height=639&id=sLnZ3&originHeight=639&originWidth=1113&originalType=binary&ratio=1&rotation=0&showTitle=false&size=66573&status=error&style=none&taskId=u137ff9e5-3237-4839-93ca-afaabaea354&title=&width=1113)
<a name="zZup5"></a>
## 网格编辑器的一些操作
<a name="NMZGD"></a>
### 创建一个节点的引用
使用此功能后会创建一个新的相同节点，新的节点的属性会完全同步旧节点的属性调整。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689134672795-56affba5-9d44-4094-a9ea-27eb14851f29.png#averageHue=%23454039&clientId=u2b227c25-553c-4&from=paste&height=246&id=uadd4f3e0&originHeight=246&originWidth=565&originalType=binary&ratio=1&rotation=0&showTitle=false&size=28677&status=done&style=none&taskId=ua5b0734b-1b72-4b64-8af8-1bc7daa112c&title=&width=565)
<a name="UkPEY"></a>
### 创建参数的引用
先复制要引用的参数![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689134794385-f2679a48-a5f2-4cda-a74a-cc14ed992018.png#averageHue=%23494137&clientId=u2b227c25-553c-4&from=paste&height=209&id=u414db8b4&originHeight=209&originWidth=372&originalType=binary&ratio=1&rotation=0&showTitle=false&size=16844&status=done&style=none&taskId=u41d8c11b-1d59-460c-872c-1b7b8a08afb&title=&width=372)<br />然后在另一个参数中右键使用粘贴，有两种方式，一个是相对路径一个是绝对路径。<br />使用此功能后将会建立双方参数的同步。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689134832342-bd421a14-cbfc-4d02-a4ff-8f16f956d240.png#averageHue=%23403c38&clientId=u2b227c25-553c-4&from=paste&height=340&id=ue4b26d5f&originHeight=340&originWidth=578&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36646&status=done&style=none&taskId=u7d247a7e-69be-4a10-a7f7-3c5db7e2b0e&title=&width=578)
<a name="P8gdF"></a>
## 将VOP中的输入变量变成参数使其可以直接在VOP节点上自定义参数值
在变量处按鼠标中间然后选择Promote Parameter即可创建出来可以用户自定义的参数、<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689241831109-ecc4032c-2541-41c5-83be-43d3021c1970.png#averageHue=%2344413e&clientId=u0b51113a-ff6a-4&from=paste&height=340&id=u705d7c37&originHeight=340&originWidth=434&originalType=binary&ratio=1&rotation=0&showTitle=false&size=28065&status=done&style=none&taskId=udb37a3a6-fd55-405c-aa87-ce3dd65df39&title=&width=434)<br />然后点击变量输入引脚的四边形即可调整参数的类型和名字。<br />添加完参数以后，即可在VOP节点外部调整参数的值。


<a name="NaAeq"></a>
## 动画相关快捷键
alt+鼠标左键点击属性进行k帧，设置关键帧<br />shift+鼠标左键点击属性：进入属性的动画曲线编辑器<br />⬆上箭头键：正序播放动画<br />⬇下箭头键：倒序播放动画

<a name="smR4p"></a>
# 不同网络对应的常用节点
<a name="nFePv"></a>
## GEO(SOP)(建模，程序化建模，K帧，展UV)
<a name="neX0x"></a>
### 建模
null：空节点，主要作用是标记和分类<br />merge：合并<br />transform ： 变换  <br />soft transform ： 带软选择的变换<br />blast：爆破（有删除的作用）<br />fuse: 焊接相邻的点<br />facet：把面与面进行拆分，将有多条边共用的点分离成多个点，需要勾选uniquePoints![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663746774746-d603a37a-6368-4c36-92c0-608661cf6429.png#averageHue=%23424242&clientId=u2b212657-78c4-4&errorMessage=unknown%20error&from=paste&height=34&id=uec3a6324&originHeight=34&originWidth=163&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1655&status=error&style=none&taskId=uda015188-9f3c-43f8-aab0-4aa5144600c&title=&width=163)<br />ends:可以使用这个节点将模型线框显示，需要将close U属性改为Open![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663747682517-bbb52790-06e0-4996-85b9-50ff04f52c21.png#averageHue=%233f3f3f&clientId=u2b212657-78c4-4&errorMessage=unknown%20error&from=paste&height=38&id=udf822390&originHeight=38&originWidth=265&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2361&status=error&style=none&taskId=u15880ef4-1bde-4587-98cd-9ae674a2600&title=&width=265)<br />add:可以将模型删除但只保留点，需要勾选![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663747791647-b52ddd33-f444-4ed9-9e0e-245380cebce8.png#averageHue=%23404040&clientId=u2b212657-78c4-4&errorMessage=unknown%20error&from=paste&height=34&id=ub2763d35&originHeight=34&originWidth=312&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3488&status=error&style=none&taskId=ua327da12-2dac-445b-a8bc-a2d3cbd6cd4&title=&width=312)。<br />add也可以将点连成线：需要在Polygons一栏中选择By Group<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689242224496-6c9efebe-9c6a-462a-a887-f4f6737e4224.png#averageHue=%23373737&clientId=u0b51113a-ff6a-4&from=paste&height=187&id=u4989e598&originHeight=187&originWidth=383&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25596&status=done&style=none&taskId=uec77778d-9bc2-4f38-89a4-a8381028fef&title=&width=383)<br />scatter：模型变点(可以自己设置点的数量)<br />polywire：将线框向外扩展变成网格<br />polyextrude: 挤出<br />polysplit：多切割，以及插入循环边，如果不能交互的话就在视图窗口中按enter键，通过改变path type切换点击切割的模式还是循环边的模式![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689131620240-afc23153-3ed1-4e5e-888e-01b01262dae4.png#averageHue=%235b4e3d&clientId=u2b227c25-553c-4&from=paste&height=77&id=u4cc0e5ef&originHeight=77&originWidth=248&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7540&status=done&style=none&taskId=u4813f39e-24d7-4d80-965c-e25c1969550&title=&width=248)<br />split：分离<br />polybevel：倒角<br />polyfill(polycap)：填充<br />poly frame：输出normal和tangent属性并且可以更改其normal属性和tangent属性的名字，例如可以在tangent属性的名字写成N，这样就相当于使用其tangent属性作为N属性来使用。<br />copy to points ：将模型复制到点上<br />sort：可以用来反转点序号<br />match size: 匹配大小，例如通过一个box为标准来使其他物体大小跟box大小匹配（需要更改一些节点的参数）<br />reverse: 反转，通常用来处理法线<br />attribute create：创建自定义属性<br />attribute randimize ： 添加或设置属性值的随机<br />mountain：翻译为山，往山的形象进行变形，作用是为模型添加变形<br />subdivide: 细分<br />color：添加颜色<br />group：组，可以将顶点或者边等进行打组，在选择节点的情况下可以按\~键然后就可以手动选择需要打组的元素，然后再按回车键进行打组。<br />也可以通过另一个geometry来进行范围的选择：![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689155853946-26709063-411d-45ac-88ea-293871a71db7.png#averageHue=%23464442&clientId=u4909db3d-a257-4&from=paste&height=475&id=u42bbf13c&originHeight=475&originWidth=510&originalType=binary&ratio=1&rotation=0&showTitle=false&size=39742&status=done&style=none&taskId=u288538d7-d7a1-422d-a7f2-a267a3f8890&title=&width=510)![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689155865380-583e139f-f199-4955-9ae7-e681b4e37159.png#averageHue=%23424241&clientId=u4909db3d-a257-4&from=paste&height=475&id=u2ada29a0&originHeight=475&originWidth=689&originalType=binary&ratio=1&rotation=0&showTitle=false&size=45432&status=done&style=none&taskId=udaebe27d-5670-48a1-84f4-b2cc6fd846f&title=&width=689)<br />L-System：提供了很多预设，可以快速做出一些形状，比如树，树丛，闪电等<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689218131712-b454f98d-3a06-484b-9eb6-85ebfccacb89.png#averageHue=%23393735&clientId=u0b51113a-ff6a-4&from=paste&height=151&id=u11757cd0&originHeight=151&originWidth=298&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9939&status=done&style=none&taskId=ub77eb91c-5ad5-41bd-a86d-a18d7794499&title=&width=298)![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689218112636-63429f71-6df6-4db8-aa7a-1b470da11743.png#averageHue=%233d3b3b&clientId=u0b51113a-ff6a-4&from=paste&height=868&id=uc1eb3cc8&originHeight=1168&originWidth=444&originalType=binary&ratio=1&rotation=0&showTitle=false&size=89665&status=done&style=none&taskId=u7efbaf37-b269-4e3c-8b85-9bba80fc419&title=&width=330)<br />pack：打包，打包后组成元素变成1![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689218298841-e4185e88-2b99-423d-b678-3e19036b6fa7.png#averageHue=%232a2c37&clientId=u0b51113a-ff6a-4&from=paste&height=120&id=uc5e7bba8&originHeight=120&originWidth=155&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5759&status=done&style=none&taskId=u34710503-d460-4cbf-b5ce-859b69771da&title=&width=155)<br />resample：重新采样，可以改变曲线的组成，例如让曲线的点更多。<br />object merge：将obj层级下的其他geometry带到另一个geometry层级下<br />switch：可以控制两个节点之间切换显示<br />magnet：磁力配合metaball来制作geometry与metaball相互作用的磁力效果<br />skin: skin节点可以将线变成面![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689239491649-651323c6-7a8f-4f31-b81c-221a54b3918e.png#averageHue=%23a1a8ac&clientId=u0b51113a-ff6a-4&from=paste&height=166&id=u7dd50d25&originHeight=166&originWidth=212&originalType=binary&ratio=1&rotation=0&showTitle=false&size=29012&status=done&style=none&taskId=u458d6b47-4f57-456a-a784-5c3f56c26dc&title=&width=212)![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689239493799-e6627735-8f73-4dc7-b077-e7d510915bcf.png#averageHue=%23acadac&clientId=u0b51113a-ff6a-4&from=paste&height=165&id=u20bee3ed&originHeight=165&originWidth=208&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27426&status=done&style=none&taskId=ub8e8a114-a42a-4bea-8776-d6d6fc53adc&title=&width=208)<br />group promote：切换组的类型<br />convert： 转换类型<br />connectivity： 新增一个属性（默认是class），将merge到一起的geometry按照顺序给0\~（geometry个数-1）的值，例如这里将两个box合并后给connectivity后，第一个box的点（或面）的class属性为0，第二个box的点（或面）的class属性为1![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1690191324087-f1663acc-835d-4cfd-bee1-7331d11ea0f4.png#averageHue=%23333333&clientId=u48f6dd24-7c60-4&from=paste&height=364&id=u12e3b5a1&originHeight=364&originWidth=143&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4167&status=done&style=none&taskId=u0da282e0-418a-4b77-8cbf-53660a17875&title=&width=143)。<br />collisionSource：通过输入后输出一个geo一个vdb

<a name="uLtUS"></a>
### UV
UV Texture：对geometry进行UV的投射,19.5测试的是在投射的时候同时能够显示出来UV的贴图18.5则不会显示出来。<br />UV Quick Shade : 赋予UV检查的Shader方便观察。


<a name="ajq2u"></a>
### 地形
下面的这些前面的HeightField都可以打hf缩写来快速定位到类型<br />HeightField：初始地形，平面网格<br />HeightField Noise : 专门针对地形的Noise<br />HeightField Distort by Noise： 对Noise进行扭曲<br />HeightField Transform：专门针对地形的移动节点<br />HeightField Erode： 模拟侵蚀（属于解算，通过移动关键帧可以看出来）<br />HeightField Flow Field：添加水流的影响![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689230248827-58b607a1-afe9-4ebe-9d91-4a0e8d48ed5a.png#averageHue=%237c5718&clientId=u0b51113a-ff6a-4&from=paste&height=128&id=u69df612c&originHeight=276&originWidth=572&originalType=binary&ratio=1&rotation=0&showTitle=false&size=154131&status=done&style=none&taskId=u447c83a8-4a2a-4b38-a4cd-4460a467d8c&title=&width=265)（红色）<br />HeightField Visualize：使为地形添加的不同细节更加形象话的表示出来（通过自定义的颜色）<br />Convert HeightField ：将地形转换成网格体<br />Time Shift：如果前面有模拟，那么可以通过这个节点停掉解算过程而得到需要的某一帧的效果。
<a name="u2Xfb"></a>
## 动画
time shift：记录输入的对象的动画，然后让这个动画的帧数由timeshift节点的属性来操控。可以通过给timeshift的属性进行K帧达到给动画的某一阶段的动画进行倍速的效果。


<a name="oMeyk"></a>
### 制作粒子可能用得到的
trail:记录输入的点的前一帧（或前几帧，可以自定义），然后会把这些记录显示在窗口上。也可以通过它来得到对象的速度属性，不过需要修改类型。![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1690535301265-4c0c9a92-5461-483d-859e-fb857e0d0776.png#averageHue=%23383736&clientId=u182835ed-113b-4&from=paste&height=210&id=u323329f3&originHeight=210&originWidth=716&originalType=binary&ratio=1&rotation=0&showTitle=false&size=18116&status=done&style=none&taskId=uaebcb37e-d114-40dd-98aa-72fc46cbaa8&title=&width=716)<br />pointReplicate: 基于输入的sop的点，来为sop的点周围来生成点云。并且可以继承点的速度（在attribute里面），能够控制点云的形状数量的noise



<a name="WMusM"></a>
## VOP（VEX Builder）
<a name="TiVHj"></a>
### VOP变量颜色对应类型介绍
先介绍一下不同颜色对应的类型：<br />没有布尔类型，布尔类型用int类型的0和1来代替了<br />绿色：vector<br />青色：float<br />深青色：floata   浮点数数组<br />蓝色：int<br />棕黄色：string
<a name="VnSyJ"></a>
### VOP变量名字对应
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689242456393-191f7ff8-e461-4c0c-b21e-baab2a044301.png#averageHue=%23464545&clientId=u0b51113a-ff6a-4&from=paste&height=763&id=uc5a4f31d&originHeight=763&originWidth=438&originalType=binary&ratio=1&rotation=0&showTitle=false&size=32437&status=done&style=none&taskId=ud999579b-86b9-4530-96b9-35ba3729bdc&title=&width=438)<br />P对应顶点属性为vector类型<br />Cd对应颜色属性为vector类型<br />ptnum意思是point number 也就是点序号，int类型<br />numpt意思是number of point 也就是点的总数量，int类型
<a name="wHGgV"></a>
### VOP节点介绍
VOP节点有很多种<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689151972832-5c5e48cc-2121-4cd3-a0b4-2d70e5194fe8.png#averageHue=%23444443&clientId=u4909db3d-a257-4&from=paste&height=149&id=u73d68979&originHeight=149&originWidth=175&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11172&status=done&style=none&taskId=u3f8d51d3-532d-4437-a000-d8d986b1f59&title=&width=175)<br />Point VOP 和 Primitive VOP 和 Vertex VOP都属于Attribute VOP,只是这三个默认的类型不同。
<a name="LkkpL"></a>
#### Attribute VOP
attributeVOP，这个是一个可以处理各种属性的节点，在节点里面可以通过可视化编程网络设置属性。<br />bind：读取属性<br />bind export： 输出属性（创建一个新属性）（跟bind节点是一样的，只不过把bind里的默认参数修改了一下）<br />random：随机<br />fit range：将数值限制在一个范围内<br />round to integer：四舍五入<br />multply add constant：乘和添加常数，配合random调节随机值<br />switch： 通过接收的数来选择自身所具有的对应位置的数来进行输出<br />subtract： 减（要求有两个输入）<br />subtract Constant：减一个常数（只需要一个输入）<br />mix：混合，跟UE材质蓝图的lerp是一个道理
<a name="Jvfsu"></a>
## out（ROP）(渲染输出)
mantra：houdini自带的渲染器节点![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689060197542-f982d1d5-d00b-47bc-9459-94ff50440ac6.png#averageHue=%23393837&clientId=u6ad503fa-7cfa-4&from=paste&height=825&id=Meet3&originHeight=825&originWidth=480&originalType=binary&ratio=1&rotation=0&showTitle=false&size=89232&status=done&style=none&taskId=uc94e0acf-2310-4867-978f-337e0bfae71&title=&width=480)
<a name="KG6F0"></a>
## mat（材质网络）
mat是为物体添加着色器和材质的网络<br />创建好shader以后可以将节点拖入到视图中的物体中可以快速地赋予材质<br />classicshader 经典shader
<a name="zpg3i"></a>
## dop（动力学解算）（烟火水粒子）
gravity：引力，重力，9.8<br />staticObject:赋予SOP路径后生成被动碰撞体
<a name="KVZ6A"></a>
### 粒子
popobject：配合popSolver使用，使其能够与DOP环境的其他对象正确交互<br />popSource：用于通过几何体生成粒子的节点<br />popCollisionDetect：用于粒子的碰撞并设置碰撞后的反应<br />popDrag：为粒子添加类似风阻的效果<br />popForce：为粒子添加新的作用力



<a name="DSIEe"></a>
### 解算器节点
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689064091029-2fcd79cc-edd2-4631-a26d-de96b91906dc.png#averageHue=%23f8f5f0&clientId=u6ad503fa-7cfa-4&from=paste&height=436&id=udefb0eaa&originHeight=436&originWidth=427&originalType=binary&ratio=1&rotation=0&showTitle=false&size=77449&status=done&style=none&taskId=ufdf2f652-568d-4456-9b4e-de45ba10820&title=&width=427)<br />rigid body solver：专门用于处理刚体物体的运动、碰撞和相互作用。<br />刚体是指在运动过程中形状和体积保持不变的物体，它们的运动受到物理力学规律的约束。<br />static solver：使其变成被动的碰撞体，但不受模拟的影响。例如，建筑物、地形、静态障碍物等都可以被视为静态物体。<br />flip solver：流体解算器，计算飞溅和波浪效应<br />Whitewater solver：在flip solve的基础上创建泡沫喷雾和气泡<br />vellum solver：属于POP solver类型，用于支持布料，头发，颗粒<br />POP Solver：用于粒子和颗粒，也可以用来模拟软体和布料。<br />Wire Solver： 用于解算毛发和皮毛或其他例如船的索具或树枝的索具等丝状物体。<br />Finite Element Solver：用于模拟四面体的材料和固体，用于模拟肌肉，软体，破碎的木头<br />Cloth Solver：对与变形物体作用的布料进行模拟<br />SOP Solver：用于SOP网络，随着时间的推移而改变物体的形状。例如墙壁被物体撞击而产生凹痕。
<a name="pUZWY"></a>
# 文件管理规范和场景比例
<a name="aoeGv"></a>
## 场景比例
houdini的场景比例是一个单位是1m，其他dcc软件的单位一般是1cm。<br />修改场景比例的方法（houdini因为计算原因所以更推荐使用m为单位）：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689144934395-1f11c023-9f25-4bdd-b6a3-31bf3a7397b1.png#averageHue=%234c463d&clientId=u2b227c25-553c-4&from=paste&height=255&id=ub2f9f4c8&originHeight=255&originWidth=584&originalType=binary&ratio=1&rotation=0&showTitle=false&size=45467&status=done&style=none&taskId=ufa9fb9df-2748-4bc0-b2ce-609e246613d&title=&width=584)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689144918467-548b3ab2-c1fc-4337-8275-b52c26471076.png#averageHue=%234f4e4e&clientId=u2b227c25-553c-4&from=paste&height=328&id=ud6088751&originHeight=328&originWidth=586&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33088&status=done&style=none&taskId=u5e89cd63-cdbb-4d6a-bb8a-1905f5d6828&title=&width=586)
<a name="AXo7u"></a>
## 文件管理规范
<a name="j88ZV"></a>
### 文件命名
内容_大版本_小版本.hip<br />v是version的意思<br />t是take的意思<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689146121770-780697f0-4a57-4566-acef-033793ebbbfc.png#averageHue=%23b2a75f&clientId=u2b227c25-553c-4&from=paste&height=128&id=u08afc83c&originHeight=128&originWidth=1227&originalType=binary&ratio=1&rotation=0&showTitle=false&size=75118&status=done&style=none&taskId=u9868cf07-4ea7-4e03-bef7-d92b14b5d45&title=&width=1227)
<a name="LUrJl"></a>
### 文件节点
经常使用的文件节点有两个，一个是file 一个是filecache<br />一般file只使用它的读取功能<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689147333670-5e2fe2b1-4ef4-464a-9307-acb836da0ef6.png#averageHue=%23424039&clientId=u2b227c25-553c-4&from=paste&height=201&id=u784b0172&originHeight=201&originWidth=725&originalType=binary&ratio=1&rotation=0&showTitle=false&size=22171&status=done&style=none&taskId=uf1c083d2-1049-4d6a-ba7b-f3e9e767d87&title=&width=725)<br />filecache：<br />这里的$HIPNAME和$OS和$HIP都是环境变量。 $HIPNAME是项目文件名称，$OS是filecache这个节点的名称，$HIP是项目文件的目录路径,$F是帧数<br />houdini项目文件名字的后缀就是hip<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689147406721-17ff8f42-fc18-42be-9e4e-1784e759a157.png#averageHue=%23383838&clientId=u2b227c25-553c-4&from=paste&height=467&id=u933bae38&originHeight=467&originWidth=748&originalType=binary&ratio=1&rotation=0&showTitle=false&size=50525&status=done&style=none&taskId=u8335ba63-08bc-4b65-ac07-6c4bfa33728&title=&width=748)
<a name="ZVfYy"></a>
# 扩展节点布局预设
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689149877195-6a53a1a9-afc2-483c-85bd-85a1ca08991e.png#averageHue=%233a3835&clientId=u4909db3d-a257-4&from=paste&height=252&id=ub070e94d&originHeight=252&originWidth=1116&originalType=binary&ratio=1&rotation=0&showTitle=false&size=52566&status=done&style=none&taskId=u420e674d-5c16-40c7-8dc0-072a628999b&title=&width=1116)<br />在节点上使用编辑参数界面功能<br />左边是能够添加的参数列表，中间是属性界面中已经存在的参数列表，右边是改变参数的一些属性.<br />也可以通过鼠标左键拖动其他节点的属性参数至设置参数的这个列表使这个节点可以控制其他节点的属性参数。（比如可以将通过节点做好的模型进行打包，然后在打包节点里的模型节点的属性参数拖入到打包节点里，这样就可以在打包节点中调整模型的细节；也可以在打包节点中新增新的属性然后将打包节点的属性值复制到模型里的节点的属性上面）<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689150395682-cdb2b59f-ae84-4f0b-96ad-a98f86a489f3.png#averageHue=%23403f3f&clientId=u4909db3d-a257-4&from=paste&height=874&id=ub5d1e80a&originHeight=874&originWidth=1234&originalType=binary&ratio=1&rotation=0&showTitle=false&size=236244&status=done&style=none&taskId=u1d4cc4bf-cc4b-4eb1-8392-908cc531b24&title=&width=1234)<br />调整好的节点界面可以保存预设，或者替换默认预设<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689150710208-46863586-3560-4948-8fa0-ecd6cd326bde.png#averageHue=%233e3c39&clientId=u4909db3d-a257-4&from=paste&height=430&id=ue32dbeda&originHeight=430&originWidth=550&originalType=binary&ratio=1&rotation=0&showTitle=false&size=41303&status=done&style=none&taskId=u90186905-a9bf-416a-80b7-f85fe240939&title=&width=550)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689150731498-e65088a0-ca8b-4d78-900b-901ed64bc41e.png#averageHue=%23646260&clientId=u4909db3d-a257-4&from=paste&height=159&id=u698b4bb0&originHeight=159&originWidth=399&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14301&status=done&style=none&taskId=u00d4fcc3-94d7-4ae5-9fe4-c007047650f&title=&width=399)
<a name="U09wQ"></a>
# HScript 
<a name="BSsV6"></a>
## @和$的区别
@是VEX的变量，$是HScript的变量<br />通常通过@来使用局部的变量(例如访问几何属性),$来使用全局的变量(例如访问houdini的帧数，文件路径)。
<a name="hq9lB"></a>
## 全局变量举例
houdini文档上提供的一些：<br />[https://www.sidefx.com/docs/houdini/network/expressions.html](https://www.sidefx.com/docs/houdini/network/expressions.html)<br />文档上没有的：<br />$CEX,$CEY,$CEZ分别表示一个物体的中心的XYZ在坐标系下的对应的X或Y或Z的值
<a name="T1NTL"></a>
## 函数
[https://www.sidefx.com/docs/houdini/expressions/index.html](https://www.sidefx.com/docs/houdini/expressions/index.html)<br />常用的函数：<br />rand<br />stamp<br />fit<br />fit01
<a name="RACTF"></a>
# VEX
VOP节点是将VEX可视化了，如果想要直接写VEX可以使用Point Wrangle节点。
<a name="tm2KR"></a>
## 浏览连接好的VOP的VEX代码
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1689563138289-fda09f3b-82ec-4911-b11b-7d3003ba3e33.png#averageHue=%234c453c&clientId=u8c90dfb8-4e44-4&from=paste&height=215&id=u1723ebdc&originHeight=215&originWidth=429&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25295&status=done&style=none&taskId=u85523f0d-9b5e-435e-a0e6-c423413a8c7&title=&width=429)
<a name="lUlRk"></a>
# VOP里的Noise的介绍
首先需要知道的是Noise不是完全随机的计算，例如针对一系列点添加Noise时，Noise控制的每个点和上一个点的变化差别。
<a name="HcNqw"></a>
## 不同NoiseType的区别
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1690390338743-74b1d669-ceeb-48d0-87ff-febbc1cc0be0.png#averageHue=%23b2a593&clientId=uf63b0efc-1872-4&from=paste&height=763&id=ud6666b83&originHeight=1145&originWidth=2693&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=1128504&status=done&style=none&taskId=uc73e4ce0-be8b-40eb-923c-2da73b7a1ec&title=&width=1795.3333333333333)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1690390366436-88d73d1b-cf5b-4411-bca1-5bae50ac9f3f.png#averageHue=%23a5a3a1&clientId=uf63b0efc-1872-4&from=paste&height=998&id=u682f120f&originHeight=1497&originWidth=2871&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=1656225&status=done&style=none&taskId=ub5d57e8b-9f10-4ffb-bbf8-e6800904627&title=&width=1914)
<a name="UF170"></a>
## Noise的一些参数
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1690388461405-429b1aba-f4da-4e7a-a3a0-87ed4c3ccc88.png#averageHue=%23323232&clientId=uf63b0efc-1872-4&from=paste&height=188&id=u02961c8f&originHeight=282&originWidth=1153&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=24558&status=done&style=none&taskId=u30f6f194-24ec-4c06-8c8e-80eb95be2ce&title=&width=768.6666666666666)<br />frequency是频率，频率在0\~1之间调整可以看到明显的区别，越高变化的次数越多<br />Amplitude意思是振幅，是指变化的幅度，正一和负一是完全相反的<br />roughness是粗糙度，0\~1之间粗糙度越高变化的越明显<br />Attenuation是衰减系数， 官方解释是Flattens the noise to prevent extreme spikes by damping the values. Higher values create a smoother look.<br />Turbulence翻译是湍流，可以理解为控制Noise的Noise，也就是为Noise再添加Noise











