---
title: pyside2的一些归纳
tags: PySide2
categories: PySide2
abbrlink: 5c6089d
date: 2023-10-07 11:45:00
---

# 各种文件对话框
**选择文件:**
```python
file_name,filetype = QFileDialog.getOpenFileName(self,"这里是对话框的标题","这里文件对话框的起始路径","所有文件(*);;文本文件(*.txt);;maya文件(*.ma)")
if not file_name:
    return
```
**选择多个文件:**
```python
files,filetype = QFileDialog.getOpenFileNames(self,"对话框标题","对话框起始路径","所有文件(*);;文本文件(*.txt);;maya文件(*.ma)")
if len(files) == 0:
    return
```
**保存文件:**
```python
file_name,filetype = QFileDialog.getSaveFileName(self,"对话框标题","对话框起始路径","所有文件(*);;文本文件(*.txt);;maya文件(*.ma)")
if not file_name:
    return
```
**选择文件夹:**
```python
folder_name = QFileDialog.getExistingDirectory(self,"对话框标题","对话框起始路径")
if not folder_name:
    return
```

---
# 各种信息对话框
**提示对话框:**
```python
reply = QMessageBox.infomation(self,"对话框标题","对话框内容",QMessageBox.Ok | QMessageBox.Close, QMessageBox.Close)
if reply == QMessageBox.Ok:
    print("选择了Ok")
else:
    print("选择了Close")
```
**询问对话框:**
```python
reply = QMessageBox.question(self,"对话框标题","对话框内容",QMessageBox.Yes | QMessageBox.No | QMessageBox.Cancel, QMessageBox.No)
```
**警告对话框:**
```python
reply = QMessageBox.warning(self,"对话框标题","对话框内容",QMessageBox.Save | QMessageBox.Discard | QMessageBox.Cancel, QMessageBox.Save)
```
**错误对话框:**
```python
reply = QMessageBox.critical(self,"对话框标题","对话框内容",QMessageBox.Retry | QMessageBox.About | QMessageBox.Ignore, QMessageBox.Retry)
```
**自定义对话框**
```python
message_box = QMessageBox(QMessageBox.NoIcon,"对话框标题","对话框内容")
message_box.setIconPixmap(QPixmap("这里填图片路径"))
save_btn = message_box.addButton("保存",QMessageBox.AcceptRole)
cancel_btn = message_box.addButton("取消",QMessageBox.RejectRole)
no_save_btn = message_box.addButton("不保存",QMessageBox.DestructiveRole)
cb = QCheckBox("自定义的控件")
message_box.setCheckBox(cb)
message_box.setDetailedText('通过点击ShowDetails按钮可以展开的详细信息')
reply = message_box.exec()
```

---
# 添加分割线
![Alt text](image.png)
```python
self.line1 = QFrame()
self.line1.setFrameShape(QFrame.HLine) # 横线，竖线是QFrame.VLine
self.line1.setFrameShadow(QFrame.Sunken) # 设置阴影
```

---
# 添加GroupBox(将不同模块区分开)
![Alt text](image-1.png)

---
# 设置ListWidget的选择模式
单选模式：setSelectionMode(QAbstractItemView.SingleSelection)
多选模式：setSelectionMode(QAbstractItemView.ExtendedSelection)

# 给QListWidget的item添加自定义右键上下文菜单并支持往里面拖入文件添加item的例子

代码解析:
1. self.customContextMenuRequested.connect(self.show_context_menu)定义了item右键时显示的上下文菜单,在调用show_context_menu方法时会自动传入一个参数,这个参数是item的位置信息,因此就可以通过这个位置信息定义上下文菜单的位置
2. set_drop_enabled,dragEnterEvent,dragMoveEvent,dropEvent通过重写父类的方法来支持拖拽,并设置了拖入时执行的方法,其中dragMoveEvent函数内容虽然是pass,但是不能够不写,不然不行.
3. show_error_log函数之所以这样写,是因为我在使用item的同时我会通过item的setData的方法来对item写数据,其中error_role = Qt.UserRole + 1中的Qt.UserRole可以理解为Qt提供的一个固定的数值,它是一个整数值,方便用在使用item的setData方法时将数据放到item的哪个地方,因为放入item的数据不一定就放一个,可能会放很多个.因此我这里就以Qt.UserRole + 1当作起始点,然后通过while循环找到item对应的所有数据,有了数据以后就可以显示出来数据内容了.

```python
class DropListWidget(QListWidget):
    WIDGET_ITEMS = []

    def __init__(self, parent=None):
        super(DropListWidget, self).__init__(parent)
        self.setContextMenuPolicy(Qt.CustomContextMenu)
        self.customContextMenuRequested.connect(self.show_context_menu)        

    def set_drop_enabled(self, enabled):
        self.setAcceptDrops(enabled)

    def dragEnterEvent(self, drag_event):

        mime_data = drag_event.mimeData()
        if mime_data.hasText() or mime_data.hasUrls():
            drag_event.acceptProposedAction()

    def dragMoveEvent(self, drag_event):
        pass

    def dropEvent(self, drop_event):
        mime_data = drop_event.mimeData()
        urls = mime_data.urls()
        paths = [url.toLocalFile() for url in urls if (url.toLocalFile().endswith(".ma") or os.path.isdir(url.toLocalFile()))]
        paths.sort()
        icon = QIcon(os.path.join(SCRIPT_DIR,"icons","add.png"))
        for path in paths:
            item = QListWidgetItem(icon,path)
            self.addItem(item)
            self.WIDGET_ITEMS.append(item)
        drop_event.acceptProposedAction()

    def show_context_menu(self, pos):
        """ 让列表项能够右键显示菜单的内容 """
        selected_item = self.itemAt(pos)
        if selected_item:
            load_location_action = QAction(u"进入本地路径",self)
            load_location_action.triggered.connect(lambda:self.enter_local_path(selected_item))
            error_log_action = QAction(u"列出检查错误原因",self)
            error_log_action.triggered.connect(lambda: self.show_error_log(selected_item))
            context_menu = QMenu()
            context_menu.addAction(load_location_action)
            context_menu.addSeparator()  # 分割线
            context_menu.addAction(error_log_action)

            context_menu.exec_(self.mapToGlobal(pos))  # 右键显示菜单
    
    def show_error_log(self,item):
        """ 显示检查发现的错误项 """
        error_roles = []
        error_role = Qt.UserRole + 1
        while error_role:
            if item.data(error_role):
                error_roles.append(error_role)
                error_role += 1
            else:
                break
        if error_roles:
            error_logs = []
            for role in error_roles:
                error_logs.append(item.data(role))
            message_box = QMessageBox(self)
            message_box.setWindowTitle(u'错误项')
            err_log = "\n".join(error_logs)
            message_box.setText(err_log)
            message_box.show()
    
    def enter_local_path(self,item):
        """ 如果item对应路径是文件夹就进入文件夹,如果是路径就进入路径对应的文件目录 """
        item_path = item.text()
        if os.path.isfile(item_path):
            local_path = os.path.dirname(item_path)
        else:
            local_path = item_path
        QDesktopServices.openUrl(QUrl.fromLocalFile(local_path))
```