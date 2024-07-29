---
title: pyside2 for maya
tags: PySide2
categories: PySide2
abbrlink: 10fbc54a
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

教程链接：[https://www.bilibili.com/video/BV1dJ41157gV?p=2&vd_source=b1de3fe38e887eb40fc55a5485724480](https://www.bilibili.com/video/BV1dJ41157gV?p=2&vd_source=b1de3fe38e887eb40fc55a5485724480)<br />购买链接：[https://zurbrigg.com/tutorials/pyside2-for-maya](https://zurbrigg.com/tutorials/pyside2-for-maya)
<a name="BKivW"></a>
# 创建一个新的界面的初始模板
```python
# coding:utf-8
import maya.cmds as cmds
import maya.mel as mel

try:
    from PySide2.QtWidgets import *
    from PySide2.QtCore import *
except:
    from PySide.QtGui import *
    from PySide.QtCore import *

try:
    from shiboken2 import wrapInstance
except ImportError:
    from shiboken import wrapInstance
from maya import OpenMayaUI as omui


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QWidget)


class TestDialog(QDialog):

    def __init__(self, parent=maya_main_window()):
        super(TestDialog, self).__init__(parent)
        
        self.setWindowTitle('MAYA-2018')
        self.setMinimumSize(300, 80)
        self.setWindowFlags(Qt.WindowType.Window)
        window_name = "WindowName"
        if cmds.window(window_name, exists=True):
            cmds.deleteUI(window_name, window=True)
        self.setObjectName(window_name)
        self.setStyleSheet("font: 12pt 'Arial';")

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        """ 控件 """
        pass

    def create_layouts(self):
        """ 布局 """
        pass

    def create_connections(self):
        """ 信号与槽的连接 """
        pass



def main():
    global aa
    app = qApp if QApplication.instance() else QApplication([])
    aa = TestDialog()
    aa.show()
    app.exec_()

```
<a name="PlgPe"></a>
# 创建对话框
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui


def maya_main_window():
    # 将maya主窗口的C++指针转换为python可以接受的对象。
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)

class TestDialog(QtWidgets.QDialog):

    def __init__(self, parent = maya_main_window()):
        super(TestDialog, self).__init__()

        self.setWindowTitle('one dialog')
        self.setMinimumSize(200,200)

        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)  # 将maya窗口的问号标志排除掉

if __name__ == '__main__':
    ui = TestDialog()
    ui.show()

```
<a name="noXJv"></a>
# 添加控件
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1660209348067-aab29e6c-8246-464d-8317-e7e652053ceb.png#averageHue=%235c5b5b&clientId=u766e0595-34d2-4&from=paste&height=239&id=Bz6mZ&originHeight=239&originWidth=216&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5305&status=done&style=none&taskId=ue78fdd29-f90b-4374-b166-ff10332b25f&title=&width=216)<br />教程中将控件和布局都分开放到函数里面了
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui


def maya_main_window():
    # 将maya主窗口的C++指针转换为python可以接受的对象。
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class TestDialog(QtWidgets.QDialog):

    def __init__(self, parent=maya_main_window()):
        super(TestDialog, self).__init__(parent)
		window_name = "my_window"
        if cmds.window(window_name, exists=True):
            cmds.deleteUI(window_name, window=True)
        self.setWindowTitle('Test Dialog')
        self.setMinimumSize(200, 200)
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)  # 将maya窗口的问号标志排除掉

        self.create_widgets()
        self.create_layouts()

    def create_widgets(self):
        self.lineEdit = QtWidgets.QLineEdit()
        self.checkBox1 = QtWidgets.QCheckBox("Checkbox1")
        self.checkBox2 = QtWidgets.QCheckBox("Checkbox2")
        self.button1 = QtWidgets.QPushButton("Button 1")
        self.button2 = QtWidgets.QPushButton("Button 2")

    def create_layouts(self):
        main_layout = QtWidgets.QVBoxLayout(self)  # 传递self将这个layout作为主layout
        main_layout.addWidget(self.lineEdit)
        main_layout.addWidget(self.checkBox1)
        main_layout.addWidget(self.checkBox2)
        main_layout.addWidget(self.button1)
        main_layout.addWidget(self.button2)


if __name__ == '__main__':
    ui = TestDialog()
    ui.show()

```

<a name="eu3dY"></a>
# layout基础
代码很优雅<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1660211434381-4c844e6c-e74b-4585-9562-d7ee77a631e2.png#averageHue=%23676767&clientId=u766e0595-34d2-4&from=paste&height=151&id=ub9a89202&originHeight=151&originWidth=216&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4631&status=done&style=none&taskId=ubdcf75eb-e84f-4704-9bf7-3258c9fc134&title=&width=216)
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui


def maya_main_window():
    # 将maya主窗口的C++指针转换为python可以接受的对象。
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class TestDialog(QtWidgets.QDialog):

    def __init__(self, parent=maya_main_window()):
        super(TestDialog, self).__init__(parent)

        self.setWindowTitle('Test Dialog')
        self.setMinimumWidth(200)
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)  # 将maya窗口的问号标志排除掉

        self.create_widgets()
        self.create_layouts()

    def create_widgets(self):
        self.lineEdit = QtWidgets.QLineEdit()
        self.checkBox1 = QtWidgets.QCheckBox()
        self.checkBox2 = QtWidgets.QCheckBox()
        self.ok_btn = QtWidgets.QPushButton("OK")
        self.cancel_btn = QtWidgets.QPushButton("Cancel")

    def create_layouts(self):
        form_layout = QtWidgets.QFormLayout()
        form_layout.addRow("Name:", self.lineEdit)
        form_layout.addRow("Hidden:", self.checkBox1)
        form_layout.addRow("Locked:", self.checkBox2)

        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.ok_btn)
        button_layout.addWidget(self.cancel_btn)

        main_layout = QtWidgets.QVBoxLayout(self)  # 传递self将这个layout作为主layout
        main_layout.addLayout(form_layout)
        main_layout.addLayout(button_layout)


if __name__ == '__main__':
    ui = TestDialog()
    ui.show()

```
<a name="pGV9c"></a>
# 删除对话框
```python
if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = TestDialog()
    ui.show()
```
<a name="rat7r"></a>
# 信号与槽
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui


def maya_main_window():
    # 将maya主窗口的C++指针转换为python可以接受的对象。
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class TestDialog(QtWidgets.QDialog):

    def __init__(self, parent=maya_main_window()):
        super(TestDialog, self).__init__(parent)

        self.setWindowTitle('Test Dialog')
        self.setMinimumWidth(200)
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)  # 将maya窗口的问号标志排除掉

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.lineEdit = QtWidgets.QLineEdit()
        self.checkBox1 = QtWidgets.QCheckBox()
        self.checkBox2 = QtWidgets.QCheckBox()
        self.ok_btn = QtWidgets.QPushButton("OK")
        self.cancel_btn = QtWidgets.QPushButton("Cancel")

    def create_layouts(self):
        form_layout = QtWidgets.QFormLayout()
        form_layout.addRow("Name:", self.lineEdit)
        form_layout.addRow("Hidden:", self.checkBox1)
        form_layout.addRow("Locked:", self.checkBox2)

        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.ok_btn)
        button_layout.addWidget(self.cancel_btn)

        main_layout = QtWidgets.QVBoxLayout(self)  # 传递self将这个layout作为主layout
        main_layout.addLayout(form_layout)
        main_layout.addLayout(button_layout)

    def create_connections(self):
        self.lineEdit.editingFinished.connect(self.print_hello_name)
        self.checkBox1.toggled.connect(self.print_is_hidden)
        self.cancel_btn.clicked.connect(self.close)  # self.close是自带的不需要自己写函数

    def print_hello_name(self):
        name = self.lineEdit.text()
        print("Hello {}!".format(name))

    def print_is_hidden(self):
        hidden = self.checkBox1.isChecked()
        if hidden:
            print("Hidden")
        else:
            print("Visible")



if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = TestDialog()
    ui.show()

```
<a name="bjO1K"></a>
## 过载信号
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1660271563886-f57ad54c-dc87-4574-ae27-6ebb78fec497.png#averageHue=%232a2c28&clientId=uc3617f6a-1057-4&from=paste&height=282&id=u7bd615cb&originHeight=282&originWidth=662&originalType=binary&ratio=1&rotation=0&showTitle=false&size=127516&status=done&style=none&taskId=uf32b9790-1ea2-48e6-99ca-1dd7ea32f28&title=&width=662)<br />通过@QtCore.Slot(int)和@QtCore.Slot(str)使信号传递的参数类型改变
<a name="mVcMe"></a>
## 自定义信号
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671169445449-5e7ff7c9-4408-440d-9fe3-f4f6c73d7d88.png#averageHue=%23707070&clientId=u0295db91-fe64-4&from=paste&height=136&id=u0c1e930c&originHeight=122&originWidth=202&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3205&status=done&style=none&taskId=u09cc59b7-0282-4952-b90f-600b0e45c40&title=&width=224.4444503901919)
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui


def maya_main_window():
    # 将maya主窗口的C++指针转换为python可以接受的对象。
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class MyLineEdit(QtWidgets.QLineEdit):
    enter_pressed = QtCore.Signal(str)  # 新建自定义信号

    def keyPressEvent(self, e):  # 使用QLineEdit自带的事件，当按键按下时触发并发送数据
        super(MyLineEdit, self).keyPressEvent(e)

        if e.key() == QtCore.Qt.Key_Enter:
            self.enter_pressed.emit("Enter Key Pressed")  # 信号触发时发送的字符串
        elif e.key() == QtCore.Qt.Key_Return:
            self.enter_pressed.emit("Enter Key Pressed")

class TestDialog(QtWidgets.QDialog):

    def __init__(self, parent=maya_main_window()):
        super(TestDialog, self).__init__(parent)

        self.setWindowTitle('Test Dialog')
        self.setMinimumWidth(200)
        self.setMinimumHeight(90)
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)  # 将maya窗口的问号标志排除掉

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.lineEdit = MyLineEdit()  # MyLineEdit 是自定义的继承QtWidgets.QLineEdit的类
        self.ok_btn = QtWidgets.QPushButton("OK")
        self.cancel_btn = QtWidgets.QPushButton("Cancel")

    def create_layouts(self):
        form_layout = QtWidgets.QFormLayout()
        form_layout.addRow("Name:", self.lineEdit)

        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.ok_btn)
        button_layout.addWidget(self.cancel_btn)

        main_layout = QtWidgets.QVBoxLayout(self)  # 传递self将这个layout作为主layout
        main_layout.addLayout(form_layout)
        main_layout.addLayout(button_layout)

    def create_connections(self):
        self.lineEdit.enter_pressed.connect(self.on_enter_pressed)
        self.cancel_btn.clicked.connect(self.close)  # self.close是自带的不需要自己写函数

    def on_enter_pressed(self, text):
        print(text)


if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = TestDialog()
    ui.show()

