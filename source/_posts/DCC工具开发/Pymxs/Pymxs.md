---
title: Pymxs
tags: Pymxs
categories: DCC工具开发
abbrlink: 86e35ccb
date: 2024-03-21 00:52:00
---
# 官方文档
https://help.autodesk.com/view/MAXDEV/2024/ENU/?guid=MAXDEV_Python_executing_python_html
# 如何使用3dsmax自带的图标
参考Loading Multi-resolution Icons:https://help.autodesk.com/view/MAXDEV/2024/ENU/?guid=MAXDEV_Python_creating_python_uis_html
3dsmax自带的图标指南:https://help.autodesk.com/view/MAXDEV/2024/ENU/?guid=Max_Developer_Help_icon_guide_icon_resource_guide_html
核心代码:
```python
from qtmax import LoadMaxMultiResIcon
toolBtn1 = QToolButton()
toolBtn1.setIcon(LoadMaxMultiResIcon("Common/Lock"))
```
# 官方提供的pymxs与pyside2的实例代码
路径:C:\Program Files\Autodesk\3ds Max 2024\scripts\PythonSamples\Python3\
