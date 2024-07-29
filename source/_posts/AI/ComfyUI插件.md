---
title: ComfyUI插件
tags: ComfyUI
categories: AI
abbrlink: ed23b055
date: 2023-11-28 09:31:00
---
# 工作流参考
https://comfyanonymous.github.io/ComfyUI_examples/

# 将工作流保存到png图像中
方法一:
1. 下载插件https://github.com/pythongosssss/ComfyUI-Custom-Scripts
2. 生成图片后,界面中会显示生成的图片的队列,将队列中的图片保存即可
方法二:
代码:
```python
#@title Add Workflow to PNG


from PIL import Image, PngImagePlugin
import os

def make_workflow_png(image_path, workflow_path):
    if not os.path.exists(image_path):
        ValueError(f"Invalid image path `{image_path}`")
    if not os.path.exists(workflow_path):
        ValueError(f"Invalid workflow path `{workflow_path}`")
    path = os.path.dirname(image_path)
    filename = os.path.basename(image_path).rsplit('.', 1)[0]
    try:
        with open(workflow_path, "r") as file:
            data = file.read()
    except OSError as e:
        Exception("There was an error reading the workflow JSON:", e)
    image = Image.open(image_path)
    info = PngImagePlugin.PngInfo()
    info.add_text("workflow", data)
    new_path = os.path.join(path, filename+'_workflow.png')
    image.save(new_path, "PNG", pnginfo=info)
    return new_path

# Create the workflow PNG

image = '/content/Comparison_Workflow.png' # 在这里填写工作流生成的图片的路径
workflow = '/content/PPF_Workflow.json' # 在这里填写工作流的Json文件路径

workflow_png_path = make_workflow_png(image, workflow)

img = Image.open(image)

print("Workflow added to image:", workflow_png_path)
```
使用方法:
1. 准备ComfyUI的工作流文件:workflow.json (名字任意)
2. 工作流生成的图片:image.png  (名字任意)
3. 在提供的代码中填写图片和工作流的文件路径
4. 运行代码
5. 在图片的路径下得到后缀为_workflow.png的携带工作流的图片
6. 将携带工作流的图片拖入到ComfyUI中即可生成对应的工作流

# ComfyUI Manager
网站:https://github.com/ltdrdata/ComfyUI-Manager
作用:方便插件的安装,识别工作流中有哪些未安装的模型和插件
推荐的设置:
![Alt text](image-4.png)
设置好这些以后,comfyui上能够显示节点对应的插件名,如果是🦊图标就是原生的,如果是不带🦊图标并且没有插件名的就是识别不出来的.
![Alt text](image-5.png)

# AnimateDiff Evolved(生成动画的工作流相关)
网站:https://github.com/Kosinkadink/ComfyUI-AnimateDiff-Evolved
额外需要的模型:参考github说明,有lora,有model.
作用:生成带动作的视频
![Alt text](image-2.png)

# FizzNodes(生成动画的工作流相关)
网站:https://github.com/FizzleDorf/ComfyUI_FizzNodes
![Alt text](image-3.png)
作用:
> Scheduled prompts, scheduled float/int values and wave function nodes for animations and utility. compatable with framesync and keyframe-string-generator for audio synced animations in Comfyui.
用于动画和实用程序的预定提示、预定浮点/整数值和波函数节点。与 Comfyui 中的音频同步动画的帧同步和关键帧字符串生成器兼容。

# ComfyUI-VideoHelperSuite(生成动画的工作流相关)
网站:https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite
![Alt text](image.png)
作用:视频工作流相关节点

# ComfyUI_Custom_Nodes_AlekPet(实时绘画的工作流相关)
网站:https://github.com/AlekPet/ComfyUI_Custom_Nodes_AlekPet


# ComfyUI_IPAdapter_plus
网站:https://github.com/cubiq/ComfyUI_IPAdapter_plus
注意:<font color=red>这个需要下载对应的需要模型,因此需要前往github查看需要的内容</font>
作用:
> 	The IPAdapter are very powerful models for image-to-image conditioning. Given a reference image you can do variations augmented by text prompt, controlnets and masks. Think of it as a 1-image lora.
IPAdapter 是非常强大的图像到图像调节模型。给定参考图像，您可以通过文本提示、控制网和遮罩进行增强的变化。将其视为单幅图像 lora。

# ComfyUI-Custom-Scripts
网站:https://github.com/pythongosssss/ComfyUI-Custom-Scripts
作用举例:可以扩展comfyUI的界面,令生成的图片都显示在界面上,然后可以拖拽复现工作流.
像这种带蟒蛇图标的都属于这个插件
![Alt text](image-1.png)

# comfyui_controlnet_aux
网站:https://github.com/Fannovel16/comfyui_controlnet_aux
注意:<font color=red>此自定义节点与comfyui_controlnet_preprocessors相冲突</font>
作用:可以将图片进行预处理,生成ControlNet模型需要的图片.

# Masquerade Nodes
网站:https://github.com/BadCafeCode/masquerade-nodes-comfyui
作用: 提供了很多与mask处理有关的节点

# Allor
网站:https://github.com/Nourepide/ComfyUI-Allor?tab=readme-ov-file
作用: 提供了很多调节图像的节点
使用文档:https://nourepide.github.io/ComfyUI-Allor-Doc/image-text.html
## ImageTransformCropAbsolute
可以将图片进行裁切
![Alt text](image-7.png)

# ComfyUI Segment Anything
网站:https://github.com/storyicon/comfyui_segment_anything
作用: 通过算法进行生成遮罩与图像

# efficiency-nodes-comfyui
网站:https://github.com/LucianoCirino/efficiency-nodes-comfyui?tab=readme-ov-file
作用:提供了一些自定义节点,例如xyplot.然后提供了一些用于简化工作流程而减少节点总数的节点,将一些流程汇总到了一个节点上面.

# ComfyUI_tinyterraNodes
网站:https://github.com/TinyTerra/ComfyUI_tinyterraNodes
作用:这个也有xyplot,也提供了一些精简工作流的节点.
实测:通过自定义节点实现只需要一个节点就能够添加多个lora的效果.并实测跟原生工作流生成图片相同.
将此图片拖入comfyui复刻工作流
![Alt text](comfyui_ttn.png)

# ComfyUI_ADV_CLIP_emb
网站:https://github.com/BlenderNeko/ComfyUI_ADV_CLIP_emb
作用:让comfyui的提示词的跟webui的提示词对于权重分配的方式一样.
## BNK_CLIPTextEncodeAdvanced
![Alt text](image-6.png)


# ComfyUI-Inspire-Pack
网站:https://github.com/ltdrdata/ComfyUI-Inspire-Pack
作用:这也有A1111 兼容性支持有助于在 ComfyUI 中精确复制 A1111 的创建。
## KSampler //Inspire
![Alt text](image-8.png)

# ComfyUI_Dave_CustomNode(manage中搜索Davemane42)
网站:https://github.com/Davemane42/ComfyUI_Dave_CustomNode
作用:线稿上色latent couple(sdwebui上面叫latent couple),注:这个不能够通过api进行调用


# ComfyUI-Impact-Pack
网站:https://github.com/ltdrdata/ComfyUI-Impact-Pack
作用:脸部修复

# was-node-suite-comfyui(manage中搜索WAS_Node_Suite)
网站:https://github.com/WASasquatch/was-node-suite-comfyui
作用:提供了很多不同类型的节点,个人主要用到的:各种switch节点.方便一个工作流来实现不同需求.