```
<a name="PJwXP"></a>
# 打开/导入/引用文件举例
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1660486774209-460c6550-a87b-416f-b824-5837e80e3c46.png#averageHue=%23626161&clientId=ud565464f-f3f4-4&from=paste&height=171&id=u578a9f29&originHeight=171&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7870&status=done&style=none&taskId=u1e460f4b-9d08-4527-b323-06e1b6f468d&title=&width=316)
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.OpenMaya as om
import maya.cmds as cmds


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class TestDialog(QtWidgets.QDialog):
    FILE_FILTERS = "Maya(*.ma *.mb);;Maya ASCII (*.ma);;Maya Binary (*.mb);;All Files (*.*)"  # 全部的过滤项

    selected_filter = "Maya (*.ma *.mb)"  # 记录选择的过滤项，每次更改过滤项的同时会更改这个全局变量的值

    def __init__(self, parent=maya_main_window()):
        super(TestDialog, self).__init__(parent)

        self.setWindowTitle('Open/Import/Reference')
        self.setMinimumSize(300, 80)
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.filepath_le = QtWidgets.QLineEdit()
        self.select_file_path_btn = QtWidgets.QPushButton()
        self.select_file_path_btn.setIcon(QtGui.QIcon(':fileOpen.png'))
        self.select_file_path_btn.setToolTip("select File")

        self.open_rb = QtWidgets.QRadioButton("Open")
        self.open_rb.setChecked(True)
        self.import_rb = QtWidgets.QRadioButton("Import")
        self.reference_rb = QtWidgets.QRadioButton("Reference")

        self.force_cb = QtWidgets.QCheckBox("Force")

        self.apply_btn = QtWidgets.QPushButton("Apply")
        self.close_btn = QtWidgets.QPushButton("Close")

    def create_layouts(self):
        file_path_layout = QtWidgets.QHBoxLayout()
        file_path_layout.addWidget(self.filepath_le)
        file_path_layout.addWidget(self.select_file_path_btn)

        radio_btn_layout = QtWidgets.QHBoxLayout()
        radio_btn_layout.addWidget(self.open_rb)
        radio_btn_layout.addWidget(self.import_rb)
        radio_btn_layout.addWidget(self.reference_rb)

        forme_layout = QtWidgets.QFormLayout()
        forme_layout.addRow("File", file_path_layout)
        forme_layout.addRow("", radio_btn_layout)
        forme_layout.addRow("", self.force_cb)

        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.apply_btn)
        button_layout.addWidget(self.close_btn)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.addLayout(forme_layout)
        main_layout.addLayout(button_layout)

    def create_connections(self):
        self.select_file_path_btn.clicked.connect(self.show_file_select_dialog)

        self.open_rb.toggled.connect(self.update_force_visibility)

        self.apply_btn.clicked.connect(self.load_file)
        self.close_btn.clicked.connect(self.close)

    def show_file_select_dialog(self):
        file_path, self.selected_filter = QtWidgets.QFileDialog.getOpenFileName(self, "Select File", "",
                                                                                self.FILE_FILTERS, self.selected_filter)
        if file_path:
            self.filepath_le.setText(file_path)

    def update_force_visibility(self, checked):
        self.force_cb.setVisible(checked)

    def load_file(self):
        file_path = self.filepath_le.text()
        if not file_path:
            return

        file_info = QtCore.QFileInfo(file_path)  # 得到文件的信息
        if not file_info.exists():  # 判断文件是否存在
            om.MGlobal.displayError("File does not exist: {}".format(file_path))
            return
        if self.open_rb.isChecked():
            self.open_file(file_path)
        if self.import_rb.isChecked():
            self.import_file(file_path)
        else:
            self.reference_file(file_path)

    def open_file(self, file_path):
        force = self.force_cb.isChecked()
        if not force and cmds.file(q=True, modified=True):
            result = QtWidgets.QMessageBox.question(self, "Modified", "Current scene has unsaved changes. Continue?")
            if result == QtWidgets.QMessageBox.StandardButton.Yes:
                force = True
            else:
                return
        cmds.file(file_path, open=True, ignoreVersion=True, force=force)

    def import_file(self, file_path):
        cmds.file(file_path, i=True, ignoreVersion=True)

    def reference_file(self, file_path):
        cmds.file(file_path, r=True, ignoreVersion=True)


if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = TestDialog()
    ui.show()

```
<a name="RbM6Q"></a>
# 将插件放入到工具架上
<a name="HzMTb"></a>
## 主要功能模块
首先这个是上一节使用的打开与导入对话框，区别是添加了show_dialog类方法来替代if name == '__main__'  。将这个py模块放到maya的script文件夹中后，然后通过另一组代码来调用类方法达到显示窗口的需求。好处是可以保存在窗口执行的操作，比如在文本框中输入了数据，关闭窗口再打开后数据依然保留。<br />然后新增加了两个函数show_event 和 close_event，这两个的作用是关闭窗口时记录窗口位置，打开窗口时设置窗口位置。
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.OpenMaya as om
import maya.cmds as cmds


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class OpenImportDialog(QtWidgets.QDialog):
    FILE_FILTERS = "Maya(*.ma *.mb);;Maya ASCII (*.ma);;Maya Binary (*.mb);;All Files (*.*)"  # 全部的过滤项

    selected_filter = "Maya (*.ma *.mb)"  # 记录选择的过滤项，每次更改过滤项的同时会更改这个全局变量的值

    dlg_instance = None

    @classmethod
    def show_dialog(cls):
        if not cls.dlg_instance:
            cls.dlg_instance = OpenImportDialog()  # 第一次使用函数会生成窗口实例给dlg_instance全局变量

        if cls.dlg_instance.isHidden():
            cls.dlg_instance.show()  # 如果窗口隐藏了就显示出来
        else:
            # 如果窗口还在屏幕中就激活窗口并顶端显示
            cls.dlg_instance.raise_()
            cls.dlg_instance.activateWindow()

    def __init__(self, parent=maya_main_window()):
        super(OpenImportDialog, self).__init__(parent)

        self.setWindowTitle('Open/Import/Reference')
        self.setMinimumSize(300, 80)
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)
        self.geometry = None
        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.filepath_le = QtWidgets.QLineEdit()
        self.select_file_path_btn = QtWidgets.QPushButton()
        self.select_file_path_btn.setIcon(QtGui.QIcon(':fileOpen.png'))
        self.select_file_path_btn.setToolTip("select File")

        self.open_rb = QtWidgets.QRadioButton("Open")
        self.open_rb.setChecked(True)
        self.import_rb = QtWidgets.QRadioButton("Import")
        self.reference_rb = QtWidgets.QRadioButton("Reference")

        self.force_cb = QtWidgets.QCheckBox("Force")

        self.apply_btn = QtWidgets.QPushButton("Apply")
        self.close_btn = QtWidgets.QPushButton("Close")

    def create_layouts(self):
        file_path_layout = QtWidgets.QHBoxLayout()
        file_path_layout.addWidget(self.filepath_le)
        file_path_layout.addWidget(self.select_file_path_btn)

        radio_btn_layout = QtWidgets.QHBoxLayout()
        radio_btn_layout.addWidget(self.open_rb)
        radio_btn_layout.addWidget(self.import_rb)
        radio_btn_layout.addWidget(self.reference_rb)

        forme_layout = QtWidgets.QFormLayout()
        forme_layout.addRow("File", file_path_layout)
        forme_layout.addRow("", radio_btn_layout)
        forme_layout.addRow("", self.force_cb)

        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.apply_btn)
        button_layout.addWidget(self.close_btn)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.addLayout(forme_layout)
        main_layout.addLayout(button_layout)

    def create_connections(self):
        self.select_file_path_btn.clicked.connect(self.show_file_select_dialog)

        self.open_rb.toggled.connect(self.update_force_visibility)

        self.apply_btn.clicked.connect(self.load_file)
        self.close_btn.clicked.connect(self.close)

    def show_file_select_dialog(self):
        file_path, self.selected_filter = QtWidgets.QFileDialog.getOpenFileName(self, "Select File", "",
                                                                                self.FILE_FILTERS, self.selected_filter)
        if file_path:
            self.filepath_le.setText(file_path)

    def update_force_visibility(self, checked):
        self.force_cb.setVisible(checked)

    def load_file(self):
        file_path = self.filepath_le.text()
        if not file_path:
            return

        file_info = QtCore.QFileInfo(file_path)  # 得到文件的信息
        if not file_info.exists():  # 判断文件是否存在
            om.MGlobal.displayError("File does not exist: {}".format(file_path))
            return
        if self.open_rb.isChecked():
            self.open_file(file_path)
        if self.import_rb.isChecked():
            self.import_file(file_path)
        else:
            self.reference_file(file_path)

    def open_file(self, file_path):
        force = self.force_cb.isChecked()
        if not force and cmds.file(q=True, modified=True):
            result = QtWidgets.QMessageBox.question(self, "Modified", "Current scene has unsaved changes. Continue?")
            if result == QtWidgets.QMessageBox.StandardButton.Yes:
                force = True
            else:
                return
        cmds.file(file_path, open=True, ignoreVersion=True, force=force)

    def import_file(self, file_path):
        cmds.file(file_path, i=True, ignoreVersion=True)

    def reference_file(self, file_path):
        cmds.file(file_path, r=True, ignoreVersion=True)
    
    def showEvent(self, e):
        super(OpenImportDialog, self).showEvent(e)

        if self.geometry:
            self.restoreGeometry(self.geometry)

    def closeEvent(self, e):
        super(OpenImportDialog, self).closeEvent(e)

        self.geometry = self.saveGeometry()


```
<a name="LGRqV"></a>
## 调用窗口显示的模块
open_import_dialog为模块名(py程序名)<br />OpenImportDialog为模块中的类名<br />注意：前两行是当py文件有更改时运行的，当没有更改py文件时不要运行。因为运行前两行会重置窗口的实例数。
```python
import open_import_dialog
reload(open_import_dialog)

from open_import_dialog import OpenImportDialog

OpenImportDialog.show_dialog()
```
<a name="FF1Ia"></a>
# 各种模式对话框
<a name="HWSLO"></a>
## 自定义对话框
这里有文件夹对话框，警告对话框，颜色选择对话框，自定义对话框<br />这里最主要学习的是自定义对话框<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671170114446-0a3d0bcd-baf4-42ee-aa68-4e09b5d92771.png#averageHue=%23655f5d&clientId=u0295db91-fe64-4&from=paste&height=594&id=ua0005fb4&originHeight=535&originWidth=1002&originalType=binary&ratio=1&rotation=0&showTitle=false&size=52403&status=done&style=none&taskId=u9f31be18-e0e4-4adf-8e57-a662337af7a&title=&width=1113.3333628265955)
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.OpenMaya as om
import maya.cmds as cmds


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class CustomDialog(QtWidgets.QDialog):

    def __init__(self, parent=maya_main_window()):
        super(CustomDialog, self).__init__(parent)

        self.setWindowTitle("Custom Dialog")
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.lineedit = QtWidgets.QLineEdit()
        self.ok_btn = QtWidgets.QPushButton('OK')

    def create_layouts(self):
        wdg_layout = QtWidgets.QHBoxLayout()
        wdg_layout.addWidget(QtWidgets.QLabel("Name: "))
        wdg_layout.addWidget(self.lineedit)

        btn_layout = QtWidgets.QHBoxLayout()
        btn_layout.addStretch()
        btn_layout.addWidget(self.ok_btn)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.addLayout(wdg_layout)
        main_layout.addLayout(btn_layout)

    def create_connections(self):
        self.ok_btn.clicked.connect(self.accept)

    def get_text(self):
        return (self.lineedit.text())


class TestDialog(QtWidgets.QDialog):

    def __init__(self, parent=maya_main_window()):
        super(TestDialog, self).__init__(parent)

        self.setWindowTitle('Test Dialog')
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)

        self.initial_directory = cmds.internalVar(userPrefDir=True)  # 默认文件窗口打开路径
        self.initial_color = QtGui.QColor(255, 0, 0)  # 默认颜色窗口初始选择的颜色

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.warning_btn = QtWidgets.QPushButton("Warning")
        self.folder_select_btn = QtWidgets.QPushButton("Folder Select")
        self.color_select_btn = QtWidgets.QPushButton("Color Select")
        self.custom_btn = QtWidgets.QPushButton("Modal (Custom)")

    def create_layouts(self):
        main_layout = QtWidgets.QHBoxLayout(self)
        main_layout.addWidget(self.warning_btn)
        main_layout.addWidget(self.folder_select_btn)
        main_layout.addWidget(self.color_select_btn)
        main_layout.addWidget(self.custom_btn)

    def create_connections(self):
        self.warning_btn.clicked.connect(self.show_warning_dialog)
        self.folder_select_btn.clicked.connect(self.show_folder_select)
        self.color_select_btn.clicked.connect(self.show_color_select)
        self.custom_btn.clicked.connect(self.show_custom_dialog)

    def show_warning_dialog(self):
        QtWidgets.QMessageBox.warning(self, "Object Not Found", "Camera 'shotcam' not found.")

    def show_folder_select(self):
        new_directory = QtWidgets.QFileDialog.getExistingDirectory(self, "Select Folder", self.initial_directory)
        if new_directory:
            self.initial_directory = new_directory

        print ("Selected Folder : {}".format(new_directory))

    def show_color_select(self):
        self.initial_color = QtWidgets.QColorDialog.getColor(self.initial_color, self)

        print("Red:{} Green:{} Blue:{}".format(self.initial_color.red(),
                                               self.initial_color.green(),
                                               self.initial_color.blue()))

    def show_custom_dialog(self):
        custom_dialog = CustomDialog()

        result = custom_dialog.exec_()  # 自定义窗口模式 这个模式是打开后只能够在当前窗口操作，窗口关闭前不能执行窗口外的操作

        if result == QtWidgets.QDialog.Accepted:
            print("Name: {}".format(custom_dialog.get_text()))


if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = TestDialog()
    ui.show()

```
<a name="n7TgF"></a>
## 标准Qt对话框
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1660703172622-7846ab65-52cb-4757-bcd4-e64748ce6b24.png#averageHue=%234c4c4c&clientId=u88fb9660-6e1f-4&from=paste&height=523&id=ucbd9754e&originHeight=523&originWidth=665&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86237&status=done&style=none&taskId=ufec16794-3083-451f-87df-542146cd64f&title=&width=665)<br />没找到源码，视频上也没显示全，就不放代码了。
<a name="az5pO"></a>
# QListWidget
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1660710501521-ea737a89-d60d-45aa-996b-a4db34ad19aa.png#averageHue=%23494948&clientId=u88fb9660-6e1f-4&from=paste&height=260&id=u4932fb14&originHeight=260&originWidth=236&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7610&status=done&style=none&taskId=ucf9c9473-c59c-498e-839f-60d0b31d97b&title=&width=236)
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.cmds as cmds


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class OutputResolutionDialog(QtWidgets.QDialog):
    # 数值用带小数点的原因是要计算长宽比，长宽比是小数
    RESOLUTION_ITEMS = [["1920X1080 (1080p)", 1920.0, 1080.0],
                        ["1280X720 (720p)", 1280.0, 720.0],
                        ["960X540 (540p)", 960.0, 540.0],
                        ["640X480", 640.0, 480.0],
                        ["320X240", 320.0, 240.0]]

    def __init__(self, parent=maya_main_window()):
        super(OutputResolutionDialog, self).__init__(parent)

        self.setWindowTitle('Output Resolution')
        self.setFixedWidth(220)
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.resolution_list_wdg = QtWidgets.QListWidget()

        for resolution_item in self.RESOLUTION_ITEMS:
            list_wdg_item = QtWidgets.QListWidgetItem(resolution_item[0])
            # QtCore.Qt.UserRole可以理解为序号0,一个item可以拥有多个数据，因此可以通过QtCore.Qt.UserRole，QtCore.Qt.UserRole+1来设置数据的序号
            list_wdg_item.setData(QtCore.Qt.UserRole,
                                  [resolution_item[1], resolution_item[2]]) 
            self.resolution_list_wdg.addItem(list_wdg_item)

        self.close_btn = QtWidgets.QPushButton('Close')

    def create_layouts(self):
        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.close_btn)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2)  # 设置布局与窗口边界的距离
        main_layout.setSpacing(2)  # 设置布局中的控件之间的间隙
        main_layout.addWidget(self.resolution_list_wdg)
        main_layout.addStretch()
        main_layout.addLayout(button_layout)

    def create_connections(self):
        self.resolution_list_wdg.itemClicked.connect(self.set_output_resolution)

        self.close_btn.clicked.connect(self.close)

    def set_output_resolution(self, item):
        resolution = item.data(QtCore.Qt.UserRole)

        cmds.setAttr("defaultResolution.width", resolution[0])
        cmds.setAttr("defaultResolution.height", resolution[1])
        cmds.setAttr("defaultResolution.deviceAspectRatio", resolution[0]/resolution[1])


if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = OutputResolutionDialog()
    ui.show()

