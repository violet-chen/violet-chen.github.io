---
title: Maya绑定
tags: Maya
categories: DCC软件
abbrlink: bbd5d1e3
date: 2024-07-21 13:40:00
---
<meta name="referrer" content="no-referrer" />

<a name="Tn5Qr"></a>
# transform节点
使用ctrl+g打一个空组，这个空组就是最简单的transform节点，transform节点拥有移动旋转缩放这些属性。<br />一个模型是由transform节点和shape节点共同组成的，shape决定模型的形状，transform决定模型的移动旋转缩放，transform节点为shape节点的父级。
<a name="LVCHR"></a>
# 父子层级关系
移动旋转缩放的数值都是在相对位置下的数值，父物体进行的任何的移动旋转缩放都不会影响到子物体的数值。<br />当父物体进行旋转的同时子物体的坐标系也会相应的发生变化，因此有时候会出现，在世界坐标系下朝一个轴移动子物体，但是显示的是子物体有两个坐标轴数值发生变化（因为子物体使用的是相对坐标系）。
<a name="Q5jw4"></a>
# 移动旋转缩放之间的关系
移动是旋转的父物体，旋转是缩放的父物体。
<a name="NnxOl"></a>
# 使用功能时选择的物体的先后顺序以及功能介绍
<a name="SBu5u"></a>
## p键决定层级关系
使用p键时会以最后选择的物体当父级，其余的选择物体都作为最后选择的物体的子级
<a name="Pkc4n"></a>
## blendshape
最后选择的物体是需要进行变形的物体，前面选择的是变形的目标。前面如果选择了多个物体，那么会分开创建多个变形目标。
<a name="m3YgD"></a>
## 约束
最后选择的是被约束的物体（子），被约束的物体会带有约束节点，在约束节点中可以控制约束物体对被约束物体的影响权重![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670217536060-ad82bcd7-0f17-4473-98c9-ee0fb165009a.png#averageHue=%23484241&clientId=uf4d82161-efcf-4&from=paste&height=176&id=u69a48566&originHeight=158&originWidth=296&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7358&status=done&style=none&taskId=ua68c44b7-9cb2-4d52-9f1d-8e9377af5d9&title=&width=328.8888976014693)，权重的计算：平均，例如这里数值都为一，那么各占二分之一，也就是50%
<a name="gYChr"></a>
## 表达式（不推荐，了解即可）
表达式是不需要在乎选择顺序的<br />表达式使用方法：首先选中要进行表达式计算的物体，然后选一个属性，然后在edit栏中找到expression editor<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670217729877-0b481305-a4c4-438e-a12e-e8f67fab7796.png#averageHue=%234e514f&clientId=uf4d82161-efcf-4&from=paste&height=137&id=ubdc3c003&originHeight=123&originWidth=426&originalType=binary&ratio=1&rotation=0&showTitle=false&size=23707&status=done&style=none&taskId=ue69569e8-fd3a-446a-9faa-a3620971bb8&title=&width=473.3333458723849)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670217938545-81a94081-a3fb-42f8-a228-2538f5749ea4.png#averageHue=%234d504d&clientId=uf4d82161-efcf-4&from=paste&height=827&id=ud6311239&originHeight=744&originWidth=803&originalType=binary&ratio=1&rotation=0&showTitle=false&size=125261&status=done&style=none&taskId=uc335e098-db46-476c-b261-b1e5801a1c8&title=&width=892.22224585804)


<a name="Mn4S5"></a>
# 约束，父子层级关系，属性连接，驱动关键帧，表达式之间的区别
<a name="QNPDu"></a>
## 父子约束与父子层级关系之间的区别
1.父子约束不对缩放进行控制<br />2.父子约束中被约束的物体的位置旋转信息都记录在约束节点上，因此针对被约束物体进行的移动旋转不会记录。而拥有父子层级关系的物体的情况是：子物体的移动旋转缩放都是自由的，只是父物体进行移动旋转缩放时子物体也会随着变化。<br />3.约束的优先级比父子层级关系高，当父子层级关系与约束同时存在时，优先使用约束的计算情况
<a name="BcfgH"></a>
## 数值的计算区别
约束看的是世界位置<br />属性连接，驱动关键帧，表达式只针对数值<br />父子关系看的是相对位置
<a name="X6jLR"></a>
# 约束的删除过程
直接delete掉约束节点
<a name="NedpU"></a>
# 控制器创建过程
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670212442477-4d720069-5b65-4bfb-8eb7-7830c2ccee9b.png#averageHue=%238191a3&clientId=uf4d82161-efcf-4&from=paste&height=433&id=ud2b9ead6&originHeight=390&originWidth=806&originalType=binary&ratio=1&rotation=0&showTitle=false&size=154852&status=done&style=none&taskId=u0e0c3759-2efc-4cb9-9b17-8c67e4171ab&title=&width=895.5555792796765)
<a name="FVJGm"></a>
# 匹配transformations功能介绍
将所有选择的物体的位移旋转缩放都设置为最后一个选择的物体的数值。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673598402928-4e8ff13b-38be-4e7a-9736-b85acad81b1e.png#averageHue=%2353504f&clientId=u28c346ee-8da3-4&from=paste&height=246&id=u367193f4&originHeight=246&originWidth=461&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25041&status=done&style=none&taskId=u67ce78a4-019d-4119-a6e7-3d97eca7bde&title=&width=461)
<a name="NDP91"></a>
# 修改物体的线框颜色步骤
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673598543851-c9dd3f11-8aa6-4dcf-8657-b9d2a2c84ace.png#averageHue=%234f4d4d&clientId=u28c346ee-8da3-4&from=paste&height=772&id=ucc431bc9&originHeight=772&originWidth=542&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42538&status=done&style=none&taskId=u408876cb-77b3-4383-ba7e-2904b757868&title=&width=542)
<a name="yVlg0"></a>
# 关节
<a name="N6Nbi"></a>
## 关节的介绍
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673258410606-e095c674-40b4-47d3-807c-d7d15313378f.png#averageHue=%2316110f&clientId=u66a221f8-cbf0-4&from=paste&height=556&id=yYqD3&originHeight=445&originWidth=872&originalType=binary&ratio=1&rotation=0&showTitle=false&size=123017&status=done&style=none&taskId=udbcfee9a-000f-45fd-97fb-11e660ce8fc&title=&width=1089.9999837577345)<br />关节的位移在冻结坐标系的时候，不会归零，旋转缩放能够归零，新增加的这个joint orient 的作用就是为了让旋转数值能为0，然后关节自带一个属性InverseScale目的是抵消冻结坐标系![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673258437041-3dbb1f61-28e4-4e27-af4b-52cae5726d35.png#averageHue=%2321130f&clientId=u66a221f8-cbf0-4&from=paste&height=295&id=Ot2uf&originHeight=236&originWidth=822&originalType=binary&ratio=1&rotation=0&showTitle=false&size=73071&status=done&style=none&taskId=uf3578f4e-7491-4569-8f9e-6a02ff49986&title=&width=1027.499984689057)<br />透过网格体显示关节：![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673258917333-2634fa7c-d218-4aad-aa42-2155e50f11ec.png#averageHue=%23545353&clientId=u9ad9c0e9-3d00-4&from=paste&height=269&id=MHNtz&originHeight=215&originWidth=447&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7018&status=done&style=none&taskId=u5dda31eb-6cda-497a-9951-10ee80288ac&title=&width=558.7499916739763)
<a name="zTdFD"></a>
## 关节定向
关节定向调整的是关节的坐标轴的方向<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673576217910-8fe1f174-accd-46ad-9174-ef2dd9d6e62c.png#averageHue=%235c5c5a&clientId=ue3611319-9eae-4&from=paste&height=273&id=WbcID&originHeight=273&originWidth=358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=70991&status=done&style=none&taskId=ufe86abbd-d60d-4432-8576-4390f8f673f&title=&width=358)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673577878554-0ce4507d-b69c-4a93-b0e6-9ac834b64729.png#averageHue=%23555454&clientId=ue3611319-9eae-4&from=paste&height=515&id=dZLIu&originHeight=515&originWidth=739&originalType=binary&ratio=1&rotation=0&showTitle=false&size=111005&status=done&style=none&taskId=u17e5cec2-67ac-498d-9b68-993295717b8&title=&width=739)
<a name="l09B1"></a>
##  关节镜像
如果选择有父物体的子关节进行镜像的话，新创建出来的镜像关节也会以那个关节为父关节。<br />关节镜像不能批量镜像，镜像后再选择其他的按G重复上一次操作。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673578129859-6a12ebe9-1b6f-4e78-ba5c-29d422c5eb26.png#averageHue=%23676663&clientId=ue3611319-9eae-4&from=paste&height=421&id=fHkX1&originHeight=421&originWidth=767&originalType=binary&ratio=1&rotation=0&showTitle=false&size=84032&status=done&style=none&taskId=u6149bc9e-ca9b-404c-be28-2e7c2703bc5&title=&width=767)
<a name="mecrK"></a>
# IK手柄
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671516712022-aa897777-850d-4232-b26f-cc6ddb6743c3.png#averageHue=%235a5857&clientId=u5317e7fd-928b-4&from=paste&height=326&id=udcf2be53&originHeight=293&originWidth=469&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13065&status=done&style=none&taskId=ua06790f4-c5e6-4921-9f91-bff4286295d&title=&width=521.1111249158415)<br />创建时先选择根关节后选择子关节
<a name="uGZ5z"></a>
## Single-Chain Solver
单一旋转平面，IK手柄的首端和尾端组成一个平面，反求关节位置时依靠平面计算。平面的改变通过更改手柄的旋转来实现。<br />一般使用在两个关节组成的骨骼
<a name="FNOwK"></a>
## Rotate-Plane Solver
多一个极向量，IK手柄的首端和尾端和极向量三者组成一个平面，反求关节位置时依靠平面计算。平面的改变通过更改极向量的位置来改变<br />一般使用在多个关节组成的骨骼<br />白色指向的就是极向量的方向<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671517435221-dcb6ae72-643a-41a2-878b-8aba83293d12.png#averageHue=%235e5b5b&clientId=u5317e7fd-928b-4&from=paste&height=417&id=ufb9efb7d&originHeight=375&originWidth=608&originalType=binary&ratio=1&rotation=0&showTitle=false&size=15936&status=done&style=none&taskId=u579a9763-5522-4c8b-b8c8-bf3037d8d06&title=&width=675.5555734516666)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671517753572-6fe72f30-2825-44e2-86d0-c10183003ca0.png#averageHue=%2344403f&clientId=u5317e7fd-928b-4&from=paste&height=370&id=uf5bdb171&originHeight=333&originWidth=310&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12604&status=done&style=none&taskId=u34c641e1-fd12-4db6-9116-d2f82db5b94&title=&width=344.4444535691064)<br />可以通过创建定位器与IK手柄进行极向量约束（先选择定位器后选择ik手柄）![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671517896461-b54e9a46-449d-4d26-9ec5-44d845a3ce67.png#averageHue=%235c5c5c&clientId=u5317e7fd-928b-4&from=paste&height=681&id=u6c824887&originHeight=613&originWidth=562&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7795&status=done&style=none&taskId=uf02be324-ea0f-4a3d-9499-432f02a01b8&title=&width=624.4444609865734)
<a name="ry1kB"></a>
## IK Spline Handle
SplineIK一般用于多个关节组合的关节链（人的脊椎，蛇，龙等）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671518819593-c1c03815-b05c-4c03-bb85-9f84aaffda5e.png#averageHue=%23565251&clientId=u5317e7fd-928b-4&from=paste&height=487&id=uba8bd816&originHeight=438&originWidth=242&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14652&status=done&style=none&taskId=u37b02980-92eb-43b3-98d8-90c69d5bb1e&title=&width=268.8888960120121)<br />使用的选择顺序： 先选择根关节后选择子关节，最后选择曲线(如果不使用自动创建曲线选项的话)（不是直接点是ctrl+鼠标点击加选）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671518978840-21644317-cb3e-4e8f-a276-072a5de24296.png#averageHue=%235d5b5a&clientId=u5317e7fd-928b-4&from=paste&height=330&id=u4b89bd63&originHeight=297&originWidth=511&originalType=binary&ratio=1&rotation=0&showTitle=false&size=22987&status=done&style=none&taskId=u8e29af4f-7e61-48b6-a1dc-f3d7e627dc8&title=&width=567.7777928187527)
<a name="oy9n8"></a>
# IKFK融合
IKFK融合有两种方式，一种是通过约束，另一种是通过blend color
<a name="Xy32X"></a>
## 约束方式
首先需要考虑的是，需不需要关节的位移，如果需要关节的位移就使用父子约束或者点约束。但是使用父子约束或者点约束会产生一个问题。当IKFKBlend的数值为0\~1的中间值时，maya会自动计算位置,这个计算的位置是最短路径位置（会导致关节的长度发生改变）。<br />1.先进行约束，分别对无IKFK手柄的整体，手肘，手腕进行旋转约束（最后选择）,然后更改插值方式为shortest<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673850121885-71c26598-b038-4a50-a2f4-a16c62a89260.png#averageHue=%23505653&clientId=ucf2e48f1-0923-4&from=paste&height=733&id=uca8b94eb&originHeight=733&originWidth=2234&originalType=binary&ratio=1&rotation=0&showTitle=false&size=590586&status=done&style=none&taskId=ub8f1826f-ee92-43c1-a7ba-02101b0d46f&title=&width=2234)<br />2.进行属性的连接![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673850817702-a5a9fd10-6815-4cd5-8133-175f956b46a5.png#averageHue=%23373030&clientId=ucf2e48f1-0923-4&from=paste&height=1093&id=u918e99e0&originHeight=1093&originWidth=1831&originalType=binary&ratio=1&rotation=0&showTitle=false&size=666339&status=done&style=none&taskId=ue04c019f-5b4d-4239-8fb8-07f735f0948&title=&width=1831)
<a name="tM5E3"></a>
# skinCluster
选择骨骼和模型（顺序无所谓）然后使用bind skin功能进行蒙皮，功能选项设置推荐如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673946303980-cffc4ca2-0722-44fe-b693-e69070530ede.png#averageHue=%23555554&clientId=u729b1e5f-1fd5-4&from=paste&height=382&id=u0484bcd7&originHeight=382&originWidth=548&originalType=binary&ratio=1&rotation=0&showTitle=false&size=18710&status=done&style=none&taskId=u0a6a0514-fb5c-465e-8bca-b48935d3ed8&title=&width=548)<br />蒙皮后会生成skinCluster节点<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673946593477-dc346536-3cbd-42a2-8536-6f4dd3cd78de.png#averageHue=%2358473b&clientId=u729b1e5f-1fd5-4&from=paste&height=1048&id=u1f9f35df&originHeight=1048&originWidth=2088&originalType=binary&ratio=1&rotation=0&showTitle=false&size=662250&status=done&style=none&taskId=ua7155168-e8e2-4c35-90cc-6c64a7cfd0c&title=&width=2088)
<a name="q17KV"></a>
# addInfluence
这个是蒙皮完以后如果需要新添加关节就使用这个功能，推荐选项设置如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673949125394-0b0e6326-7091-4ed6-8ea5-fd3da464da13.png#averageHue=%23515151&clientId=u729b1e5f-1fd5-4&from=paste&height=466&id=u389c67fc&originHeight=466&originWidth=667&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63575&status=done&style=none&taskId=u748f487f-5e95-418e-91e9-12035db399e&title=&width=667)
<a name="IUOjg"></a>
# 刷权重
选中已经蒙皮的皮肤，然后右键找到Paint Skin Weights Tool<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674008708447-3780340e-fa6d-47c6-ad37-556ce56d6658.png#averageHue=%236c8092&clientId=u0af6a990-500b-4&from=paste&height=322&id=u43673dc3&originHeight=322&originWidth=711&originalType=binary&ratio=1&rotation=0&showTitle=false&size=128265&status=done&style=none&taskId=u1444a44b-2812-4a6c-bab9-2786769efcf&title=&width=711)
<a name="XdKgG"></a>
# 变形器
<a name="cXJX7"></a>
## BlendShape
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674021502267-8b64365c-ed79-474d-8ccc-f44b1d000af6.png#averageHue=%23514f4f&clientId=u0af6a990-500b-4&from=paste&height=430&id=u0cd4fae4&originHeight=430&originWidth=702&originalType=binary&ratio=1&rotation=0&showTitle=false&size=75715&status=done&style=none&taskId=u4db66afb-71ce-4228-b8b1-2149214b465&title=&width=702)
<a name="SAgWM"></a>
## cluster簇
跟关节差不多，一般不用簇，簇跟关节一样都是影响对应的顶点。
<a name="qFU0f"></a>
## deltaMush
deltaMush的作用： 一个模型应用deltaMush后，移动模型的顶点时，变形器会自动平滑模型来使模型布线均匀。<br />注意：是应用deltaMush后再移动顶点。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674099425473-7e3080cb-8a93-47e5-93c9-b319f0a8dede.png#averageHue=%236f80a1&clientId=u0af6a990-500b-4&from=paste&height=669&id=u4df0011f&originHeight=669&originWidth=844&originalType=binary&ratio=1&rotation=0&showTitle=false&size=380832&status=done&style=none&taskId=ud8d73674-d894-4249-b036-321e80efbe5&title=&width=844)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674099145812-75f8fe76-7175-45de-a154-2d3b1787fb00.png#averageHue=%2353524f&clientId=u0af6a990-500b-4&from=paste&height=284&id=uba80905e&originHeight=284&originWidth=400&originalType=binary&ratio=1&rotation=0&showTitle=false&size=64997&status=done&style=none&taskId=ud3c03d7b-54a3-4e3d-a7c0-9fcbbd59d32&title=&width=400)<br />参数介绍： <br />envelope是总的影响程度设置<br />distance weight 为0时不会考虑模型的布线，会平滑所有模型曲线。如果值为1时，那么会自动判断模型的布线，平滑时不会影响模型中离得很近的线(那些用来卡线的线)。<br />displacement 为1时平滑时会考虑模型的细节，为0时不会考虑模型的细节。
<a name="QOEjE"></a>
## lattice晶格变形器
选择一个物体创建晶格变形器，会生成两个新节点：ffd1Lattice与ffd1Base。然后物体会根据ffd1Lattice与ffd1Base进行插值来产生形变
<a name="Pqx7x"></a>
## Wrap包裹变形器
先选择被驱动物体，再选择驱动物体。<br />然后就像晶格变形器一样在驱动物体会产生一个base物体，然后被驱动物体会根据驱动物体与base物体之间进行插值来产生形变。<br />包裹变形器运行很慢，尽量不用。
<a name="R12ZK"></a>
## shrinkWrap
先选择被驱动物体，再选择驱动物体<br />应用这个变形器后，被驱动物体的顶点会根据不同的映射方式依附到驱动物体的顶点上面去。<br />映射方式介绍：<br />面片为被驱动物体，球为驱动物体<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674105821630-561e5323-d8df-4b85-b4fd-ee0cb7b07ee2.png#averageHue=%23434342&clientId=u0af6a990-500b-4&from=paste&height=241&id=u01fbd000&originHeight=241&originWidth=524&originalType=binary&ratio=1&rotation=0&showTitle=false&size=58598&status=done&style=none&taskId=u749ca5fe-7de2-4c7e-934a-0014043ff7f&title=&width=524)<br /> Toward lnner object：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674105844158-564af453-1fe6-46ea-9079-459bffa2e810.png#averageHue=%23647381&clientId=u0af6a990-500b-4&from=paste&height=180&id=ub8f35d77&originHeight=952&originWidth=1586&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1054024&status=done&style=none&taskId=u42f8420a-842c-48f7-8040-7e3a364133b&title=&width=300)![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674105856727-601b6ee7-e2f8-4af0-b003-3c682ce607dd.png#averageHue=%23648183&clientId=u0af6a990-500b-4&from=paste&height=178&id=u81ae0845&originHeight=490&originWidth=692&originalType=binary&ratio=1&rotation=0&showTitle=false&size=302332&status=done&style=none&taskId=u52459b8e-55e4-44f2-afea-69d11429554&title=&width=251)<br />Vertex normals:<br />被驱动物体与驱动物体的接触的顶点会产生依附效果<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674106015351-e34399f0-ed98-4d22-bece-fa38520bed28.png#averageHue=%236a817f&clientId=u0af6a990-500b-4&from=paste&height=214&id=u2a8f8a2f&originHeight=891&originWidth=1421&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1194143&status=done&style=none&taskId=u538817d5-47e4-40aa-a270-644f1986ff7&title=&width=341) ![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674106104759-3eb44e86-c529-4ac9-b7f0-a716a7b70dd0.png#averageHue=%237f8d81&clientId=u0af6a990-500b-4&from=paste&height=172&id=uf48d2b49&originHeight=727&originWidth=1291&originalType=binary&ratio=1&rotation=0&showTitle=false&size=660663&status=done&style=none&taskId=u93078f12-c454-4d55-b216-4c4787ba59e&title=&width=306)
<a name="yD86A"></a>
## Wire线变形器
使用步骤：<br />选择模型按回车，再选择曲线按回车<br />然后就可以通过曲线来驱动模型使模型产生形变<br />一些属性的介绍:<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674106695740-58de65e6-8aa5-4be0-b37f-67673d251c50.png#averageHue=%23414141&clientId=u0af6a990-500b-4&from=paste&height=242&id=u90b0566c&originHeight=242&originWidth=582&originalType=binary&ratio=1&rotation=0&showTitle=false&size=53040&status=done&style=none&taskId=u3655e9cf-cc07-4bf7-aa65-4cb8c123cab&title=&width=582)<br />Rotation: 产生形变时对模型旋转属性影响的权重<br />Dropoff distance： 曲线点寻找最近的顶点的距离范围<br />变形器是可以刷权重的<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674107272387-47291f7f-a956-4cdf-bc4b-2b923336abc2.png#averageHue=%235e605a&clientId=u0af6a990-500b-4&from=paste&height=1148&id=ub2d6705d&originHeight=1148&originWidth=417&originalType=binary&ratio=1&rotation=0&showTitle=false&size=263266&status=done&style=none&taskId=ubefac0cd-ae31-4c5e-9f50-fcb5b6eb6f8&title=&width=417)
<a name="v54zy"></a>
## Nonlinear非线性变形器
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674107436732-c044c177-673f-4a4f-82a3-aedae7925efd.png#averageHue=%23585956&clientId=u0af6a990-500b-4&from=paste&height=213&id=u55dcd8b8&originHeight=213&originWidth=529&originalType=binary&ratio=1&rotation=0&showTitle=false&size=65312&status=done&style=none&taskId=u5693f4ad-851f-4577-b92a-72cf3b5cfd0&title=&width=529)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674107864601-3ebdd4ef-ca5e-447b-ae35-4fc6ecbbde2d.png#averageHue=%235e6d80&clientId=u0af6a990-500b-4&from=paste&height=629&id=u25284a14&originHeight=629&originWidth=1093&originalType=binary&ratio=1&rotation=0&showTitle=false&size=191598&status=done&style=none&taskId=u69a9992e-f21b-432e-a5c3-318be7e3542&title=&width=1093)
<a name="MymSj"></a>
## sculpt雕刻变形器
选择一个模型就可以使用这个雕刻变形器了。没啥用这个变形器，他能做的shrinkWrap也能做并且更方便。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674108375883-b4128dd2-7ebf-4636-86ca-8bc5f10c41ba.png#averageHue=%23596987&clientId=u0af6a990-500b-4&from=paste&height=563&id=u70f38e32&originHeight=563&originWidth=712&originalType=binary&ratio=1&rotation=0&showTitle=false&size=450905&status=done&style=none&taskId=u019d6c5e-8db2-496b-8b70-78d08a9f3bf&title=&width=712)
<a name="FDn1j"></a>
# deformation_order
如果一个模型只受一个变形器控制都很好理解，但是如果受到多个变形器控制的话就会根据变形器的顺序不同而导致不同的结果，因此要理清变形器的顺序是很重要的。<br />这里介绍两个更改变形器执行的顺序的方法：<br />第一种：<br />选择好模型然后查看其所有的输入属性，然后通过鼠标中键拖拽即可改变变形器执行的顺序<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674112832754-5fb47a6d-38f3-4525-929c-f8bb19314217.png#averageHue=%23535451&clientId=u0af6a990-500b-4&from=paste&height=264&id=u72763447&originHeight=264&originWidth=382&originalType=binary&ratio=1&rotation=0&showTitle=false&size=66502&status=done&style=none&taskId=uaa04c244-170b-403a-88b2-495c2f134db&title=&width=382)<br />第二种：deformation order<br />更改对应变形器的deformation order<br />automatic是让maya自己判断设置变形器的执行顺序，pre-deformation是将变形器设置成最先执行，post-deformation是将变形器设置成最后执行。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1674112912258-bb05c6fb-40cb-4529-acf5-4e5b5d8bacbc.png#averageHue=%23535353&clientId=u0af6a990-500b-4&from=paste&height=453&id=uf6af1e1e&originHeight=453&originWidth=711&originalType=binary&ratio=1&rotation=0&showTitle=false&size=72269&status=done&style=none&taskId=u181af5f8-b802-4a8d-a600-42d6fd9f519&title=&width=711)
<a name="jEW6m"></a>
# 快速转化低模
首先通过自带的reduce功能减面，删除历史，使用deltaMush变形器并调整参数使布线变得均匀，删除历史，选择低模后选择高模使用shrinkWrap变形器并调整参数来保留高模的模型细节，删除历史。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1675221119348-35b72450-d2fc-4b8d-87f9-d0fe64a1195b.png#averageHue=%235b5a59&clientId=u7fb7aa6f-4485-4&from=paste&height=603&id=u41f81f5a&originHeight=603&originWidth=470&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42211&status=done&style=none&taskId=u0ebf8a5c-d834-4d3d-bea8-e192be2b143&title=&width=470)![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1675221693200-dc2aedc3-c7d3-481c-a7f6-3328c41870a9.png#averageHue=%23464745&clientId=u7fb7aa6f-4485-4&from=paste&height=273&id=u1a530abf&originHeight=273&originWidth=389&originalType=binary&ratio=1&rotation=0&showTitle=false&size=62102&status=done&style=none&taskId=u4536fd8b-bc76-4175-8110-346cad89b24&title=&width=389)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1675221640088-83ebb73b-f320-48e8-a014-4adfe704c730.png#averageHue=%23595855&clientId=u7fb7aa6f-4485-4&from=paste&height=404&id=u1d6c89c9&originHeight=404&originWidth=360&originalType=binary&ratio=1&rotation=0&showTitle=false&size=102413&status=done&style=none&taskId=u0be85a61-a4df-4af9-8d7b-2bf4ec41c85&title=&width=360)


