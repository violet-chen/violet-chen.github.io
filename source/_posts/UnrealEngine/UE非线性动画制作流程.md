---
title: UE非线性动画制作流程
tags: UnrealEngine
categories: UnrealEngine
abbrlink: c5cbedfb
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

<a name="HBLu7"></a>
# 推荐链接
[Technical Guide to Linear Content Creation | Learning path](https://dev.epicgames.com/community/learning/paths/YJ/technical-guide-to-linear-content-creation)<br />[https://cdn2.unrealengine.com/animation-field-guide-v1-2-8-zhcn-d338b3986f3f.pdf](https://cdn2.unrealengine.com/animation-field-guide-v1-2-8-zhcn-d338b3986f3f.pdf)<br />[https://cdn2.unrealengine.com/Unreal+Engine%2FEGC%2F%28CHS%29Fortnite-Trailer-Developing-a-real-time-pipeline-for-a-faster-workflow-dc2016593b1a879342feb037c7a0f6162dea4867.pdf](https://cdn2.unrealengine.com/Unreal+Engine%2FEGC%2F%28CHS%29Fortnite-Trailer-Developing-a-real-time-pipeline-for-a-faster-workflow-dc2016593b1a879342feb037c7a0f6162dea4867.pdf)<br />[https://www.unrealengine.com/zh-CN/animation-field-guide ](https://www.unrealengine.com/zh-CN/animation-field-guide )
<a name="j1eFb"></a>
# UE非线性动画制作流程的概念和价值
<a name="tuNFU"></a>
## 流程创建
目标：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686023326482-3fdb94e5-a193-484f-a2a3-79dd59c24454.png#averageHue=%23f7f6f5&clientId=u0e4b6326-6d4a-4&from=paste&height=334&id=u11bbecfc&originHeight=334&originWidth=702&originalType=binary&ratio=1&rotation=0&showTitle=false&size=179870&status=done&style=none&taskId=u7fc42403-541a-4847-be93-f08224b49e6&title=&width=702)<br />任务：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686023363068-5d75e24a-6b6e-4a08-8ba9-bd9d11574330.png#averageHue=%23f9f8f5&clientId=u0e4b6326-6d4a-4&from=paste&height=770&id=u518a49c8&originHeight=770&originWidth=685&originalType=binary&ratio=1&rotation=0&showTitle=false&size=273331&status=done&style=none&taskId=uc543a736-1a12-4110-9007-708bbdff3fe&title=&width=685)

<a name="ROYHi"></a>
## 实时流程和线性渲染流程的差异与讲解
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686027945944-7ba4f098-ee75-4e32-8a80-7de6b7086b80.png#averageHue=%23a8a5a2&clientId=u0e4b6326-6d4a-4&from=paste&height=1027&id=BRDBw&originHeight=1027&originWidth=1497&originalType=binary&ratio=1&rotation=0&showTitle=false&size=627080&status=done&style=none&taskId=uf969346f-39ec-4235-80fe-481c383f057&title=&width=1497)
<a name="vJlEk"></a>
### 制作工具的差异
在线性流程中很多项目的岗位间习惯通过类似贴图alembic fbx等中间数据进行衔接，因此可以不存在整个项目的中心工具，甚至可以允许每个岗位根据自己的喜好选择dcc工具来制作中间数据，最终以镜头为单位将序列帧素材在后期软件中进行组装。<br />而在实时渲染流程中并不是指资产制作也必须都在ue中完成，而是强调以ue为中心，平台将通过其他dcc软件制作的资产在ue中进行整合。同时各岗位围绕ue进行工作，最终通过ue直接输出成片。
<a name="agQF3"></a>
### 工作流的差异
工作流的差异主要在于不同环节的工作并行度，由于在实时流程中各岗位都能通过ue协作，镜头设计，拆分，资产整合，场景制作，渲染输出都在ue中完成，同时借助版本管理软件来保障资产管理和协作，因此才能实现不同岗位，不同环节在同一个中心制作平台上的平行工作。要强调一下的是，这里的平行工作并不是指多个岗位可以同时制作同一个环节的不同工作，比如分别制作多个模型资产，这在线性流程中也能够轻松实现。而是指原本需要相互等待的镜头设计，场景搭建，资产制作等环节在统一的项目工程，统一的技术标准，统一的ue数据格式进行衔接的基础上同时开展分别迭代实时预览，最大程度地降低环节之间的等待时间。
<a name="qrzaJ"></a>
### 数据组织管理
表格中所指的数据组织管理的实时流程的中心化相对于线性流程的分散，指的就是将各类dcc制作的资产通过ue这个中心技术平台以一个完整工程的形式进行整合和协作。同时这里的中心化从技术上并不是指所有岗位都同时操作一个项目的股本，而是在各自本地的项目副本中进行工作然后通过版本管理软件根据服务器上的权威版本进行同步等管理。允许客户端只在必要时访问服务器，既保证了工程的统一，又保留了各自工作的灵活度。
<a name="kEJ69"></a>
### 命名规则
这里的严格和自由是相对的，比如常用的文件名前后缀关键词在实时流程中应该也是有明确要求的，只是在例如文件保存时间，版本号等信息保存方面在不少线性流程项目中，依然习惯于通过文件名体现。而在实时流程项目中更多的是通过版本管理软件来自动记录，文件名可以只保留核心信息，相对自由。
<a name="CdEF7"></a>
### 版本资源控制
线性流程项目趋向于手动管理，当然目前也有不少业务管理软件可以实现例如自动修改文件名等自动化功能。<br />在实时流程中整个工程通常要通过版本控制软件自动管理更新迭代。
<a name="LySR8"></a>
### 输出形式
线性流程习惯于输出分层通道序列图然后到后期软件中进行合成<br />实时流程最推荐的方式是在游戏中直接输出最终画面，对于一些具有特殊要求的项目，ue也支持通过movie rq插件输出分层图片mrq插件输出分层图片，具体细节查看![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686029460215-911bcbb1-e651-41f2-9bb3-d2b16f6835c5.png#averageHue=%23d8caaa&clientId=u0e4b6326-6d4a-4&from=paste&height=344&id=u8085ab69&originHeight=344&originWidth=340&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86728&status=done&style=none&taskId=u17016de5-3736-494f-8a09-6bc227a4347&title=&width=340)
<a name="SqGKx"></a>
### 资源要求
线性流程通常允许直接使用最高精度的模型贴图资产。<br />实时流程中需要对资产进行适度优化，在UE5中，由于新增了nanite，虚拟纹理等技术，对影视及美术资产的兼容性正在不断提高。具体技术细节回顾![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686029603666-d4f2420d-197d-4cb9-a5aa-32db788c5ac0.png#averageHue=%23bbb49f&clientId=u0e4b6326-6d4a-4&from=paste&height=313&id=u8d388357&originHeight=313&originWidth=326&originalType=binary&ratio=1&rotation=0&showTitle=false&size=88341&status=done&style=none&taskId=u8e697751-200b-4561-9f20-aaa6e242d34&title=&width=326)
<a name="t0oRJ"></a>
### 流程介绍
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686029721842-d9053b3b-6c01-4700-beff-28efdcb11dd3.png#averageHue=%23f0f0f0&clientId=u0e4b6326-6d4a-4&from=paste&height=1352&id=u34c04e8f&originHeight=1352&originWidth=1482&originalType=binary&ratio=1&rotation=0&showTitle=false&size=298293&status=done&style=none&taskId=ue85b18e3-8d0b-4a2f-94c2-b64d7b4c7e9&title=&width=1482)虽然线性流程和实时流程在最终都需要渲染输出影片，但两者在整个项目周期中的渲染时机有很大不同。<br />在线性流程中建模绑定动画模拟场景编辑后期等多个工作阶段，审核人员通常不会直接获取并打开dcc工作文件。而是要求各岗位将当前的工作进度以图像或视频的形式进行输出，并根据视觉进行审核和反馈。因此在整个项目生命周期中需要非常频繁地进行渲染输出，某些阶段输出速度较快，而某些阶段消耗的时间较多，累积后的整体时间成本相当可观，并且频繁的渲染等待时间会打断创作和制作的持续性，带来后续的很多回忆相关的工作。在实时渲染非线性流程中由于除最终画面以外的各阶段的最终结果都是以实时渲染方式呈现，因此可以理解为每时每刻都在渲染输出，因此审查人员可以针对开发岗位当前编辑器中的实际画面通过截屏录屏甚至是像素流的方式实时审核反馈，整个过程快速连续，只在生成最终版本视频阶段，为了最大化画面细节，才需要渲染输出。
<a name="zMHcB"></a>
### 工作流的并行程度差异
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686030176165-d89c960c-7b9e-4be9-a5e0-7785d7c991c6.png#averageHue=%23030303&clientId=u0e4b6326-6d4a-4&from=paste&height=1333&id=ube87d9f9&originHeight=1333&originWidth=2569&originalType=binary&ratio=1&rotation=0&showTitle=false&size=546609&status=done&style=none&taskId=u6389ac2e-58b4-45bf-9330-d35ca754966&title=&width=2569)线性流程中各阶段工作通常依赖上一阶段的成果需要在上一阶段成果审查通过后才能够执行。<br />在实时流程中多岗位工作是可以并行推进的，各阶段有各自的审查标准，在特定阶段才会审查各类工作成果整合后的最终效果。<br />这项差异本质上来自于两个方面，一个是数据的统一性，二是成果审查方式。<br />线性流程中各岗位之间是通过中间格式文件来交换数据的，各自使用的dcc源文件并不衔接，整个项目也通常是以镜头为单位进行拆分，而不是以统一的工程形式进行中心化管理，这样导致整个项目在多个阶段的数据都是通过中间文件塌陷过的，并不统一连续。这就导致下一个工序对上一个工序的结果中间文件产生了很强的依赖，无法基于工作文件同步推进。一旦某个阶段的工作成果需要修改，那么之后的所有岗位必然也会增加相应的修改工作量。<br />实时流程中各岗位围绕统一的中心化的工程进行协作，每个岗位之间的工作都是通过引用关系，和其他岗位进行自动整合。并且由于实时渲染的特性，整合后的当前最终结果都是可以在ue中实时预览到的，并不需要再进行输出，因此客观上省略了中间文件的衔接工作。各岗位的工作数据都是在统一连续的状态下持续推进的。<br />至于审查方式：<br />在线性流程中由于通常以各阶段的像素结果为审查对象忽略中间过程同样不影响审查，导致的结果就是每个阶段通过将成果塌陷成中间文件的方式来确保数据的确定性，也就导致了对上一个岗位工作结果的依赖。<br />而在实时流程中各岗位围绕同一个工程进行协作，很多过程中产生的问题会直观反映在实时渲染的结果中无法忽略，因此审查的对象就不再只是最终呈现出的像素，而是中间数据也要正确。例如pbr材质框架中的关键参数，角色的绑定方式，镜头动画数据等大量数据都会实时互相产生影响。客观上增加了可能出现的问题种类提高了审查要求。但这种通过中间过程及时定位问题的审查方式确保了各岗位间可以并行工作，快速暴露问题快速定位和解决问题。<br />此外基于ue的实时流程可以活用很多编辑器自带工具或编写脚本工具来辅助进行数据审查，可以大大提升审查效率。
<a name="zstwH"></a>
### 岗位管理模式差异
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686030683745-50473c86-1efb-4812-bcae-b2797de9af35.png#averageHue=%23040404&clientId=u0e4b6326-6d4a-4&from=paste&height=1336&id=u1098419e&originHeight=1336&originWidth=2377&originalType=binary&ratio=1&rotation=0&showTitle=false&size=599850&status=done&style=none&taskId=u126bfd8c-047a-4b5b-ae2c-562f0a31eb8&title=&width=2377)
<a name="ZIEH0"></a>
### 分层输出的差异
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686030857772-cb61bf20-8279-447e-ada4-9188254aaad0.png#averageHue=%23ebebeb&clientId=u0e4b6326-6d4a-4&from=paste&height=634&id=u29d82236&originHeight=634&originWidth=625&originalType=binary&ratio=1&rotation=0&showTitle=false&size=100624&status=done&style=none&taskId=ubb2c0a7d-03b2-4382-a0dc-eab126b46a3&title=&width=625)
<a name="IbEVc"></a>
## 流程举例与展开讲解
比较旧了，现在ue5加入了模型编辑模式和control rig，当前我们可以在ue编辑器中完成的工作其实比这张图中描述的还要多<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686031115260-8428d81c-5e3d-446e-afeb-075ee9ade2d5.png#averageHue=%23f9f9f8&clientId=u0e4b6326-6d4a-4&from=paste&height=1164&id=ue58ff07e&originHeight=1164&originWidth=1263&originalType=binary&ratio=1&rotation=0&showTitle=false&size=173330&status=done&style=none&taskId=u8cbea1c8-0025-4b72-99e7-75609653b96&title=&width=1263)
<a name="rRxV6"></a>
### 故事和布局设计
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686031513044-fee26b96-9902-42d1-a681-0dedfaf43a5b.png#averageHue=%231d1c1b&clientId=u0e4b6326-6d4a-4&from=paste&height=917&id=u4324ce09&originHeight=917&originWidth=1588&originalType=binary&ratio=1&rotation=0&showTitle=false&size=427986&status=done&style=none&taskId=u100900a8-51c5-485b-a627-30dd39d2d9e&title=&width=1588)<br />首先是2d故事版创作阶段,这个过程和线性流程一致,通过手绘的方式创作故事版图片,具象化描述故事情节和场景气氛并导入视频编辑软件生成故事样片。然后根据2d故事版，在UE的sequence工具中拆分镜头，幕，节拍，并且在拆分好的sequence中直接创作粗略的3d分镜，而不是先在玛雅等dcc软件中创作分镜以后再把镜头动画导入到ue。这一步看似只是分镜创作时使用的工具不同，但其实决定了整个项目的整合方式，通过ue制作粗略分镜的方式可以让所有镜头在第一时间呈现出大致的面貌。中间的资产引用，镜头组织结构等信息都已经明确。而不是先分镜头在dcc中分别制作，然后再进行整合。这个阶段得到的分镜后续肯定会不断修改，但由于相关信息已经统一整合到一个工程中，并且通过实时渲染的方式直观呈现出来，未来的修改可以用很高的效率围绕sequence进行。关于sequence作为ui动画制作核心的内容![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686031708093-838dfc81-b7ab-41b1-bd2d-91bfc7e2ac7a.png#averageHue=%23bab18a&clientId=u0e4b6326-6d4a-4&from=paste&height=222&id=u922c7588&originHeight=222&originWidth=229&originalType=binary&ratio=1&rotation=0&showTitle=false&size=47138&status=done&style=none&taskId=u67ff6b0e-55c6-45bd-9620-18a43d57948&title=&width=229)。
<a name="hTz6l"></a>
###   ![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686032010016-04663999-bd24-4459-bc31-5c799283c782.png#averageHue=%23e1dcd7&clientId=u0e4b6326-6d4a-4&from=paste&height=894&id=uce388cb8&originHeight=894&originWidth=1130&originalType=binary&ratio=1&rotation=0&showTitle=false&size=993806&status=done&style=none&taskId=ub04da3b4-1aa9-4ce5-bccb-c763935a1f3&title=&width=1130) 第一单位可视化预览
第一单位可视化预览阶段可以理解为角色动画实时3d分镜。首先根据剧情通过临时占位资产搭建大致的场景布局，比如地面建筑等。然后请动作捕捉演员根据粗略场景进行首次动作表演，演员可以根据剧本进行多次演出并通过sequence的镜头实拍功能进行组织，导演可以随时决定并切换使用哪个take（试拍），并在未来以此为基础进行评审，重新动捕或截取动作。<br />传统线性动画流程更倾向于将场景制作，3d镜头调整和角色动画分为明确的三个阶段<br />实时流程更倾向于在同一个场地，同一个时间根据最终效果实时调整场景，角色和镜头之间的关系，统一调度，并同时记录角色动画表演和相机镜头动画，这个过程和拍摄真人实景电影的逻辑很相似。不同之处在于实时流程不仅可以灵活调度角色镜头，甚至连场景也可以瞬间切换。
<a name="uf0QT"></a>
### sequence的组织形式
白皮书在这里也提到了sequence的具体组织形式，就是有一个完整的level sequence动画序列。包含了镜头动画序列，角色动画序列，这些序列又各自包含了不同版本的take（镜头试拍），随着动画创作的推进会持续增长，同时可以根据镜头进行剪辑。由于项目围绕ue实时渲染展开创作，每个阶段的成果和过程都会持续累积保留，随时可以查询或回溯，客观上确保了各岗位并行工作的可能，同时也对项目的统一管理提出了严格的要求。<br />为了方便管理和协作，项目将所有关卡通过UE子关卡工具分为场景子关卡，角色子关卡，镜头子关卡，灯光子关卡，蓝图子关卡，后期子关卡。其中分别包含各自的专用对象，然后一起包含在一个母关卡中，母关卡对应的是影视拍摄中的幕，通常可以是一个空关卡，然后根据需要添加相关的子关卡。这样做的明显的好处是例如场景设计师，动画设计师，灯光设计师等岗位可以同时打开同一个游戏工程针对同一个镜头分别编辑各自的子关卡而不会导致工作冲突，进一步保证了各岗位并行工作。在ue5 中由于引入了word partition，世界分区和level instance关卡实例等技术和工具使我们在组织关卡时拥有更多的方案实现子关卡方式难以实现的高效率和灵活度。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686033068346-e5430cbb-babc-4c72-8980-db5506f2f562.png#averageHue=%23847468&clientId=u0e4b6326-6d4a-4&from=paste&height=1017&id=ud444892c&originHeight=1017&originWidth=1274&originalType=binary&ratio=1&rotation=0&showTitle=false&size=126124&status=done&style=none&taskId=u40a24f6e-6b06-4664-b16f-dd2f917c611&title=&width=1274)<br />上图中的sequence指的都是关卡序列，资产轨迹指的是序列中的轨道，文件夹指的是sequence工具中用来管理轨道的文件夹。
<a name="sEogN"></a>
## 中期制作阶段
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686034164487-a8b29a9b-42f9-4e50-b0df-298822d50eff.png#averageHue=%23f5f4f3&clientId=u0e4b6326-6d4a-4&from=paste&height=706&id=u3dd0be29&originHeight=706&originWidth=1155&originalType=binary&ratio=1&rotation=0&showTitle=false&size=686222&status=done&style=none&taskId=u72908a4d-98c7-40a8-9ddb-0344d3ba486&title=&width=1155)<br />角色面部是通过alembic格式导出的<br />在dcc软件中需要在面次层级指定材质<br />并且在导出时需要勾选face set
<a name="awSEz"></a>
## 特效和后期
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686034632865-bf3683ce-a606-4972-ae1c-61d7ba2e95df.png#averageHue=%23dddcd8&clientId=u0e4b6326-6d4a-4&from=paste&height=861&id=u8c3b532a&originHeight=861&originWidth=985&originalType=binary&ratio=1&rotation=0&showTitle=false&size=674385&status=done&style=none&taskId=u29b2e2f1-6a26-4c2c-a4db-a8bf13f3908&title=&width=985)

<a name="OBvLc"></a>
## 