```
<a name="BM1yP"></a>
# 可以设置的选择模式
举例：<br />self.resolution_list_wdg = QtWidgets.QListWidget()<br />self.resolution_list_wdg.setSelectionMode(QtWidgets.QAbstractItemView.MultiSelection) # 设置listWidget控件的选择模式为MultiSelection     <br />ExtendedSelection与MultiSelection的区别是第一个需要按住ctrl或者shift多选，第二个不需要

| Constant | Value | Description |
| --- | --- | --- |
| QAbstractItemView::SingleSelection | 1 | When the user selects an item, any already-selected item becomes unselected. It is possible for the user to deselect the selected item by pressing the Ctrl key when clicking the selected item. |
| QAbstractItemView::ContiguousSelection | 4 | When the user selects an item in the usual way, the selection is cleared and the new item selected. However, if the user presses the Shift key while clicking on an item, all items between the current item and the clicked item are selected or unselected, depending on the state of the clicked item. |
| QAbstractItemView::ExtendedSelection | 3 | When the user selects an item in the usual way, the selection is cleared and the new item selected. However, if the user presses the Ctrl key when clicking on an item, the clicked item gets toggled and all other items are left untouched. If the user presses the Shift key while clicking on an item, all items between the current item and the clicked item are selected or unselected, depending on the state of the clicked item. Multiple items can be selected by dragging the mouse over them. |
| QAbstractItemView::MultiSelection | 2 | When the user selects an item in the usual way, the selection status of that item is toggled and the other items are left alone. Multiple items can be toggled by dragging the mouse over them. |
| QAbstractItemView::NoSelection | 0 | Items cannot be selected. |

<a name="LaZ0H"></a>
# QTableDialog
<a name="PgPfM"></a>
## 显示大纲模型名字以及变换信息窗口
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1660717613536-9bd230fa-ce6a-43ed-8188-b428b498e914.png#averageHue=%23595755&clientId=u88fb9660-6e1f-4&from=paste&height=356&id=ue9e1df1d&originHeight=356&originWidth=691&originalType=binary&ratio=1&rotation=0&showTitle=false&size=76846&status=done&style=none&taskId=ua6156b97-b453-4274-a681-bd2645ee798&title=&width=691)
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.cmds as cmds


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class TableExampleDialog(QtWidgets.QDialog):

    ATTR_ROLE = QtCore.Qt.UserRole
    VALUE_ROLE = QtCore.Qt.UserRole + 1

    def __init__(self, parent=maya_main_window()):
        super(TableExampleDialog, self).__init__(parent)

        self.setWindowTitle('Table Example')
        self.setFixedWidth(500)
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.table_wdg = QtWidgets.QTableWidget()
        self.table_wdg.setColumnCount(5)
        self.table_wdg.setColumnWidth(0, 22)
        self.table_wdg.setColumnWidth(2, 70)
        self.table_wdg.setColumnWidth(3, 70)
        self.table_wdg.setColumnWidth(4, 70)
        self.table_wdg.setHorizontalHeaderLabels(["", "Name", "TransX", "TransY", "TransZ"])
        header_view = self.table_wdg.horizontalHeader()
        header_view.setSectionResizeMode(1, QtWidgets.QHeaderView.Stretch)  # 设置标题栏为自动填充窗口

        self.refresh_btn = QtWidgets.QPushButton("Refresh")
        self.close_btn = QtWidgets.QPushButton("Close")

    def create_layouts(self):
        button_layout = QtWidgets.QHBoxLayout()
        button_layout.setSpacing(2)
        button_layout.addStretch()
        button_layout.addWidget(self.refresh_btn)
        button_layout.addWidget(self.close_btn)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2)
        main_layout.setSpacing(2)
        main_layout.addWidget(self.table_wdg)
        main_layout.addStretch()
        main_layout.addLayout(button_layout)

    def create_connections(self):
        self.set_cell_changed_connection_enabled(True)
        self.refresh_btn.clicked.connect(self.refresh_table)
        self.close_btn.clicked.connect(self.close)

    def set_cell_changed_connection_enabled(self, enabled):  # 设置单元格信号与槽的连接状态  目的是使执行refresh时不执行槽函数
        if enabled:
            self.table_wdg.cellChanged.connect(self.on_cell_changed)
        else:
            self.table_wdg.cellChanged.disconnect(self.on_cell_changed)

    def showEvent(self, e):
        super(TableExampleDialog, self).showEvent(e)  # 当启动窗口时执行这个函数
        self.refresh_table()

    def keyPressEvent(self, e):
        super(TableExampleDialog, self).keyPressEvent(e)
        e.accept()  # 当在工具窗口中使用键盘时不会影响到maya主窗口的对象

    def refresh_table(self):
        self.set_cell_changed_connection_enabled(False)

        self.table_wdg.setRowCount(0)  # 将tableWidget 的所有项清空

        meshes = cmds.ls(typ="mesh")
        for i in range(len(meshes)):
            transform_name = cmds.listRelatives(meshes[i], parent=True)[0]
            translation = cmds.getAttr("{}.translate".format(transform_name))[0]
            visible = cmds.getAttr("{}.visibility".format(transform_name))

            self.table_wdg.insertRow(i)
            self.insert_item(i, 0, "", "visibility", visible, True)
            self.insert_item(i, 1, transform_name, None, transform_name, False)
            self.insert_item(i, 2, self.float_to_string(translation[0]), "tx", translation[0], False)
            self.insert_item(i, 3, self.float_to_string(translation[1]), "ty", translation[0], False)
            self.insert_item(i, 4, self.float_to_string(translation[2]), "tz", translation[0], False)

        self.set_cell_changed_connection_enabled(True)

    def insert_item(self, row, column, text, attr, value, is_boolean):
        item = QtWidgets.QTableWidgetItem(text)
        self.set_item_attr(item, attr)
        self.set_item_value(item, value)
        if is_boolean:
            item.setFlags(QtCore.Qt.ItemIsUserCheckable | QtCore.Qt.ItemIsEnabled)  # 设置复选框
            self.set_item_checked(item, value)

        self.table_wdg.setItem(row, column, item)

    def on_cell_changed(self, row, column):
        # 单元格进行改变时先将信号与槽断开连接，当rename执行完成以后再连接起来
        # 控制信号与槽连接状态的目的就是控制什么时候改变单元格的信息时执行槽函数
        self.set_cell_changed_connection_enabled(False)

        item = self.table_wdg.item(row, column)
        if column == 1:
            self.rename(item)
        else:
            is_boolean = column == 0
            self.update_attr(self.get_full_attr_name(row, item), item, is_boolean)

        self.set_cell_changed_connection_enabled(True)

    def rename(self, item):
        old_name = self.get_item_value(item)
        new_name = self.get_item_text(item)
        if old_name != new_name:
            actual_new_name = cmds.rename(old_name, new_name)
            if actual_new_name != new_name:
                self.set_item_text(item, actual_new_name)
            self.set_item_value(item, actual_new_name)

    def update_attr(self, attr_name, item, is_boolean):
        if is_boolean:
            value = self.is_item_checked(item)
            self.set_item_text(item, "")
        else:
            text = self.get_item_text(item)
            try:
                value = float(text)
            except ValueError:
                self.revert_original_value(item, is_boolean)
                return
        try:
            cmds.setAttr(attr_name, value)
        except:
            self.revert_original_value(item, is_boolean)
            return

        new_value = cmds.getAttr(attr_name)
        if is_boolean:
            self.set_item_checked(item, new_value)
        else:
            self.set_item_text(item, self.float_to_string(new_value))
        self.set_item_value(item, new_value)


    def set_item_text(self, item, text):
        item.setText(text)

    def get_item_text(self, item):
        return item.text()

    def set_item_checked(self, item, checked):
        if checked:
            item.setCheckState(QtCore.Qt.Checked)
        else:
            item.setCheckState(QtCore.Qt.Unchecked)

    def is_item_checked(self, item):
        return item.checkState() == QtCore.Qt.Checked

    def set_item_attr(self, item, attr):
        item.setData(self.ATTR_ROLE, attr)

    def get_item_attr(self, item):
        return item.data(self.ATTR_ROLE)

    def set_item_value(self, item, value):
        item.setData(self.VALUE_ROLE, value)

    def get_full_attr_name(self, row, item):
        node_name = self.table_wdg.item(row, 1).data(self.VALUE_ROLE)
        attr_name = self.get_item_attr(item)
        return "{0}.{1}".format(node_name, attr_name)

    def get_item_value(self, item):
        return item.data(self.VALUE_ROLE)

    def float_to_string(self, value):
        return "{0:.4f}".format(value)  # 令浮点数变成保留四位数的字符串

    def revert_original_value(self, item, is_boolean):
        original_value = self.get_item_value(item)
        if is_boolean:
            self.set_item_checked(item, original_value)
        else:
            self.set_item_text(item, self.flate_to_string(original_value))


if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = TableExampleDialog()
    ui.show()

```
<a name="lWuF1"></a>
## 在表格控件中添加其他控件
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661410775956-afb1b836-aa01-412e-846a-397b927d705f.png#averageHue=%23505050&clientId=u9eaa8f12-95dd-4&from=paste&height=260&id=uabb0d097&originHeight=260&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7437&status=done&style=none&taskId=ua2bdaaf9-3ef7-4efe-9e3c-cdbc5f38ed8&title=&width=316)
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.cmds as cmds


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class TableExampleDialog(QtWidgets.QDialog):

    def __init__(self, parent=maya_main_window()):
        super(TableExampleDialog, self).__init__(parent)

        self.setWindowTitle('Table Example')
        self.setFixedWidth(300)
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.table_wdg = QtWidgets.QTableWidget()
        self.table_wdg.setColumnCount(3)
        self.table_wdg.setHorizontalHeaderLabels(["QPushButton", "QSpinBox", "QComboBox"])
        header_view = self.table_wdg.horizontalHeader()
        header_view.setSectionResizeMode(1, QtWidgets.QHeaderView.Stretch)  # 设置标题栏为自动填充窗口

        self.refresh_btn = QtWidgets.QPushButton("Refresh")
        self.close_btn = QtWidgets.QPushButton("Close")

    def create_layouts(self):
        button_layout = QtWidgets.QHBoxLayout()
        button_layout.setSpacing(2)
        button_layout.addStretch()
        button_layout.addWidget(self.refresh_btn)
        button_layout.addWidget(self.close_btn)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2)
        main_layout.setSpacing(2)
        main_layout.addWidget(self.table_wdg)
        main_layout.addStretch()
        main_layout.addLayout(button_layout)

    def create_connections(self):
        self.refresh_btn.clicked.connect(self.refresh_table)
        self.close_btn.clicked.connect(self.close)
    
    def showEvent(self, e):
        super(TableExampleDialog, self).showEvent(e)  # 当启动窗口时执行这个函数
        self.refresh_table()

    def refresh_table(self):
        self.table_wdg.setRowCount(0)
        self.table_wdg.insertRow(0)

        btn = QtWidgets.QPushButton("Button")
        btn.clicked.connect(self.on_button_pressed)
        self.table_wdg.setCellWidget(0, 0, btn)

        spin_box = QtWidgets.QSpinBox()
        spin_box.valueChanged.connect(self.on_value_changed)
        self.table_wdg.setCellWidget(0, 1, spin_box)

        combo_box = QtWidgets.QComboBox()
        combo_box.addItems(["Item 1", "Item2", "Item3"])
        combo_box.currentTextChanged.connect(self.on_current_text_changed)
        self.table_wdg.setCellWidget(0, 2, combo_box)

    def on_button_pressed(self):
        print("Button was pressed")

    def on_value_changed(self, value):
        print("SpinBox value changed: {}".format(value))

    def on_current_text_changed(self, text):
        print("ComboBox text changed: {}".format(text))


if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = TableExampleDialog()
    ui.show()

```
<a name="tbVxe"></a>
# QSpinBox与QDoubleSpinBox
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661412226518-48951f98-411f-4fd4-9fc4-9b8306dfb70e.png#averageHue=%23737271&clientId=u9eaa8f12-95dd-4&from=paste&height=106&id=uf4e77954&originHeight=106&originWidth=211&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5030&status=done&style=none&taskId=u71974899-6a25-4801-b784-e71cbac61fa&title=&width=211)<br />可以通过鼠标滚轮滑动来更改数值
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.cmds as cmds


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class SpinBoxDialog(QtWidgets.QDialog):

    def __init__(self, parent=maya_main_window()):
        super(SpinBoxDialog, self).__init__(parent)

        self.setWindowTitle('Spin Box Dialog')
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.spin_box = QtWidgets.QSpinBox()
        self.spin_box.setFixedWidth(80)
        self.spin_box.setMinimum(-100)
        self.spin_box.setMaximum(100)
        self.spin_box.setSingleStep(5)
        self.spin_box.setPrefix("$ ")  # 设置显示的前缀 但是不会当值来交互，仅仅是显示
        self.spin_box.setButtonSymbols(QtWidgets.QAbstractSpinBox.NoButtons)  # 取消显示上下按钮框

        self.double_spin_box = QtWidgets.QDoubleSpinBox()
        self.double_spin_box.setFixedWidth(80)
        self.double_spin_box.setRange(-50.0, 50.0)
        self.double_spin_box.setSuffix(" m")

    def create_layouts(self):
        main_layout = QtWidgets.QFormLayout(self)
        main_layout.addRow("Spin Box:", self.spin_box)
        main_layout.addRow("Double Spin Box:", self.double_spin_box)

    def create_connections(self):
        self.spin_box.valueChanged.connect(self.print_value)
        self.double_spin_box.valueChanged.connect(self.print_value)

    def print_value(self, value):
        print("Value: {}".format(value))


if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = SpinBoxDialog()
    ui.show()

```
<a name="L2Pcc"></a>
# 启动maya图标资源管理器
import maya.app.general.resourceBrowser as resourceBrowser<br />resourceBrowser.resourceBrowser().run()<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661419111759-00e4785c-b7ec-4dbf-bc59-ef400fa10604.png#averageHue=%23514f4e&clientId=uc6467607-8068-4&from=paste&height=296&id=ubbdb2553&originHeight=296&originWidth=351&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14092&status=done&style=none&taskId=ue1cf3996-139b-4ae6-9efa-f1f57dc83aa&title=&width=351)<br />在这里可以预览窗口的图标和名字
<a name="uYFCq"></a>
# QTreeView File Explorer
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661422262493-6e04ef7d-e127-46ac-8ba1-ef98557b76b2.png#averageHue=%233d3d3c&clientId=uc6467607-8068-4&from=paste&height=439&id=u3bf9a10f&originHeight=439&originWidth=516&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12708&status=done&style=none&taskId=ua705bd21-cea0-4f6f-ac3c-1470a3bd245&title=&width=516)
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.OpenMaya as om
import maya.cmds as cmds


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class TreeViewDialog(QtWidgets.QDialog):

    WINDOW_TITLE = "Tree View Dialog"

    def __init__(self, parent=maya_main_window()):
        super(TreeViewDialog, self).__init__(parent)

        self.setWindowTitle(self.WINDOW_TITLE)
        self.setMinimumSize(500, 400)
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)

        self.create_widgets()
        self.create_layout()
        self.create_connections()

    def create_widgets(self):
        root_path = "{}scripts".format(cmds.internalVar(userAppDir=True))  # 得到maya脚本目录

        self.model = QtWidgets.QFileSystemModel() # 获得一个FileSystem模式
        self.model.setRootPath(root_path)

        self.tree_view = QtWidgets.QTreeView() # 创建QTreeView控件
        self.tree_view.setModel(self.model) # 为控件添加模式
        self.tree_view.setRootIndex(self.model.index(root_path))
        self.tree_view.hideColumn(1)
        self.tree_view.setColumnWidth(0, 240)

        # self.model.setFilter(QtCore.QDir.Dirs | QtCore.QDir.NoDotAndDotDot)

        self.model.setNameFilters(["*.py"])  # 使只能选中.py后缀的文件
        self.model.setNameFilterDisables(False)  # 将不能选中的文件进行隐藏

    def create_layout(self):
        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2)
        main_layout.addWidget(self.tree_view)


    def create_connections(self):
        self.tree_view.doubleClicked.connect(self.on_double_clicked)

    def on_double_clicked(self, index):
        path = self.model.filePath(index)

        if self.model.isDir(index):
            print("Directory selected: {}".format(path))
        else:
            print("Directory selected: {}".format(path))


if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = TreeViewDialog()
    ui.show()

```
<a name="ornOr"></a>
# 制作简单的大纲
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661497459146-e8a29ae1-0130-4554-abcd-245750f64cfa.png#averageHue=%23494848&clientId=u7b21ee06-bbc2-4&from=paste&height=345&id=ub97e2f98&originHeight=345&originWidth=384&originalType=binary&ratio=1&rotation=0&showTitle=false&size=20501&status=done&style=none&taskId=u9b265fd3-2f15-494b-aa9b-c4a7a3b5274&title=&width=384)
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
from functools import partial
import maya.OpenMayaUI as omui
import maya.OpenMaya as om
import maya.cmds as cmds



def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class SimpleOutliner(QtWidgets.QDialog):
    WINDOW_TITLE = "Simple Outliner"

    def __init__(self, parent=maya_main_window()):
        super(SimpleOutliner, self).__init__(parent)

        self.setWindowTitle(self.WINDOW_TITLE)
        if cmds.about(ntOS=True):
            self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)
        elif cmds.about(macOS=True):
            self.setWindowFlags(QtCore.Qt.Tool)

        self.setMinimumWidth(300)

        self.transform_icon = QtGui.QIcon(":transform.svg")
        self.camera_icon = QtGui.QIcon(":Camera.png")
        self.mesh_icon = QtGui.QIcon(":mesh.svg")

        self.script_job_number = -1

        self.create_actions()
        self.create_widgets()
        self.create_layout()
        self.create_connections()

        self.setContextMenuPolicy(QtCore.Qt.CustomContextMenu)  # 使能显示上下文菜单
        self.customContextMenuRequested.connect(self.show_context_menu)  # 设置上下文菜单的ui

        self.refresh_tree_widget()

    def create_actions(self):
        self.about_action = QtWidgets.QAction("About", self)

        self.display_shape_action = QtWidgets.QAction("Shapes", self)
        self.display_shape_action.setCheckable(True)
        self.display_shape_action.setChecked(True)
        self.display_shape_action.setShortcut(QtGui.QKeySequence("Ctrl+Shift+H"))

    def create_widgets(self):
        self.menu_bar = QtWidgets.QMenuBar()
        display_menu = self.menu_bar.addMenu("Display")
        display_menu.addAction(self.display_shape_action)
        help_menu = self.menu_bar.addMenu("Help")
        help_menu.addAction(self.about_action)

        self.tree_widget = QtWidgets.QTreeWidget()
        self.tree_widget.setSelectionMode(QtWidgets.QAbstractItemView.ExtendedSelection)
        self.tree_widget.setHeaderHidden(True)
        # header = self.tree_widget.headerItem()
        # header.setText(0, "Column 0 Text")

        self.refresh_btn = QtWidgets.QPushButton("Refresh")

    def create_layout(self):
        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.refresh_btn)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2) # 设置左上右下的边距
        main_layout.setSpacing(2)
        main_layout.setMenuBar(self.menu_bar)
        main_layout.addWidget(self.tree_widget)
        main_layout.addLayout(button_layout)

    def create_connections(self):
        self.about_action.triggered.connect(self.about)
        self.display_shape_action.toggled.connect(self.set_shape_nodes_visible)

        self.tree_widget.itemCollapsed.connect(self.update_icon)
        self.tree_widget.itemExpanded.connect(self.update_icon)
        self.tree_widget.itemSelectionChanged.connect(self.select_items)

        self.refresh_btn.clicked.connect(self.refresh_tree_widget)

    def refresh_tree_widget(self):
        self.shape_nodes = cmds.ls(shapes=True)

        self.tree_widget.clear()

        top_level_object_names = cmds.ls(assemblies=True)
        for name in top_level_object_names:
            item = self.create_item(name)
            self.tree_widget.addTopLevelItem(item)

        self.update_selection()

    def create_item(self, name):
        item = QtWidgets.QTreeWidgetItem([name])
        self.add_children(item)
        self.update_icon(item)

        is_shape = name in self.shape_nodes
        item.setData(0, QtCore.Qt.UserRole, is_shape)

        return item

    def add_children(self, item):
        children = cmds.listRelatives(item.text(0), children=True)
        if children:
            for child in children:
                child_item = self.create_item(child)
                item.addChild(child_item)

    def update_icon(self, item):
        object_type = ""

        if item.isExpanded():  # 如果item被展开
            object_type = "transform"
        else:
            child_count = item.childCount()
            if child_count == 0:
                object_type = cmds.objectType(item.text(0))
            elif child_count == 1:
                child_item = item.child(0)
                object_type = cmds.objectType(child_item.text(0))
            else:
                object_type = "transform"
        if object_type == "transform":
            item.setIcon(0, self.transform_icon)
        elif object_type == "camera":
            item.setIcon(0, self.camera_icon)
        elif object_type == "mesh":
            item.setIcon(0, self.mesh_icon)

    def select_items(self):
        items = self.tree_widget.selectedItems()
        names = []
        for item in items:
            names.append(item.text(0))

        cmds.select(names, replace=True)

    def about(self):
        QtWidgets.QMessageBox.about(self, "About Simple Outliner", "Add About Text Here")

    def set_shape_nodes_visible(self, visible):
        iterator = QtWidgets.QTreeWidgetItemIterator(self.tree_widget)
        while iterator.value():
            item = iterator.value()
            is_shape = item.data(0, QtCore.Qt.UserRole)
            if is_shape:
                item.setHidden(not visible)

            iterator += 1

    def show_context_menu(self, point):
        context_menu = QtWidgets.QMenu()
        context_menu.addAction(self.display_shape_action)
        context_menu.addSeparator()  # 分割线
        context_menu.addAction(self.about_action)

        context_menu.exec_(self.mapToGlobal(point))  # 右键显示菜单

    def update_selection(self):
        selection = cmds.ls(selection=True)

        iterator = QtWidgets.QTreeWidgetItemIterator(self.tree_widget)
        while iterator.value():
            item = iterator.value()
            is_selected = item.text(0) in selection
            item.setSelected(is_selected)

            iterator += 1

    def set_script_job_enabled(self, enabled):
        if enabled and self.script_job_number < 0:
            self.script_job_number = cmds.scriptJob(event=["SelectionChanged", partial(self.update_selection)], protected=True)
        elif not enabled and self.script_job_number >= 0:
            cmds.scriptJob(kill=self.script_job_number, force=True)
            self.script_job_number = -1

    def showEvent(self, e):
        super(SimpleOutliner, self).showEvent(e)
        self.set_script_job_enabled(True)

    def closeEvent(self, e):
        if isinstance(self, SimpleOutliner):
            super(SimpleOutliner, self).closeEvent(e)
            self.set_script_job_enabled(False)

if __name__ == '__main__':
    try:
        ui.set_script_job_enabled(False)
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = SimpleOutliner()
    ui.show()

```
<a name="i75Bg"></a>
# 制作进度条
<a name="QCRZm"></a>
## 不同对话框
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661740738923-bdd5fa24-618f-4436-b04c-b92f416af8ff.png#averageHue=%23636262&clientId=u8655e55d-37ca-4&from=paste&height=183&id=uf5be9777&originHeight=183&originWidth=602&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10984&status=done&style=none&taskId=u4732af8d-49c4-43a5-a08f-52902460a05&title=&width=602)
```python
# coding:utf-8
import time
from PySide2 import QtCore
from PySide2 import QtWidgets
from shiboken2 import wrapInstance

import maya.OpenMayaUI as omui
import maya.cmds as cmds



def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class ProgressTestDialog(QtWidgets.QDialog):
    WINDOW_TITLE = "Progress Test"

    def __init__(self, parent=maya_main_window()):
        super(ProgressTestDialog, self).__init__(parent)

        self.setWindowTitle(self.WINDOW_TITLE)
        if cmds.about(ntOS=True):
            self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)
        elif cmds.about(macOS=True):
            self.setWindowFlags(QtCore.Qt.Tool)

        self.setMinimumSize(300, 120)

        self.create_widgets()
        self.create_layout()
        self.create_connections()

    def create_widgets(self):
        self.progress_bar_button = QtWidgets.QPushButton("Do It!")

    def create_layout(self):
        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.progress_bar_button)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2)
        main_layout.addStretch()
        main_layout.addLayout(button_layout)

    def create_connections(self):
        self.progress_bar_button.clicked.connect(self.run_progress_test)

    def run_progress_test(self):
        number_of_operations = 10  # 循环的数量

        progress_dialog = QtWidgets.QProgressDialog("Waiting to process...", "Cancel", 0, number_of_operations, self)
        progress_dialog.setWindowTitle("Progress...")
        progress_dialog.setValue(0)
        progress_dialog.setWindowModality(QtCore.Qt.WindowModal)  # 设置为进度条窗口出现时，代码依然能够执行，但是不能使用除对话框之外的操作
        progress_dialog.show()

        QtCore.QCoreApplication.processEvents()  # 在执行代码之前显示对话框

        for i in range(1, number_of_operations + 1):
            if progress_dialog.wasCanceled():  # 当按了cancel按钮后中止代码
                break
            progress_dialog.setLabelText("Processing operation: {0} (fo {1})".format(i, number_of_operations))
            progress_dialog.setValue(i)
            time.sleep(0.5)

            QtCore.QCoreApplication.processEvents()  # 显示对话框的内容

        progress_dialog.close()



if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = ProgressTestDialog()
    ui.show()

```

换一个函数举例
```python
    def run_progress_test(self):

        mesh_list = cmds.ls(assemblies=True)
        number_of_operations = len(mesh_list)

        progress_dialog = QtWidgets.QProgressDialog("Waiting to process...", "Cancel", 0, number_of_operations, self)
        progress_dialog.setWindowTitle("Progress...")
        progress_dialog.setValue(0)
        progress_dialog.setWindowModality(QtCore.Qt.WindowModal)  # 设置为进度条窗口出现时，代码依然能够执行，但是不能使用除对话框之外的操作
        progress_dialog.show()

        QtCore.QCoreApplication.processEvents()  # 在执行代码之前显示对话框

        for num,i in enumerate(mesh_list):
            if progress_dialog.wasCanceled():  # 当按了cancel按钮后中止代码
                break
            progress_dialog.setLabelText("{0}".format(i))
            progress_dialog.setValue(num)
            print i
            time.sleep(0.5)

            QtCore.QCoreApplication.processEvents()  # 显示对话框的内容

        progress_dialog.close()

```
<a name="gP9wT"></a>
## 同一个对话框
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661744051767-0810ebd0-b8ae-434d-ac81-c539eb784adf.png#averageHue=%23696969&clientId=u8655e55d-37ca-4&from=paste&height=139&id=u6ef4cc63&originHeight=139&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3399&status=done&style=none&taskId=ud246af90-c02d-4c8b-a77b-e03625aadad&title=&width=316)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661744057610-f2773001-1ecb-4c07-b68f-8eabdd426779.png#averageHue=%23696968&clientId=u8655e55d-37ca-4&from=paste&height=139&id=u9287f141&originHeight=139&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5246&status=done&style=none&taskId=u7482b385-c5c1-46f8-aa0e-a9604252dce&title=&width=316)

```python
# coding:utf-8
import time
from PySide2 import QtCore
from PySide2 import QtWidgets
from shiboken2 import wrapInstance

import maya.OpenMayaUI as omui
import maya.cmds as cmds



def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class ProgressTestDialog(QtWidgets.QDialog):
    WINDOW_TITLE = "Progress Test"

    def __init__(self, parent=maya_main_window()):
        super(ProgressTestDialog, self).__init__(parent)

        self.setWindowTitle(self.WINDOW_TITLE)
        if cmds.about(ntOS=True):
            self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)
        elif cmds.about(macOS=True):
            self.setWindowFlags(QtCore.Qt.Tool)

        self.setMinimumSize(300, 100)

        self.test_in_progress = False

        self.create_widgets()
        self.create_layout()
        self.create_connections()

    def create_widgets(self):
        self.progress_bar_label = QtWidgets.QLabel("Operation Progress")
        self.progress_bar = QtWidgets.QProgressBar()

        self.progress_bar_button = QtWidgets.QPushButton("Do It!")
        self.cancel_button = QtWidgets.QPushButton("Cancel")

        self.update_visibility()

    def create_layout(self):
        progress_layout = QtWidgets.QVBoxLayout()
        progress_layout.addWidget(self.progress_bar_label)
        progress_layout.addWidget(self.progress_bar)

        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.progress_bar_button)
        button_layout.addWidget(self.cancel_button)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2) # 设置左上右下的边距
        main_layout.addLayout(progress_layout)
        main_layout.addStretch()
        main_layout.addLayout(button_layout)

    def create_connections(self):
        self.progress_bar_button.clicked.connect(self.run_progress_test)
        self.cancel_button.clicked.connect(self.cancel_progress_test)

    def update_visibility(self):
        self.progress_bar_label.setVisible(self.test_in_progress)
        self.progress_bar.setVisible(self.test_in_progress)

        self.cancel_button.setVisible(self.test_in_progress)
        self.progress_bar_button.setHidden(self.test_in_progress)

    def run_progress_test(self):
        if self.test_in_progress:
            return

        number_of_operation = 10

        self.progress_bar.setRange(0, number_of_operation)
        self.progress_bar.setValue(0)
        self.progress_bar_label.setText("Operation Progress")

        self.test_in_progress = True
        self.update_visibility()

        for i in range(1, number_of_operation + 1):
            if not self.test_in_progress:
                break

            self.progress_bar_label.setText("Processing operation: {0} (of {1})".format(i, number_of_operation))
            self.progress_bar.setValue(i)
            time.sleep(0.5)

            QtCore.QCoreApplication.processEvents()

        self.test_in_progress = False
        self.update_visibility()

    def cancel_progress_test(self):
        self.test_in_progress = False


if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = ProgressTestDialog()
    ui.show()

```
<a name="oQ0bx"></a>
# QWidget vs QDialog
<a name="GiDDj"></a>
## QWidget与QDialog的显示区别

首先一个区别就是这两个<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1662026474082-19caa88c-f472-4130-9f16-c0d88eee7657.png#averageHue=%23494949&clientId=u283bb055-7ea9-4&from=paste&height=337&id=u7f86f38f&originHeight=337&originWidth=918&originalType=binary&ratio=1&rotation=0&showTitle=false&size=45973&status=done&style=none&taskId=ub15c8f00-9cf4-4090-ae90-0b144a8e8c6&title=&width=918)<br />但是如果想要使用QWidget窗口的话可能会出现窗口不能独立显示出画面中，可能会内嵌到maya主窗口中，要想使用QWidget需要解决这个问题。<br />导致QWidget窗口内嵌到maya主窗口中的原因是因为之前都一直设置的将maya主窗口设置为我们的工具UI的parent，因此QWidget会内嵌到maya主窗口中。<br />要想解决QWidget窗口内嵌到maya主窗口，这里给出一个QWidget的案例<br />主要解决代码为：self.setWindowFlags(QtCore.Qt.WindowType.Window)<br />**这行代码也可以直接用在QDialog的案例上面，可以直接将QDialog中的窗口类型改为Window。使QDialog窗口也能够显示最小化最大化窗口按钮**
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class TestDialog(QtWidgets.QWidget):
    WINDOW_TITLE = "Window Test"

    def __init__(self, parent=maya_main_window()):
        super(TestDialog, self).__init__(parent)

        self.setWindowTitle(self.WINDOW_TITLE)
        self.setMinimumSize(300, 200)
        self.setWindowFlags(QtCore.Qt.WindowType.Window)

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.ok_button = QtWidgets.QPushButton("OK")
        self.ok_button.setMinimumWidth(80)
        self.cancel_button = QtWidgets.QPushButton("Cancel")
        self.cancel_button.setMinimumWidth(80)

    def create_layouts(self):
        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.ok_button)
        button_layout.addWidget(self.cancel_button)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2)
        main_layout.addStretch()
        main_layout.addLayout(button_layout)

    def create_connections(self):
        pass


if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = TestDialog()
    ui.show()
```
<a name="hAiut"></a>
# 添加图片（QImage，QPixmap）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1662358835263-488379c3-ddef-4112-9de1-9efe02044a60.png#averageHue=%23ceb079&clientId=u4f2d97de-80f8-4&from=paste&height=259&id=u9f6dd67f&originHeight=259&originWidth=619&originalType=binary&ratio=1&rotation=0&showTitle=false&size=112997&status=done&style=none&taskId=u3f249d07-3316-4b17-8bfe-078053fe98f&title=&width=619)左边是使用平滑模式，右边没有使用。<br />image = image.scaled(280, 100, QtCore.Qt.IgnoreAspectRatio, QtCore.Qt.SmoothTransformation)  # 使用平滑模式，使缩小图片时不会丢失细节。<br />QPushButton 使用setIcon方法<br />QLabel 使用setPixmap方法<br />设置pixmap对象时需要为pixmap指定一个image对象，调整图片就调整image。
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.OpenMaya as om
import maya.cmds as cmds


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class TestDialog(QtWidgets.QDialog):
    FILE_FILTERS = "Maya(*.ma *.mb);;Maya ASCII (*.ma);;Maya Binary (*.mb);;All Files (*.*)"  # 全部的过滤项

    selected_filter = "Maya (*.ma *.mb)"  # 记录选择的过滤项，每次更改过滤项的同时会更改这个全局变量的值

    def __init__(self, parent=maya_main_window()):
        super(TestDialog, self).__init__(parent)

        self.setWindowTitle('Open/Import/Reference')
        self.setMinimumSize(300, 80)
        self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        self.create_title_label()

        self.filepath_le = QtWidgets.QLineEdit()
        self.select_file_path_btn = QtWidgets.QPushButton()
        self.select_file_path_btn.setIcon(QtGui.QIcon(':fileOpen.png'))
        self.select_file_path_btn.setToolTip("select File")

        self.open_rb = QtWidgets.QRadioButton("Open")
        self.open_rb.setChecked(True)
        self.import_rb = QtWidgets.QRadioButton("Import")
        self.reference_rb = QtWidgets.QRadioButton("Reference")

        self.force_cb = QtWidgets.QCheckBox("Force")

        self.apply_btn = QtWidgets.QPushButton("Apply")
        self.close_btn = QtWidgets.QPushButton("Close")

    def create_title_label(self):
        image_path = "D:/ZhangRuiChen/image/test_image.jpg"
        image = QtGui.QImage(image_path)
        image = image.scaled(280, 100, QtCore.Qt.IgnoreAspectRatio, QtCore.Qt.SmoothTransformation)

        pixmap = QtGui.QPixmap()
        pixmap.convertFromImage(image)

        self.title_label = QtWidgets.QLabel("My Awesome Utility")
        self.title_label.setPixmap(pixmap)

    def create_layouts(self):
        file_path_layout = QtWidgets.QHBoxLayout()
        file_path_layout.addWidget(self.filepath_le)
        file_path_layout.addWidget(self.select_file_path_btn)

        radio_btn_layout = QtWidgets.QHBoxLayout()
        radio_btn_layout.addWidget(self.open_rb)
        radio_btn_layout.addWidget(self.import_rb)
        radio_btn_layout.addWidget(self.reference_rb)

        forme_layout = QtWidgets.QFormLayout()
        forme_layout.addRow("File", file_path_layout)
        forme_layout.addRow("", radio_btn_layout)
        forme_layout.addRow("", self.force_cb)

        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.apply_btn)
        button_layout.addWidget(self.close_btn)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.addWidget(self.title_label)
        main_layout.addLayout(forme_layout)
        main_layout.addLayout(button_layout)

    def create_connections(self):
        self.select_file_path_btn.clicked.connect(self.show_file_select_dialog)

        self.open_rb.toggled.connect(self.update_force_visibility)

        self.apply_btn.clicked.connect(self.load_file)
        self.close_btn.clicked.connect(self.close)

    def show_file_select_dialog(self):
        file_path, self.selected_filter = QtWidgets.QFileDialog.getOpenFileName(self, "Select File", "",
                                                                                self.FILE_FILTERS, self.selected_filter)
        if file_path:
            self.filepath_le.setText(file_path)

    def update_force_visibility(self, checked):
        self.force_cb.setVisible(checked)

    def load_file(self):
        file_path = self.filepath_le.text()
        if not file_path:
            return

        file_info = QtCore.QFileInfo(file_path)  # 得到文件的信息
        if not file_info.exists():  # 判断文件是否存在
            om.MGlobal.displayError("File does not exist: {}".format(file_path))
            return
        if self.open_rb.isChecked():
            self.open_file(file_path)
        if self.import_rb.isChecked():
            self.import_file(file_path)
        else:
            self.reference_file(file_path)

    def open_file(self, file_path):
        force = self.force_cb.isChecked()
        if not force and cmds.file(q=True, modified=True):
            result = QtWidgets.QMessageBox.question(self, "Modified", "Current scene has unsaved changes. Continue?")
            if result == QtWidgets.QMessageBox.StandardButton.Yes:
                force = True
            else:
                return
        cmds.file(file_path, open=True, ignoreVersion=True, force=force)

    def import_file(self, file_path):
        cmds.file(file_path, i=True, ignoreVersion=True)

    def reference_file(self, file_path):
        cmds.file(file_path, r=True, ignoreVersion=True)


if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = TestDialog()
    ui.show()

```
<a name="jN8Ha"></a>
# 遍历文件夹列出树结构
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671160357979-d432cf28-a6dd-4089-a185-1fca578d8897.png#averageHue=%23484847&clientId=u0295db91-fe64-4&from=paste&height=309&id=u14a78c68&originHeight=278&originWidth=262&originalType=binary&ratio=1&rotation=0&showTitle=false&size=6045&status=done&style=none&taskId=u0d81fb05-71d8-41c8-817f-2df86fdee7e&title=&width=291.11111882292215)
```python
# coding:utf-8
# 以树状结构显示指定路径下的所有内容，并且可以通过右键打开资源管理器并进入路径
from PySide2 import QtCore
from PySide2 import QtGui
from PySide2 import QtWidgets
from shiboken2 import wrapInstance

import maya.cmds as cmds
import maya.OpenMayaUI as omui

def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)

class FileExplorerDialog(QtWidgets.QDialog):

    WINDOW_TITLE = "File Explorer"

    DIRECTOR_PATH = "{0}scripts".format(cmds.internalVar(userAppDir=True))

    def __init__(self, parent=maya_main_window()):
        super(FileExplorerDialog, self).__init__(parent)

        self.setWindowTitle(self.WINDOW_TITLE)
        if cmds.about(ntOS=True):
            self.setWindowFlags(self.windowFlags() ^ QtCore.Qt.WindowContextHelpButtonHint)
        elif cmds.about(macOS=True):
            self.setWindowFlags(QtCore.Qt.Tool)

        self.create_actions()
        self.create_widgets()
        self.create_layout()
        self.create_connections()

        self.tree_wdg.setContextMenuPolicy(QtCore.Qt.CustomContextMenu) # 使Context菜单只针对tree_wdg
        self.tree_wdg.customContextMenuRequested.connect(self.show_context_menu) # 使Context菜单为自定义的并给出菜单

        self.refresh_list()

    def create_actions(self):
        self.show_in_folder_action = QtWidgets.QAction("Show in Folder", self)

    def create_widgets(self):
        self.path_label = QtWidgets.QLabel(self.DIRECTOR_PATH)

        self.tree_wdg = QtWidgets.QTreeWidget()
        self.tree_wdg.setHeaderHidden(True)

        self.close_btn = QtWidgets.QPushButton("Close")
    
    def create_layout(self):
        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.close_btn)

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2) # 设置左上右下的边距
        main_layout.addWidget(self.path_label)
        main_layout.addWidget(self.tree_wdg)
        main_layout.addLayout(button_layout)
    
    def create_connections(self):
        self.close_btn.clicked.connect(self.close)
        self.show_in_folder_action.triggered.connect(self.show_in_folder)

    def refresh_list(self):
        """ 显示文件树状结构 """
        self.tree_wdg.clear()

        self.add_children(None, self.DIRECTOR_PATH)
    
    def add_children(self, parent_item, dir_path):
        """ 添加所有的子节点 """
        directory = QtCore.QDir(dir_path) # 创建目录为dir_path的QDir对象
        # entryList作用是得到目录下的所有文件的字符串列表，参数第一个是设置过滤器，这里是要所有项并且没有.和..   第二个是设置排列，目录在最上方并且不区分大小写
        files_in_directory = directory.entryList(QtCore.QDir.NoDotAndDotDot | QtCore.QDir.AllEntries, QtCore.QDir.DirsFirst | QtCore.QDir.IgnoreCase) 

        for file_name in files_in_directory:
            self.add_child(parent_item, dir_path, file_name)

    def add_child(self, parent_item, dir_path, file_name):
        """ 实现添加子节点 """
        file_path = "{0}/{1}".format(dir_path, file_name)
        file_info = QtCore.QFileInfo(file_path)

        if file_info.suffix().lower() == "pyc": # 过滤后缀为pyc的文件
            return

        item = QtWidgets.QTreeWidgetItem(parent_item, [file_name])
        item.setData(0, QtCore.Qt.UserRole, file_path) # QtCore.Qt.UserRole可以理解为序号0,一个item可以拥有多个数据，因此可以通过QtCore.Qt.UserRole，QtCore.Qt.UserRole+1来设置数据的序号

        if file_info.isDir():
            """ 如果是文件夹就用add_children方法 """
            self.add_children(item, file_info.absoluteFilePath())

        if not parent_item:
            """ 将item添加到最顶层树结构中 """
            self.tree_wdg.addTopLevelItem(item)

    def show_context_menu(self, pos):
        """ 自定义菜单 """
        item = self.tree_wdg.itemAt(pos) # 鼠标位置处的item
        if not item:
            return
        
        file_path = item.data(0, QtCore.Qt.UserRole) # 得到item里的数据
        self.show_in_folder_action.setData(file_path) # 设置action对应的数据

        context_menu = QtWidgets.QMenu() # 创建一个菜单
        context_menu.addAction(self.show_in_folder_action) # 将action添加到菜单下
        context_menu.exec_(self.tree_wdg.mapToGlobal(pos)) # 在鼠标位置处右键显示菜单

    def show_in_folder(self):
        file_path = self.show_in_folder_action.data()
        
        if cmds.about(windows=True): # 如果是windows系统就使用windows系统的方法打开资源管理器
            if self.open_in_explorer(file_path): 
                return
        elif cmds.about(macOS=True): # 如果是mac系统就使用mac系统的方法打开资源管理器
            if self.open_in_finder(file_path):
                return
        # 两个方法都不可以的情况下，使用Qt自带的方法打开，缺点是不能自动选择对应的文件
        file_info = QtCore.QFileInfo(file_path)
        if file_info.isDir(): # 如果是路径是目录就直接使用
            QtGui.QDesktopServices.openUrl(file_path)
        else: # 如果是文件就通过file_info.path方法得到目录路径
            QtGui.QDesktopServices.openUrl(file_info.path())
    
    def open_in_explorer(self, file_path):
        """ Windows打开资源管理器 """
        file_info = QtCore.QFileInfo(file_path)
        args = []
        if not file_info.isDir(): # 如果不是目录就选择路径对应的文件
            args.append("/select,")
        
        args.append(QtCore.QDir.toNativeSeparators(file_path))

        if QtCore.QProcess.startDetached("explorer", args):
            return True
        
        return False
    
    def open_in_finder(self, file_path):
        args = []
        args.append('-e')
        args.append('tell application "Finder"')
        args.append('-e')
        args.append('activate')
        args.append('-e')
        args.append('select POSIX file "{0}"'.format(file_path))
        args.append('-e')
        args.append('end tell')
        args.append('-e')
        args.append('return')

        if(QtCore.QPrecess.startDetached("/usr/bin/osascript", args)):
            return True
        
        return False
    
    
if __name__ == "__main__":

    try:
        my_dialog.close()  
        my_dialog.deleteLater()
    except:
        pass

    my_dialog = FileExplorerDialog()
    my_dialog.show()
    
        
```
<a name="NIYFB"></a>
# 灯光面板
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1672827738289-ccf9c154-f02e-4b86-9323-dde79302d9bb.png#averageHue=%23595958&clientId=u1b81c09d-af2e-4&from=paste&height=324&id=u58ec6abd&originHeight=292&originWidth=502&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13895&status=done&style=none&taskId=uf8b0edb7-09fb-4b48-a1c4-4ca5add6f0d&title=&width=557.7777925538431)
```python
# coding:utf-8
# 灯光面板举例
from functools import partial
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.cmds as cmds


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)

class CustomColorButton(QtWidgets.QWidget): # 自定义颜色按钮

    color_changed = QtCore.Signal(QtGui.QColor) # 自定义信号

    def __init__(self, color=QtCore.Qt.white, parent=None): # 表示可以类接收一个颜色参数,默认是白色
        super(CustomColorButton, self).__init__(parent)

        self.setObjectName("CustomColorButton")

        self.create_control()

        self.set_size(50, 14)
        self.set_color(color) # 设置初始颜色,如果对象有传过来颜色设置则为对象的颜色

    def create_control(self):
        """ 1. 创建colorSliderGrp """
        window = cmds.window()
        self._name = cmds.colorSliderGrp()
        # print("original name: {0}".format(self._name))

        """ 2. 找到colorSliderGrp控件 """
        color_slider_obj = omui.MQtUtil.findControl(self._name) # color_slider_obj是一个c++的形式
        if color_slider_obj:
            self._color_slider_widget = wrapInstance(long(color_slider_obj), QtWidgets.QWidget)
        
            """ 3. 将colorSliderGrp控件的父级设置为这个自定义控件 """
            main_layout = QtWidgets.QVBoxLayout(self)
            main_layout.setObjectName("main_layout")
            main_layout.setContentsMargins(0, 0, 0, 0)
            main_layout.addWidget(self._color_slider_widget)

            """ 4. 更新colorSliderGrp的control name (之前是属于maya的) """
            self._name = self._color_slider_widget.objectName()
            # print("new name: {0}".format(self._name))

            """ 5. 识别或存储 colorSliderGrp的子控件(在必要的时候可以隐藏它) """
            # children = self._color_slider_widget.children()
            # for child in children:
            #     print(child)
            #     print(child.objectName())
            # print("---")

            self._slider_widget = self._color_slider_widget.findChild(QtWidgets.QWidget, "slider")
            if self._slider_widget:
                self._slider_widget.hide()
            
            self._color_widget = self._color_slider_widget.findChild(QtWidgets.QWidget, "port")

            cmds.colorSliderGrp(self._name, e=True, changeCommand=partial(self.on_color_changed))

        cmds.deleteUI(window, window=True)
          
    
    def set_size(self, width, height):
        self._color_slider_widget.setFixedWidth(width)
        self._color_widget.setFixedHeight(height)
    
    def set_color(self, color):
        color = QtGui.QColor(color)

        if color != self.get_color():
            cmds.colorSliderGrp(self._name, e=True, rgbValue=(color.redF(), color.greenF(), color.blueF())) # F代表以浮点数表示
            self.on_color_changed()
    
    def get_color(self):
        color = cmds.colorSliderGrp(self._name, q=True, rgbValue=True)

        color = QtGui.QColor(color[0] *255, color[1] * 255, color[2] * 255)
        return color
      
    def on_color_changed(self, *args):
        self.color_changed.emit(self.get_color())

class LightItem(QtWidgets.QWidget):
    # 自定义灯光控件，一个灯光对应一个控件

    SUPPORTED_TYPES = ["ambientLight", "directionalLight", "pointLight", "spotLight", "areaLight"]
    EMIT_TYPES = ["directionalLight", "pointLight", "spotLight", "areaLight"]

    node_deleted = QtCore.Signal(str) # 自定义节点删除时的信号

    def __init__(self, shape_name, parent=None):
        super(LightItem, self).__init__(parent)

        self.setFixedHeight(26)

        self.shape_name = shape_name # 灯光的shape名字
        self.uuid = cmds.ls(shape_name, uuid=True) # 灯光的uuid

        self.script_jobs = []

        self.create_widgets()
        self.create_layout()
        self.create_connections()

        self.create_script_jobs()
    
    def create_widgets(self):
        """ 创建控件 """
        self.light_type_btn = QtWidgets.QPushButton()
        self.light_type_btn.setFixedSize(20, 20)
        self.light_type_btn.setFlat(True) # 设置按钮的显示形式

        self.visiblity_cb = QtWidgets.QCheckBox()
        
        self.transform_name_label = QtWidgets.QLabel("placeholder")
        self.transform_name_label.setFixedWidth(120)
        self.transform_name_label.setAlignment(QtCore.Qt.AlignCenter)

        light_type = self.get_light_type()
        if light_type in self.SUPPORTED_TYPES:
            self.intensity_dsb = QtWidgets.QDoubleSpinBox()
            self.intensity_dsb.setRange(0.0, 100.0)
            self.intensity_dsb.setDecimals(3) # 设置数值到小数点后三位
            self.intensity_dsb.setSingleStep(0.1)
            self.intensity_dsb.setButtonSymbols(QtWidgets.QAbstractSpinBox.NoButtons) # 设置spinbox没有上下箭头

            self.color_btn = CustomColorButton()

            if light_type in self.EMIT_TYPES:
                self.emit_diffuse_cb = QtWidgets.QCheckBox()
                self.emit_specular_cb = QtWidgets.QCheckBox()
        
        self.update_values()
    
    def create_layout(self):
        """ 创建布局 """
        main_layout = QtWidgets.QHBoxLayout(self)
        main_layout.setContentsMargins(0, 0, 0, 0)
        main_layout.addWidget(self.light_type_btn)
        main_layout.addWidget(self.visiblity_cb)
        main_layout.addWidget(self.transform_name_label)

        light_type = self.get_light_type()
        if light_type in self.SUPPORTED_TYPES:
            main_layout.addWidget(self.intensity_dsb)
            main_layout.addSpacing(10)
            main_layout.addWidget(self.color_btn)

            if light_type in self.EMIT_TYPES:
                main_layout.addSpacing(34)
                main_layout.addWidget(self.emit_diffuse_cb)
                main_layout.addSpacing(50)
                main_layout.addWidget(self.emit_specular_cb)

        main_layout.addStretch()
    
    def create_connections(self):
        """ 创建信号与槽的连接 """
        self.light_type_btn.clicked.connect(self.select_light)
        self.visiblity_cb.toggled.connect(self.set_visibility)
        
        light_type = self.get_light_type()
        if light_type in self.SUPPORTED_TYPES:
            self.intensity_dsb.editingFinished.connect(self.on_intensity_changed)
            self.color_btn.color_changed.connect(self.set_color)

            if light_type in self.EMIT_TYPES:
                self.emit_diffuse_cb.toggled.connect(self.set_emit_diffuse)
                self.emit_specular_cb.toggled.connect(self.set_emit_specular)

    def update_values(self):
        self.light_type_btn.setIcon(self.get_light_type_icon())
        self.visiblity_cb.setChecked(self.is_visible())
        self.transform_name_label.setText(self.get_transform_name())

        light_type = self.get_light_type()
        if light_type in self.SUPPORTED_TYPES:
            self.intensity_dsb.setValue(self.get_intensity())
            self.color_btn.set_color(self.get_color())
            
            if light_type in self.EMIT_TYPES:
                self.emit_diffuse_cb.setChecked(self.emits_diffuse())
                self.emit_specular_cb.setChecked(self.emits_specular())

    def get_transform_name(self):
        return cmds.listRelatives(self.shape_name, parent=True)[0]

    def get_attribute_value(self, name, attribute):
        return cmds.getAttr("{0}.{1}".format(name, attribute))

    def set_attribute_value(self, name, attribute,*args):

        # 如果设置颜色或者属性的值与当前值相同就不进行设置，避免script job产生的重复设置属性的bug
        if attribute == "color":
            if self.get_color() == self.color_btn.get_color():
                return
        elif args[0] == self.get_attribute_value(name, attribute):
            return
        
        attr_name = "{0}.{1}".format(name, attribute)
        cmds.setAttr(attr_name, *args)

    def get_light_type(self):
        return cmds.objectType(self.shape_name)

    def get_light_type_icon(self):
        light_type = self.get_light_type()

        icon = QtGui.QIcon()
        if light_type == "ambientLight":
            icon = QtGui.QIcon(":ambientLight.svg")
        elif light_type == "directionalLight":
            icon = QtGui.QIcon(":directionalLight.svg")
        elif light_type == "pointLight":
            icon = QtGui.QIcon(":pointLight.svg")
        elif light_type == "spotLight":
            icon = QtGui.QIcon(":spotLight.svg")
        else:
            icon = QtGui.QIcon(":Light.png")

        return icon

    def is_visible(self):
        transform_name = self.get_transform_name()
        return self.get_attribute_value(transform_name, "visibility")
    
    def get_intensity(self):
        return self.get_attribute_value(self.shape_name, "intensity")

    def get_color(self):
        temp_color = self.get_attribute_value(self.shape_name, "color")[0]
        return QtGui.QColor(temp_color[0] * 255, temp_color[1] * 255, temp_color[2] * 255)

    def emits_diffuse(self):
        return self.get_attribute_value(self.shape_name, "emitDiffuse")

    def emits_specular(self):
        return self.get_attribute_value(self.shape_name, "emitSpecular")
    
    def select_light(self):
        cmds.select(self.get_transform_name())

    def set_visibility(self, checked):
        self.set_attribute_value(self.get_transform_name(), "visibility", checked)
    
    def on_intensity_changed(self):
        self.set_attribute_value(self.shape_name, "intensity", self.intensity_dsb.value())
    
    def set_color(self, color):
        self.set_attribute_value(self.shape_name, "color", color.redF(), color.greenF(), color.blueF())
    
    def set_emit_diffuse(self, checked):
        self.set_attribute_value(self.shape_name, "emitDiffuse", checked)

    def set_emit_specular(self, checked):
        self.set_attribute_value(self.shape_name, "emitSpecular", checked)

    def on_node_deleted(self):
        """ 当节点删除时执行 """
        self.node_deleted.emit(self.shape_name)

    def on_name_changed(self):
        """ 当名字修改时执行 """
        self.shape_name = cmds.ls(self.uuid)[0]
        self.update_values()
    
    def create_script_jobs(self):
        """ 为每个灯光都创建script jobs """
        self.delete_script_jobs()

        self.add_attribute_change_script_job(self.get_transform_name(), "visibility")
        light_type = self.get_light_type()
        if light_type in self.SUPPORTED_TYPES:
            self.add_attribute_change_script_job(self.shape_name, "color")
            self.add_attribute_change_script_job(self.shape_name, "intensity")

            if light_type in self.EMIT_TYPES:
                self.add_attribute_change_script_job(self.shape_name, "emitDiffuse")
                self.add_attribute_change_script_job(self.shape_name, "emitSpecular")

        self.script_jobs.append(cmds.scriptJob(nodeDeleted=(self.shape_name, partial(self.on_node_deleted))))
        self.script_jobs.append(cmds.scriptJob(nodeNameChanged=(self.shape_name, partial(self.on_name_changed))))
    
    def add_attribute_change_script_job(self, name, attribute):
        """ 添加某一节点的某一属性改变时的script_job时使用的方法 """
        self.script_jobs.append(cmds.scriptJob(attributeChange=("{0}.{1}".format(name, attribute), partial(self.update_values))))

    def delete_script_jobs(self):
        for job_number in self.script_jobs:
            cmds.evalDeferred("if cmds.scriptJob(exists={0}):\tcmds.scriptJob(kill={0}, force=True)".format(job_number))
        
        self.script_jobs = []
    

class LightPanel(QtWidgets.QDialog):

    WINDOW_TITLE = "Light Panel"

    def __init__(self, parent=maya_main_window()):
        super(LightPanel, self).__init__(parent)
        
        self.setWindowTitle(self.WINDOW_TITLE)
        self.setMinimumSize(500, 260)
        self.setWindowFlags(QtCore.Qt.WindowType.Window)

        self.light_items = []
        self.script_jobs = []

        self.create_widgets()
        self.create_layouts()
        self.create_connections()

    def create_widgets(self):
        """ 控件 """
        self.refreshButton = QtWidgets.QPushButton("Refresh Lights")

    def create_layouts(self):
        """ 布局 """
        header_layout = QtWidgets.QHBoxLayout()
        header_layout.addSpacing(100)
        header_layout.addWidget(QtWidgets.QLabel("Light"))
        header_layout.addSpacing(50)
        header_layout.addWidget(QtWidgets.QLabel("Intensity"))
        header_layout.addSpacing(44)
        header_layout.addWidget(QtWidgets.QLabel("Color"))
        header_layout.addSpacing(24)
        header_layout.addWidget(QtWidgets.QLabel("Emit Diffuse"))
        header_layout.addSpacing(10)
        header_layout.addWidget(QtWidgets.QLabel("Emit Spec"))
        header_layout.addStretch()

        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.refreshButton)

        light_list_wdg = QtWidgets.QWidget()

        self.light_layout = QtWidgets.QVBoxLayout(light_list_wdg) # light_list_wdg在light_layout下
        self.light_layout.setContentsMargins(2, 2, 2, 2)
        self.light_layout.addSpacing(3)
        self.light_layout.setAlignment(QtCore.Qt.AlignTop)

        light_list_scroll_area = QtWidgets.QScrollArea()
        light_list_scroll_area.setWidgetResizable(True)
        light_list_scroll_area.setWidget(light_list_wdg) # scroll_area下有light_list_wdg

        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2)
        main_layout.addLayout(header_layout)
        main_layout.addWidget(light_list_scroll_area) # 主布局下有个scroll_area
        main_layout.addLayout(button_layout)

    def create_connections(self):
        """ 信号与槽的连接 """
        self.refreshButton.clicked.connect(self.refresh_lights)
        
    def get_lights_in_scene(self):
        """ 得到场景中所有灯光 """
        return cmds.ls(typ="light")

    def refresh_lights(self):
        """ 刷新灯光面板 """
        self.clear_lights()

        scene_lights = self.get_lights_in_scene()
        for light in scene_lights:
            light_item = LightItem(light)
            light_item.node_deleted.connect(self.on_node_deleted) # 自定义信号node_deleted发送数据时传给on_node_deleted函数

            self.light_layout.addWidget(light_item)
            self.light_items.append(light_item)
            
    
    def clear_lights(self):
        """ 清空灯光面板 """
        for light in self.light_items:
            light.delete_script_jobs()

        self.light_items = []
        
        while self.light_layout.count() > 0:
            light_item = self.light_layout.takeAt(0)
            if light_item.widget():
                light_item.widget().deleteLater()
    
    def create_script_jobs(self):
        """ 创建script jobs """
        self.script_jobs.append(cmds.scriptJob(event=["DagObjectCreated", partial(self.on_dag_object_created)])) # 当创建dag物体时执行on_dag_object_created函数
        self.script_jobs.append(cmds.scriptJob(event=["Undo", partial(self.on_undo)])) # 当ctrl+z时执行on_undo函数

    def delete_script_jobs(self):
        """ 删除script jobs """
        for job_number in self.script_jobs:
            cmds.scriptJob(kill=job_number)

        self.script_jobs = []

    def on_dag_object_created(self):
        """ 当dag中出现新物体时执行 """
        if len(cmds.ls(typ="light")) != len(self.light_items):
            print("New light created...")
            self.refresh_lights()

    def on_undo(self):
        """ ctrl+z时执行 """
        if len(cmds.ls(typ="light")) != len(self.light_items):
            print("Undo light created...")
            self.refresh_lights()

    def on_node_deleted(self):
        """ 节点删除时执行 """
        self.refresh_lights()

    def showEvent(self, event):
        """ 当打开窗口时执行 """
        self.refresh_lights()
        self.create_script_jobs()
    
    def closeEvent(self, event):
        """ 当关闭窗口时执行 """
        self.clear_lights()
        self.delete_script_jobs()

if __name__ == '__main__':
    cmds.file(new=True,f=True)
    cmds.file("D:/ZhangRuiChen/Pyside2ForMaya/light_test.ma",o=True,f=True)
    try:
        light_panel_dialog.close()
        light_panel_dialog.deleteLater()
    except:
        pass
    light_panel_dialog = LightPanel()
    light_panel_dialog.show()

```
<a name="ZzJ9v"></a>
## scriptJob
不知道scriptJob的话在这里看[https://www.yuque.com/quanmianxiaokangdelouwangzhiyu/pk4uzy/ucqe3u#Rk562](https://www.yuque.com/quanmianxiaokangdelouwangzhiyu/pk4uzy/ucqe3u#Rk562)<br />注册scriptJob：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671697160970-4d903cf0-97ad-438b-bd77-a3ad27d538c2.png#averageHue=%2334302c&clientId=ub7d727ca-d9ed-4&from=paste&height=382&id=u618a8281&originHeight=344&originWidth=1208&originalType=binary&ratio=1&rotation=0&showTitle=false&size=174235&status=done&style=none&taskId=udb8d8554-33f9-4a7f-9192-67c2b7e20eb&title=&width=1342.2222577789694)<br />取消注册scriptJob:<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671697289737-9aca734a-76ed-46bf-820c-849acdf948ba.png#averageHue=%23291d1d&clientId=ub7d727ca-d9ed-4&from=paste&height=146&id=u7a1ba4a6&originHeight=131&originWidth=885&originalType=binary&ratio=1&rotation=0&showTitle=false&size=49637&status=done&style=none&taskId=u8326d511-f58c-4ccb-be1f-125f8ed025a&title=&width=983.3333593827714)
<a name="TgmeX"></a>
# Docking
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1676368412774-62e89b75-050f-4042-ae72-172252a91f7c.png#averageHue=%230b0b0b&clientId=u0ed65455-fe7e-4&from=paste&height=575&id=u9137e5aa&originHeight=575&originWidth=1321&originalType=binary&ratio=1&rotation=0&showTitle=false&size=195907&status=done&style=none&taskId=u361a55fc-af62-47f2-bdfc-d0f90735912&title=&width=1321)
<a name="rVb0T"></a>
## maya的workspaces设置存放的位置
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1676428725500-72ba1326-f7bc-45b8-8e11-030d22cc2206.png#averageHue=%23f9f9f9&clientId=u0ed65455-fe7e-4&from=paste&height=174&id=ub49c11ba&originHeight=174&originWidth=537&originalType=binary&ratio=1&rotation=0&showTitle=false&size=48522&status=done&style=none&taskId=u0996483e-911b-4ff2-90b3-113dba0bc9b&title=&width=537)
<a name="Ooqxq"></a>
## mayaMixin.py
mayaMixin模块可以令我们更方便的创建可以停靠的窗口。<br />模块的路径为:C:\Program Files\Autodesk\Maya2018\Python\Lib\site-packages\maya\app\general\mayaMixin.py<br />其中模块使用的最重要的命令是cmds.workspaceControl<br />这里的会自动保存在工作区上面，关掉maya不会清除窗口内容。是有一个前置条件的，条件是这个模块是实实在在存在的文件，然后这个模块在maya的识别目录上面。<br />令其能够自动保存在工作区上面，实现的代码是：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1677225584722-63c8cec0-dea6-42fa-8dab-15951408b3b1.png#averageHue=%23ffffff&clientId=ueacdff51-fb88-4&from=paste&height=167&id=ua8a8de90&originHeight=150&originWidth=607&originalType=binary&ratio=0.8999999761581421&rotation=0&showTitle=false&size=19623&status=done&style=none&taskId=ua8a9886e-c8f0-4d96-8f6b-4e390b8bc36&title=&width=674.4444623111211)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1677225538425-50afbed0-ddf3-4d53-9d07-a61791ef937b.png#averageHue=%23ffffff&clientId=ueacdff51-fb88-4&from=paste&height=52&id=ub903c2e4&originHeight=47&originWidth=833&originalType=binary&ratio=0.8999999761581421&rotation=0&showTitle=false&size=11152&status=done&style=none&taskId=u534c562f-94d8-47fb-bf23-516bfb8f0b8&title=&width=925.5555800744052)<br />[Help](https://help.autodesk.com/view/MAYAUL/2018/ENU/?guid=__CommandsPython_index_html)
```python
# 配合MayaQWidgetDockableMixin模块制作 可以停靠在maya界面上的参考
# 特点：会自动保存在工作区上面，关掉maya不会清除窗口内容
# 开发时需要注意的点：在dock状态下不方便调试，开发时要在非dock状态以便调试
from PySide2 import QtWidgets
from shiboken2 import getCppPointer

from maya.app.general.mayaMixin import MayaQWidgetDockableMixin
from maya.OpenMayaUI import MQtUtil

import maya.cmds as cmds
# 多重继承中要把MayaQWidgetDockableMixin放在首位
class MyDockableButtonStatic(MayaQWidgetDockableMixin, QtWidgets.QPushButton):

    UI_NAME = "MyDockableButtonStatic" # 定义一个准确的UI_NAME使UI具有唯一性

    def __init__(self):
        super(MyDockableButtonStatic, self).__init__()

        self.setObjectName(self.UI_NAME)

        self.setWindowTitle("Dockable Window")
        self.setText("My Button")

        workspace_control_name = "{0}WorkspaceControl".format(self.UI_NAME)
        # 设置父级为工作区
        if cmds.workspaceControl(workspace_control_name, q=True, exists=True):
            workspace_control_ptr = long(MQtUtil.findControl(workspace_control_name))
            widget_ptr = long(getCppPointer(self)[0])

            MQtUtil.addWidgetToMayaLayout(widget_ptr, workspace_control_ptr)

if __name__ == "__main__":
    try:
        if button and button.parent():
            workspace_control_name = button.parent().objectName()

            if cmds.window(workspace_control_name, exists=True):
                cmds.deleteUI(workspace_control_name)
    except:
        pass

    button = MyDockableButtonStatic()

    ui_script = "from dockable_button_example import MyDockableButtonStatic\nbutton = MyDockableButtonStatic()"
    button.show(dockable=True, uiScript=ui_script) # 调用MayaQWidgetDockableMixin模块的show方法来使创建的窗口能够dock

```
<a name="OCpb5"></a>
## workspace_control.py
workspaceControl的介绍:<br />创建和管理用于在允许将窗口停靠和堆叠在一起的布局中托管窗口的小部件
```python
# 让UI成为workspaceControl的widget，这样就能够创建出可以dock的UI了
from PySide2 import  QtCore
from PySide2 import  QtWidgets
from shiboken2 import getCppPointer

import maya.OpenMayaUI as omui
import maya.cmds as cmds


class WorkspaceControl(object):
    """ 根据workspaceControl命令自定义的方便使用类 """
    
    def __init__(self,name):
        self.name = name
        self.widget = None
    
    def create(self, label, widget, ui_script=None):
        
        cmds.workspaceControl(self.name, label=label)

        if ui_script:
            cmds.workspaceControl(self.name, e=True, uiScript=ui_script)
        
        self.add_widget_to_layout(widget)
        self.set_visible(True)

    def restore(self, widget):
        """ 恢复widget的显示 """
        self.add_widget_to_layout(widget)
    
    def add_widget_to_layout(self, widget):
        """ 将widget添加到layout上 """
        if widget:
            self.widget = widget
            self.widget.setAttribute(QtCore.Qt.WA_DontCreateNativeAncestors) # 参考mayaMixin推荐的一个属性设置，意思是我们的widget会跟随父窗口属性改变，但是不要跟随父窗口属性改变的同时将祖先窗口改变。

            workspace_control_ptr = long(omui.MQtUtil.findControl(self.name)) # 得到workspaceControl的指针
            widget_ptr = long(getCppPointer(self.widget)[0]) # 得到widget的cpp指针

            omui.MQtUtil.addWidgetToMayaLayout(widget_ptr, workspace_control_ptr) # 令我们的widget属于maya布局

    def exists(self):
        """ 判断workspaceControl是否存在 """
        return cmds.workspaceControl(self.name, q=True, exists=True)
    
    def is_visible(self):
        """ 判断workspaceControl可视性 """
        return cmds.workspaceControl(self.name, q=True, visible=True)
    
    def set_visible(self, visible):
        """ 设置workspaceControl的可视性 """
        if visible:
            cmds.workspaceControl(self.name, e=True, restore=True)
        else:
            cmds.workspaceControl(self.name, e=True, visible=False)
    
    def set_label(self, label):
        """ 设置workspaceControl的标签 """
        cmds.workspaceControl(self.name, e=True, label=label)
    
    def is_floating(self):
        """ 判断workspaceControl是否浮动 """
        return cmds.workspaceControl(self.name, q=True, floating=True)

    def is_collapsed(self):
        """ 判断workspaceControl是否收缩 """
        return cmds.workspaceControl(self.name, q=True, collapse=True)
    

class SampleUI(QtWidgets.QWidget):

    WINDOW_TITLE = "Sample UI"
    UI_NAME = "SampleUI"

    ui_instance = None

    # 创建一个类方法，方便外界调用来显示可以dock的UI,如果SampleUI存在就显示它，不存在就创建
    @classmethod
    def display(cls):
        if cls.ui_instance:
            cls.ui_instance.show_workspace_control()
        else:
            cls.ui_instance = SampleUI()

    @classmethod
    def get_workspace_control_name(cls):
        """ 设置控件对应的workspaceControl名字 """
        return "{0}WorkspaceControl".format(cls.UI_NAME)
    

    def __init__(self):
        super(SampleUI, self).__init__()

        self.setObjectName(self.__class__.UI_NAME)
        self.setMinimumSize(200, 100)

        self.create_widget()
        self.create_layout()
        self.create_connections()
        self.create_workspace_control()
    
    def create_widget(self):
        self.apply_button = QtWidgets.QPushButton("Apply")
    
    def create_layout(self):
        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2)
        main_layout.addStretch()
        main_layout.addWidget(self.apply_button)
    
    def create_connections(self):
        self.apply_button.clicked.connect(self.on_clicked)
    
    def create_workspace_control(self):
        """ 创建workspaceControl """
        self.workspace_control_instance = WorkspaceControl(self.get_workspace_control_name())
        if self.workspace_control_instance.exists():
            self.workspace_control_instance.restore(self) # 如果workspace_control已经存在了那么就将它显示出来
        else:
            self.workspace_control_instance.create(self.WINDOW_TITLE, self, ui_script="from workspace_control import SampleUI\nSampleUI.display()")
    
    def show_workspace_control(self):
        self.workspace_control_instance.set_visible(True)
    
    def on_clicked(self):
        print("Button Clicked")

    def showEvent(self, e):
        """ 设置窗口float时以及dock时对应的标题 """
        if self.workspace_control_instance.is_floating():
            self.workspace_control_instance.set_label("Floating Window")
        else:
            self.workspace_control_instance.set_label("Docked Window")



if __name__ == "__main__":

    workspace_control_name = SampleUI.get_workspace_control_name()
    if cmds.window(workspace_control_name, exists=True):
        cmds.deleteUI(workspace_control_name)

    # 这串代码可以使UI在dock的同时能够通过更改UI的代码来更新界面
    # try:
    #     sample_ui.setParent(None)
    #     sample_ui.deleteLater()
    # except:
    #     pass
    
    sample_ui = SampleUI()
    sample_ui.show()
```
<a name="mBEs1"></a>
## 将workspace_control作为模块导入使用的步骤
<a name="Q6A1e"></a>
### workspace_control主要修改区域：
新增类方法<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1677206784328-27769875-35d3-4793-a1cd-9f5797845ec5.png#averageHue=%23201f1f&clientId=u642778c3-94fb-4&from=paste&height=241&id=u312e1185&originHeight=241&originWidth=1027&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27884&status=done&style=none&taskId=u1c14e281-ceaa-4e91-afcb-0e4981bc2f0&title=&width=1027)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1677206827356-bdbb4405-ed33-4df9-bd50-6b9969887555.png#averageHue=%23231f1e&clientId=u642778c3-94fb-4&from=paste&height=189&id=ue63728d9&originHeight=189&originWidth=1212&originalType=binary&ratio=1&rotation=0&showTitle=false&size=37526&status=done&style=none&taskId=u1cee2a55-4a75-43ba-ab90-f9a252f71ba&title=&width=1212)
```python
from PySide2 import QtCore
from PySide2 import QtWidgets
from shiboken2 import getCppPointer

import maya.OpenMayaUI as omui
import maya.cmds as cmds


class WorkspaceControl(object):

    def __init__(self, name):
        self.name = name
        self.widget = None

    def create(self, label, widget, ui_script=None):

        cmds.workspaceControl(self.name, label=label)

        if ui_script:
            cmds.workspaceControl(self.name, e=True, uiScript=ui_script)

        self.add_widget_to_layout(widget)
        self.set_visible(True)

    def restore(self, widget):
        self.add_widget_to_layout(widget)

    def add_widget_to_layout(self, widget):
        if widget:
            self.widget = widget
            self.widget.setAttribute(QtCore.Qt.WA_DontCreateNativeAncestors)

            workspace_control_ptr = long(omui.MQtUtil.findControl(self.name))
            widget_ptr = long(getCppPointer(self.widget)[0])

            omui.MQtUtil.addWidgetToMayaLayout(widget_ptr, workspace_control_ptr)

    def exists(self):
        return cmds.workspaceControl(self.name, q=True, exists=True)

    def is_visible(self):
        return cmds.workspaceControl(self.name, q=True, visible=True)

    def set_visible(self, visible):
        if visible:
            cmds.workspaceControl(self.name, e=True, restore=True)
        else:
            cmds.workspaceControl(self.name, e=True, visible=False)

    def set_label(self, label):
        cmds.workspaceControl(self.name, e=True, label=label)

    def is_floating(self):
        return cmds.workspaceControl(self.name, q=True, floating=True)

    def is_collapsed(self):
        return cmds.workspaceControl(self.name, q=True, collapse=True)



class DockableUI(QtWidgets.QWidget):

    WINDOW_TITLE = "DockableUI"

    ui_instance = None


    @classmethod
    def display(cls):
        if cls.ui_instance:
            cls.ui_instance.show_workspace_control()
        else:
            cls.ui_instance = cls()

    @classmethod
    def get_workspace_control_name(cls):
        return "{0}WorkspaceControl".format(cls.__name__)

    @classmethod
    def get_ui_script(cls):
        module_name = cls.__module__
        if module_name == "__main__":
            module_name = cls.module_name_override

        ui_script = "from {0} import {1}\n{1}.display()".format(module_name, cls.__name__)
        return ui_script


    def __init__(self):
        super(DockableUI, self).__init__()

        self.setObjectName(self.__class__.__name__)

        self.create_actions()
        self.create_widgets()
        self.create_layout()
        self.create_connections()
        self.create_workspace_control()

    def create_actions(self):
        pass

    def create_widgets(self):
        pass

    def create_layout(self):
        pass

    def create_connections(self):
        pass

    def create_workspace_control(self):
        self.workspace_control_instance = WorkspaceControl(self.get_workspace_control_name())
        if self.workspace_control_instance.exists():
            self.workspace_control_instance.restore(self)
        else:
            self.workspace_control_instance.create(self.WINDOW_TITLE, self, ui_script=self.get_ui_script())

    def show_workspace_control(self):
        self.workspace_control_instance.set_visible(True)




```
<a name="nmdWc"></a>
### dockable_outliner与原版的区别：

![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1677207029301-874922a2-f359-435d-98d9-0cf9bf68c815.png#averageHue=%23f9f0ef&clientId=u642778c3-94fb-4&from=paste&height=570&id=ub48cbe34&originHeight=570&originWidth=1597&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63586&status=done&style=none&taskId=ufb8c8f75-f8ce-4b61-aa78-830ce3efeb1&title=&width=1597)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1677207062777-560665cd-7aa2-4c38-a2fb-e418c1790104.png#averageHue=%23f9e7e7&clientId=u642778c3-94fb-4&from=paste&height=221&id=u25f2a923&originHeight=221&originWidth=1607&originalType=binary&ratio=1&rotation=0&showTitle=false&size=17522&status=done&style=none&taskId=u4387a327-dd89-42da-abd6-615d531c8f8&title=&width=1607)
```python
from functools import partial


from PySide2 import QtCore
from PySide2 import QtGui
from PySide2 import QtWidgets


import maya.cmds as cmds


from workspace_control import DockableUI



class DockableOutliner(DockableUI):


    WINDOW_TITLE = "Dockable Outliner"


    def __init__(self):
        super(DockableOutliner, self).__init__()


        self.setMinimumWidth(300)
        self.setContextMenuPolicy(QtCore.Qt.CustomContextMenu)
        self.customContextMenuRequested.connect(self.show_context_menu)


        self.transform_icon = QtGui.QIcon(":transform.svg")
        self.camera_icon = QtGui.QIcon(":Camera.png")
        self.mesh_icon = QtGui.QIcon(":mesh.svg")


        self.script_job_number = -1


        self.refresh_tree_widget()


    def create_actions(self):
        self.about_action = QtWidgets.QAction("About", self)


        self.display_shape_action = QtWidgets.QAction("Shapes", self)
        self.display_shape_action.setCheckable(True)
        self.display_shape_action.setChecked(True)
        self.display_shape_action.setShortcut(QtGui.QKeySequence("Ctrl+Shift+H"))


    def create_widgets(self):
        self.menu_bar = QtWidgets.QMenuBar()
        display_menu = self.menu_bar.addMenu("Display")
        display_menu.addAction(self.display_shape_action)
        help_menu = self.menu_bar.addMenu("Help")
        help_menu.addAction(self.about_action)


        self.tree_widget = QtWidgets.QTreeWidget()
        self.tree_widget.setSelectionMode(QtWidgets.QAbstractItemView.ExtendedSelection)
        self.tree_widget.setHeaderHidden(True)
        # header = self.tree_widget.headerItem()
        # header.setText(0, "Column 0 Text")


        self.refresh_btn = QtWidgets.QPushButton("Refresh")


    def create_layout(self):
        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.refresh_btn)


        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2)
        main_layout.setSpacing(2)
        main_layout.setMenuBar(self.menu_bar)
        main_layout.addWidget(self.tree_widget)
        main_layout.addLayout(button_layout)


    def create_connections(self):
        self.about_action.triggered.connect(self.about)
        self.display_shape_action.toggled.connect(self.set_shape_nodes_visible)


        self.tree_widget.itemCollapsed.connect(self.update_icon)
        self.tree_widget.itemExpanded.connect(self.update_icon)
        self.tree_widget.itemSelectionChanged.connect(self.select_items)


        self.refresh_btn.clicked.connect(self.refresh_tree_widget)


    def refresh_tree_widget(self):
        self.shape_nodes = cmds.ls(shapes=True)


        self.tree_widget.clear()


        top_level_object_names = cmds.ls(assemblies=True)
        for name in top_level_object_names:
            item = self.create_item(name)
            self.tree_widget.addTopLevelItem(item)


        self.update_selection()


    def create_item(self, name):
        item = QtWidgets.QTreeWidgetItem([name])
        self.add_children(item)
        self.update_icon(item)


        is_shape = name in self.shape_nodes
        item.setData(0, QtCore.Qt.UserRole, is_shape)


        return item


    def add_children(self, item):
        children = cmds.listRelatives(item.text(0), children=True)
        if children:
            for child in children:
                child_item = self.create_item(child)
                item.addChild(child_item)


    def update_icon(self, item):
        object_type = ""


        if item.isExpanded():
            object_type = "transform"
        else:
            child_count = item.childCount()
            if child_count == 0:
                object_type = cmds.objectType(item.text(0))
            elif child_count == 1:
                child_item = item.child(0)
                object_type = cmds.objectType(child_item.text(0))
            else:
                object_type = "transform"


        if object_type == "transform":
            item.setIcon(0, self.transform_icon)
        elif object_type == "camera":
            item.setIcon(0, self.camera_icon)
        elif object_type == "mesh":
            item.setIcon(0, self.mesh_icon)


    def select_items(self):
        items = self.tree_widget.selectedItems()
        names = []
        for item in items:
            names.append(item.text(0))


        cmds.select(names, replace=True)


    def about(self):
        QtWidgets.QMessageBox.about(self, "About Simple Outliner", "Add About Text Here")


    def set_shape_nodes_visible(self, visible):
        iterator = QtWidgets.QTreeWidgetItemIterator(self.tree_widget)
        while iterator.value():
            item = iterator.value()
            is_shape = item.data(0, QtCore.Qt.UserRole)
            if is_shape:
                item.setHidden(not visible)


            iterator += 1


    def show_context_menu(self, point):
        context_menu = QtWidgets.QMenu()
        context_menu.addAction(self.display_shape_action)
        context_menu.addSeparator()
        context_menu.addAction(self.about_action)


        context_menu.exec_(self.mapToGlobal(point))


    def update_selection(self):
        selection = cmds.ls(selection=True)


        iterator = QtWidgets.QTreeWidgetItemIterator(self.tree_widget)
        while iterator.value():
            item = iterator.value()
            is_selected = item.text(0) in selection
            item.setSelected(is_selected)


            iterator += 1


    def set_script_job_enabled(self, enabled):
        if enabled and self.script_job_number < 0:
            self.script_job_number = cmds.scriptJob(event=["SelectionChanged", partial(self.update_selection)], protected=True)
        elif not enabled and self.script_job_number >= 0:
            cmds.scriptJob(kill=self.script_job_number, force=True)
            self.script_job_number = -1


    def showEvent(self, e):
        super(DockableOutliner, self).showEvent(e)
        self.set_script_job_enabled(True)


    def closeEvent(self, e):
        if isinstance(self, DockableOutliner):
            super(DockableOutliner, self).closeEvent(e)
            self.set_script_job_enabled(False)



if __name__ == "__main__":


    workspace_control_name = DockableOutliner.get_workspace_control_name()
    if cmds.window(workspace_control_name, exists=True):
        cmds.deleteUI(workspace_control_name)


    DockableOutliner.module_name_override = "dockable_outliner"
    test_dialog = DockableOutliner()
```
<a name="t4Cku"></a>
# Qt事件
<a name="TNHWF"></a>
## 事件介绍
<a name="ENkHI"></a>
### 事件系统
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673245476361-c19b8bda-147b-4b63-b911-2c617fab571b.png#averageHue=%230c0c0c&clientId=u07b614fd-bd46-4&from=paste&height=679&id=u290a994e&originHeight=611&originWidth=1467&originalType=binary&ratio=1&rotation=0&showTitle=false&size=296520&status=done&style=none&taskId=ucf5758dc-3e02-4f6a-aabb-391e65599eb&title=&width=1630.0000431802548)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673245481192-e407fce6-d96f-4dbb-826e-2700eed58b08.png#averageHue=%23100f0e&clientId=u07b614fd-bd46-4&from=paste&height=533&id=u9e628b49&originHeight=480&originWidth=1061&originalType=binary&ratio=1&rotation=0&showTitle=false&size=67608&status=done&style=none&taskId=u26ab3981-a2a1-454a-af85-fe10b864a6f&title=&width=1178.88892011878)
<a name="Miv2S"></a>
### 事件驱动VS实时
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673246046841-93f5eafd-7c7b-4b50-b79b-75d9b3819b6a.png#averageHue=%230b0b0b&clientId=u07b614fd-bd46-4&from=paste&height=832&id=uafbddc9f&originHeight=749&originWidth=1560&originalType=binary&ratio=1&rotation=0&showTitle=false&size=366420&status=done&style=none&taskId=udd76986b-f221-4f4b-b16e-72f9b1d9c34&title=&width=1733.3333792509868)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673246088391-e3b83926-7b34-40de-a0ad-84bf9428a48a.png#averageHue=%230e0d0c&clientId=u07b614fd-bd46-4&from=paste&height=613&id=u1524d774&originHeight=552&originWidth=1512&originalType=binary&ratio=1&rotation=0&showTitle=false&size=87238&status=done&style=none&taskId=ud5e95d16-6dca-46a5-9155-c5151bff665&title=&width=1680.0000445048026)
<a name="C3KQI"></a>
### Qt事件
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673246124739-710bc149-89f6-4a35-a955-089bb7e468ed.png#averageHue=%23080808&clientId=u07b614fd-bd46-4&from=paste&height=787&id=u7d60f664&originHeight=708&originWidth=1586&originalType=binary&ratio=1&rotation=0&showTitle=false&size=274694&status=done&style=none&taskId=u7403b032-62a3-4e27-b7d9-12e5fd26a66&title=&width=1762.22226890517)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673246139637-502905e8-36c7-4804-90e8-3a07a874ebe1.png#averageHue=%230b0a09&clientId=u07b614fd-bd46-4&from=paste&height=638&id=ued172028&originHeight=574&originWidth=1077&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63418&status=done&style=none&taskId=u01787e55-a086-430c-8775-795e6e142f8&title=&width=1196.6666983675082)
<a name="IQQkl"></a>
### 事件处理
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673246166933-d98416fc-5646-4c61-b821-a40aafcda3bf.png#averageHue=%230a0a0a&clientId=u07b614fd-bd46-4&from=paste&height=780&id=u3142b467&originHeight=702&originWidth=1624&originalType=binary&ratio=1&rotation=0&showTitle=false&size=350911&status=done&style=none&taskId=u17e17f0c-3953-4dc1-825a-4b72eea3c04&title=&width=1804.444492245899)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673246180926-469e0cbf-b90c-4b60-9766-4638289cef72.png#averageHue=%23090908&clientId=u07b614fd-bd46-4&from=paste&height=579&id=u8b97687c&originHeight=521&originWidth=1598&originalType=binary&ratio=1&rotation=0&showTitle=false&size=69519&status=done&style=none&taskId=u68fcd36c-086c-422f-a635-d9b3036c141&title=&width=1775.555602591716)
<a name="DWTYd"></a>
### 事件过滤
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673246220310-155f22c4-3bc3-4967-bf62-9980f0ce6665.png#averageHue=%230b0b0b&clientId=u07b614fd-bd46-4&from=paste&height=543&id=u9d714b1b&originHeight=489&originWidth=1574&originalType=binary&ratio=1&rotation=0&showTitle=false&size=232756&status=done&style=none&taskId=uf7edba98-7884-4862-99c9-f020cc1bb21&title=&width=1748.8889352186238)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673246260732-b5d7bcd7-19f6-46ac-b103-4a72c450d97a.png#averageHue=%230d0c0b&clientId=u07b614fd-bd46-4&from=paste&height=390&id=u94cec4c9&originHeight=312&originWidth=1266&originalType=binary&ratio=1&rotation=0&showTitle=false&size=39026&status=done&style=none&taskId=ud6a3f8ef-4721-4be4-9711-e7d89090604&title=&width=1582.4999764189129)
<a name="KYXAz"></a>
## 举例
<a name="zdhdh"></a>
### KeyPress事件处理
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673247679167-269b96f7-fd7d-447f-9332-8ae9a1310fce.png#averageHue=%23464645&clientId=u07b614fd-bd46-4&from=paste&height=285&id=ufb2910ab&originHeight=228&originWidth=302&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3096&status=done&style=none&taskId=uc597ac55-cdd1-47db-a24e-bafbaf9e786&title=&width=377.4999943748117)
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.cmds as cmds



def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class CustomPlainTextEdit(QtWidgets.QPlainTextEdit):
    """ 输入文本编辑器 """
    def __init__(self, parent=None):
        super(CustomPlainTextEdit, self).__init__(parent)
    
    def keyPressEvent(self, key_event):
        """ 重载keyPressEvent方法 """
        # print("Key Pressed: {0}".format(key_event.text()))


        ctrl = key_event.modifiers() == QtCore.Qt.ControlModifier # ctrl为布尔值，代表ctrl键是否处于按下的状态
        # print("Control Modifiers: {0}".format(ctrl))


        shift = key_event.modifiers() == QtCore.Qt.ShiftModifier
        # print("Shift Modifiers: {0}".format(shift))


        alt = key_event.modifiers() == QtCore.Qt.AltModifier
        # print("Alt Modifiers: {0}".format(alt))


        ctrl_alt = key_event.modifiers() == (QtCore.Qt.ControlModifier | QtCore.Qt.AltModifier)
        # print("Ctrl+Alt Modifiers: {0}".format(ctrl_alt))


        # if shift:
        #     return


        key = key_event.key()


        if key == QtCore.Qt.Key_Return or key == QtCore.Qt.Key_Enter:
            """ Key_Return代表中间的回车键 Key_Enter代表右边的回车键 """
            if ctrl: # 如果是ctrl+enter
                print("Execute Code")
            elif ctrl_alt: # 如果是ctrl+alt+enter
                print("Execute Line")
                return
        
        super(CustomPlainTextEdit, self).keyPressEvent(key_event) # 重载QtWidgets.QPlainTextEdit的keyPressEvent方法的同时，不影响keyPressEvent的功能


class KeyPressExample(QtWidgets.QDialog):


    WINDOW_TITLE = "Keypress Example"


    def __init__(self, parent=maya_main_window()):
        super(KeyPressExample, self).__init__(parent)
        
        self.setWindowTitle(self.WINDOW_TITLE)
        self.setMinimumSize(300, 80)
        self.setWindowFlags(QtCore.Qt.WindowType.Window)


        self.create_widgets()
        self.create_layouts()


    def create_widgets(self):
        """ 控件 """
        self.plain_text = CustomPlainTextEdit()


    def create_layouts(self):
        """ 布局 """
        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2)
        main_layout.addWidget(self.plain_text)




if __name__ == '__main__':
    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    
    ui = KeyPressExample()
    ui.show()
```
<a name="Rwerv"></a>
### Mouse事件处理
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673251794443-0628b284-6f6f-49c8-b3e0-5dec7bb5f149.png#averageHue=%23504f4f&clientId=ud572c1dd-7c66-4&from=paste&height=540&id=u5a5d4291&originHeight=432&originWidth=402&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3716&status=done&style=none&taskId=u36be2f99-c435-4d76-a543-e34e857c7e5&title=&width=502.4999925121666)
```python
# coding:utf-8
from PySide2 import QtCore
from PySide2 import QtWidgets
from PySide2 import QtGui
from shiboken2 import wrapInstance
import maya.OpenMayaUI as omui
import maya.cmds as cmds


def maya_main_window():
    main_window_ptr = omui.MQtUtil.mainWindow()
    return wrapInstance(long(main_window_ptr), QtWidgets.QWidget)


class MoveableWidget(QtWidgets.QWidget):

    def __init__(self, x, y, width, height, color, parent=None):
        super(MoveableWidget, self).__init__(parent)

        self.setFixedSize(width, height)
        self.move(x, y)

        self.color = color
        self.original_color = color

        self.move_enabled = False
    
    def mousePressEvent(self, mouse_event):
        """ 鼠标点击时的事件 """
        print("Mouse Button Pressed")

        if mouse_event.button() == QtCore.Qt.LeftButton:
            self.initial_pos = self.pos()
            self.global_pos = mouse_event.globalPos()

            self.move_enabled = True # 点击时可以移动widget
    
    def mouseReleaseEvent(self, mouse_event):
        """ 鼠标释放时的事件 """
        print("Mouse Button Released")

        if self.move_enabled:
            self.move_enabled = False # 松开后不能移动widget
    
    def mouseDoubleClickEvent(self, mouse_event):
        """ 鼠标双击后改变颜色 """
        print("Mouse Double-Click")

        if self.color == self.original_color:
            self.color = QtCore.Qt.yellow
        else:
            self.color = self.original_color

        self.update() # 更新颜色
    
    def mouseMoveEvent(self, mouse_event):
        """ 鼠标点击并移动时widget也移动 """
        print("Mouse Move")

        if self.move_enabled:
            diff = mouse_event.globalPos() - self.global_pos
            self.move(self.initial_pos + diff)
    
    def paintEvent(self, paint_event):
        """ 绘制填充矩形 """
        painter = QtGui.QPainter(self)
        painter.fillRect(paint_event.rect(), self.color)

class MouseEventExample(QtWidgets.QDialog):

    WINDOW_TITLE = "MAYA-2018"

    def __init__(self, parent=maya_main_window()):
        super(MouseEventExample, self).__init__(parent)
        
        self.setWindowTitle(self.WINDOW_TITLE)
        self.setMinimumSize(400, 400)
        self.setWindowFlags(QtCore.Qt.WindowType.Window)

        self.create_widgets()
        self.create_layouts()

    def create_widgets(self):
        """ 控件 """
        self.red_widget = MoveableWidget(100, 100, 24, 24, QtCore.Qt.red, self)
        self.blue_widget = MoveableWidget(300, 300, 24, 24, QtCore.Qt.blue, self)

    def create_layouts(self):
        """ 布局 """
        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.setContentsMargins(2, 2, 2, 2)

if __name__ == '__main__':

    try:
        ui.close()
        ui.deleteLater()
    except:
        pass
    ui = MouseEventExample()
    ui.show()

```
<a name="Hk9pA"></a>
# Drag and Drop

