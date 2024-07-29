---
title: PyQt5
tags: PyQt5
categories: PySide2
abbrlink: 9898eb96
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

<a name="P2iGF"></a>
## 
<a name="yeGPb"></a>
# PyQt5的使用
<a name="WwrnW"></a>
## 布局
<a name="YWCW5"></a>
### 绝对布局
直接通过QLabel指定self使标签出现在窗口上<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648020085545-8b33a6e6-2b54-4bfd-b2f3-cf5d9fba0bea.png#clientId=u61b28784-2765-4&from=paste&height=275&id=aPuBS&originHeight=275&originWidth=569&originalType=binary&ratio=1&rotation=0&showTitle=false&size=132399&status=done&style=none&taskId=u95d47597-04a7-4d48-9d1e-d2905315e87&title=&width=569)
<a name="XMKwb"></a>
### 水平盒布局QHBoxLayout
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648020264952-bda1ccfb-49f8-43a5-b7ac-90782f5d6570.png#clientId=u61b28784-2765-4&from=paste&height=436&id=Baqjx&originHeight=436&originWidth=909&originalType=binary&ratio=1&rotation=0&showTitle=false&size=259508&status=done&style=none&taskId=u33736d8e-5337-4863-a962-edbfc6aecb5&title=&width=909)<br />可以使用布局对象的setSpacing()方法控制控件之间的间距<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648020742456-cfd50efc-6410-4f76-a43f-794c7f0cfa6d.png#clientId=u61b28784-2765-4&from=paste&height=75&id=YLoxR&originHeight=75&originWidth=600&originalType=binary&ratio=1&rotation=0&showTitle=false&size=62351&status=done&style=none&taskId=u33ff5b2e-ed6d-4da1-9e0d-6c774eee625&title=&width=600)
<a name="TUasf"></a>
### 设置控件的对齐方式
可以通过在addWidget中增加两个参数改变伸缩量和对齐方式<br />第一个参数为按钮控件，第二个参数为伸缩量，第三个为对齐方式<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648020570838-975db8b9-cbc0-4d10-801e-3fff68015656.png#clientId=u61b28784-2765-4&from=paste&height=685&id=UwLIq&originHeight=685&originWidth=1275&originalType=binary&ratio=1&rotation=0&showTitle=false&size=305221&status=done&style=none&taskId=u4fc78ca0-fd60-465b-9369-41ad941f2df&title=&width=1275)

<a name="KlYMT"></a>
### 垂直盒布局QVBoxLayout
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648021137561-504065d9-587f-456a-ae05-fdeda6652158.png#clientId=u61b28784-2765-4&from=paste&height=387&id=ySmL4&originHeight=387&originWidth=409&originalType=binary&ratio=1&rotation=0&showTitle=false&size=28231&status=done&style=none&taskId=u4530b144-eef7-4d72-a535-9888f3810c1&title=&width=409)
<a name="PGNgd"></a>
### 设置布局的伸缩量addStretch
设置布局伸缩量有两种方法，第一种：添加控件时设置<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648176606518-d0b43209-6b94-42f7-8f0b-64ffd37196ee.png#clientId=u3f1ac442-2738-4&from=paste&height=56&id=xYoof&originHeight=56&originWidth=589&originalType=binary&ratio=1&rotation=0&showTitle=false&size=69800&status=done&style=none&taskId=ud34a6a9e-1d4d-4def-9244-48ef730814c&title=&width=589)<br />第二种：addStretch
```python
import sys
from PyQt5.QtWidgets import *


class Stretch(QWidget):
    def __init__(self):
        super(Stretch, self).__init__()
        self.setWindowTitle('设置伸缩量')
        btn1 = QPushButton('按钮1')
        btn2 = QPushButton('按钮2')
        btn3 = QPushButton('按钮3')
        layout = QHBoxLayout()
        layout.addStretch(1)  # 设置伸缩量
        layout.addWidget(btn1)  # 设置1个伸缩量后添加一个按钮
        layout.addStretch(2)
        layout.addWidget(btn2)  # 伸缩量为2
        layout.addStretch(3)
        layout.addWidget(btn3)  # 伸缩量为3
        self.setLayout(layout)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = Stretch()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648204691401-d31e56f9-c9da-41fa-b091-d21788d184ed.png#clientId=uddd2ac66-43c5-4&from=paste&height=329&id=Dv2rj&originHeight=329&originWidth=946&originalType=binary&ratio=1&rotation=0&showTitle=false&size=15910&status=done&style=none&taskId=u1819aec5-564b-493a-9da7-1f21f987ce6&title=&width=946)
```python
import sys
from PyQt5.QtWidgets import *


class Stretch(QWidget):
    def __init__(self):
        super(Stretch, self).__init__()
        self.setWindowTitle('设置伸缩量')
        self.resize(800,100)
        btn1 = QPushButton('按钮1')
        btn2 = QPushButton('按钮2')
        btn3 = QPushButton('按钮3')
        btn4 = QPushButton('按钮4')
        btn5 = QPushButton('按钮5')
        layout = QHBoxLayout()
        layout.addStretch(0)  # 设置伸缩量
        layout.addWidget(btn1)  # 设置1个伸缩量后添加一个按钮
        layout.addStretch(1)  # 再设置一个伸缩量
        #  再次设置伸缩量后添加4个按钮
        layout.addWidget(btn2)
        layout.addWidget(btn3)
        layout.addWidget(btn4)
        layout.addWidget(btn5)
        btnOK = QPushButton('确定')
        btnCancel = QPushButton('取消')
        layout.addStretch(1)
        layout.addWidget(btnOK)
        layout.addWidget(btnCancel)
        self.setLayout(layout)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = Stretch()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648205801054-3dd3c46d-3cd2-4db7-80d9-ed7f101a5e16.png#clientId=uddd2ac66-43c5-4&from=paste&height=139&id=q8gmo&originHeight=139&originWidth=816&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8582&status=done&style=none&taskId=u1e27fcee-305d-4c59-a409-ad129ba9420&title=&width=816)
<a name="rJfxx"></a>
### 让按钮永远在窗口的右下角
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtCore import Qt


class RightBottomButton(QWidget):
    def __init__(self):
        super(RightBottomButton, self).__init__()
        self.setWindowTitle("让按钮永远在右下角")
        self.resize(400, 300)
        okButton = QPushButton("确定")
        cancelButton = QPushButton('取消')
        hbox = QHBoxLayout()

        hbox.addStretch(1)
        hbox.addWidget(okButton)
        hbox.addWidget(cancelButton)

        vbox = QVBoxLayout()
        btn1 = QPushButton('按钮1')
        btn2 = QPushButton('按钮2')
        btn3 = QPushButton('按钮3')

        vbox.addStretch(0)
        vbox.addWidget(btn1)
        vbox.addWidget(btn2)
        vbox.addWidget(btn3)

        vbox.addStretch(1)
        vbox.addLayout(hbox)

        self.setLayout(vbox)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = RightBottomButton()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648206781934-dcedd939-1b89-4d01-bc6e-29875e94dd4d.png#clientId=uddd2ac66-43c5-4&from=paste&height=339&id=EJxgq&originHeight=339&originWidth=416&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9999&status=done&style=none&taskId=u6786aeca-c068-4ec1-ac51-9f562208ffd&title=&width=416)   **两个布局，一个垂直布局一个水平布局通过addStretch设置伸缩量使它们分开**
<a name="Ronyr"></a>
### 栅格布局QGridLayout
<a name="vXMwA"></a>
#### 用循环方式实现计算器
```python
import sys
from PyQt5.QtWidgets import *


class Calc(QWidget):
    def __init__(self):
        super(Calc, self).__init__()
        self.setWindowTitle('栅格布局')
        grid = QGridLayout()
        self.setLayout(grid)
        names = ['Cls', 'Back', '', 'Close',
                 '7', '8', '9', '/',
                 '4', '5', '6', '*',
                 '1', '2', '3', '-',
                 '0', '.', '=', '+', ]
        positions = [(i, j) for i in range(5) for j in range(4)]  # 得到5（下标为4）行4（下标为3）列的值
        print(positions)
        # zip 的作用是将两个不同列表中的元素一一对应（也可以元素对应元组），形成一个新的列表（以元组的形式对应）
        for position, name in zip(positions, names):
            if name == '':
                continue
            button = QPushButton(name)

            grid.addWidget(button, *position)  # *号的作用是将元组拆成元素，例如（1，2）拆成1 2，之所以拆是因为addWidget不接受元组


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = Calc()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648209766370-221517da-1c9d-4ea4-9828-b6f8cc140176.png#clientId=uddd2ac66-43c5-4&from=paste&height=200&id=p24jO&originHeight=200&originWidth=356&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7729&status=done&style=none&taskId=uc42ed763-6612-4b77-9dd8-d8ec4cefd8b&title=&width=356)
<a name="B9gb9"></a>
#### 进行表单UI设计
```python
import sys
from PyQt5.QtWidgets import *


class GridForm(QWidget):
    def __init__(self):
        super(GridForm, self).__init__()
        self.setWindowTitle('栅格布局:表单设计')
        titleLabel = QLabel('标题')
        authorLabel = QLabel('作者')
        contentLabel = QLabel('内容')
        titleEdit = QLineEdit()
        authorEdit = QLineEdit()
        contentEdit = QTextEdit()

        grid = QGridLayout()
        grid.setSpacing(10) # 设置栅格的间距
        grid.addWidget(titleLabel, 1, 0)
        grid.addWidget(titleEdit, 1, 1)
        grid.addWidget(authorLabel, 2, 0)
        grid.addWidget(authorEdit, 2, 1)
        grid.addWidget(contentLabel, 3, 0)
        grid.addWidget(contentEdit, 3, 1, 5, 1)

        self.setLayout(grid)
        self.resize(350, 300)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = GridForm()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648211139062-de28221d-8911-42c3-a9a8-3797308ae5de.png#clientId=uddd2ac66-43c5-4&from=paste&height=339&id=xpQHd&originHeight=339&originWidth=366&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10111&status=done&style=none&taskId=u772bcde4-2a44-4cf0-a619-9d741a26557&title=&width=366)
<a name="WZ4aI"></a>
### 表单布局QFormLayout
表单设计可以通过栅格布局或者表单布局创建<br />主要区别是一个是使用addWidget  一个是使用addRow
```python
import sys
from PyQt5.QtWidgets import *


class FormLayout(QWidget):
    def __init__(self):
        super(FormLayout, self).__init__()
        self.setWindowTitle('表单布局')
        titleLabel = QLabel('标题')
        authorLabel = QLabel('作者')
        contentLabel = QLabel('内容')
        titleEdit = QLineEdit()
        authorEdit = QLineEdit()
        contentEdit = QTextEdit()

        formLayout = QFormLayout()
        formLayout.addRow(titleLabel,titleEdit)
        formLayout.addRow(authorLabel,authorEdit)
        formLayout.addRow(contentLabel,contentEdit)

        self.setLayout(formLayout)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = FormLayout()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648211552063-f0b688d2-8e90-4c63-8d45-fafdb20e9427.png#clientId=uddd2ac66-43c5-4&from=paste&height=305&id=xBKi4&originHeight=305&originWidth=324&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7592&status=done&style=none&taskId=u8035015c-05fd-4e14-9ed1-1f4a3efaad7&title=&width=324)
<a name="hs5MB"></a>
### 拖动控件之间的边界（QSplitter）
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class Splitter(QWidget):
    def __init__(self):
        super(Splitter, self).__init__()
        self.initUI()

    def initUI(self):
        hbox = QHBoxLayout()
        self.setWindowTitle('QSplitter 例子')
        self.setGeometry(300, 300, 300, 200)
        topleft = QFrame()
        topleft.setFrameShape(QFrame.StyledPanel)  # 绘制一个矩形面板
        bottom = QFrame()
        bottom.setFrameShape(QFrame.StyledPanel)
        splitter1 = QSplitter(Qt.Horizontal)  # 创建水平拖动控件
        textedit = QTextEdit()
        # 设置受水平拖动控件控制的矩形面板
        splitter1.addWidget(topleft)
        splitter1.addWidget(textedit)
        splitter1.setSizes([200, 100])  # 设置拖动控件默认位置

        splitter2 = QSplitter(Qt.Vertical)  # 创建垂直拖动控件
        # 设置受水平拖动控件控制的矩形面板
        splitter2.addWidget(splitter1)
        splitter2.addWidget(bottom)

        hbox.addWidget(splitter2)
        self.setLayout(hbox)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = Splitter()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648215257269-8be0648e-5a5a-4117-a1b8-50c35ca0005f.png#clientId=uddd2ac66-43c5-4&from=paste&height=239&id=Y8k1Z&originHeight=239&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=6368&status=done&style=none&taskId=ue98f6ef4-b1c2-4156-a15f-50143da2aff&title=&width=316)
<a name="ICI2k"></a>
## 信号和槽
在 Qt 中，用户和控件的每次交互过程称为一个事件，比如“用户点击按钮”是一个事件，“用户关闭窗口”也是一个事件。每个事件都会发出一个信号，例如用户点击按钮会发出“按钮被点击”的信号，用户关闭窗口会发出“窗口被关闭”的信号。

Qt 中的所有控件都具有接收信号的能力，一个控件还可以接收多个不同的信号。对于接收到的每个信号，控件都会做出相应的响应动作。例如，按钮所在的窗口接收到“按钮被点击”的信号后，会做出“关闭自己”的响应动作；再比如输入框自己接收到“输入框被点击”的信号后，会做出“显示闪烁的光标，等待用户输入数据”的响应动作。在 Qt 中，**对信号做出的响应动作就称为槽。**

![](https://cdn.nlark.com/yuque/0/2022/gif/2623605/1647265244137-79d7c317-be6d-47a3-8a0a-d51b481cba97.gif#clientId=u88a69422-e7a2-4&from=paste&id=wWp88&originHeight=427&originWidth=500&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u1f621fff-41d3-4faa-95ec-654681be45f&title=)<br />图 1 信号和槽

信号和槽机制底层是通过函数间的相互调用实现的。每个信号都可以用函数来表示，称为信号函数；每个槽也可以用函数表示，称为槽函数。例如，“按钮被按下”这个信号可以用 clicked() 函数表示，“窗口关闭”这个槽可以用 close() 函数表示，信号和槽机制实现“点击按钮会关闭窗口”的功能，其实就是 clicked() 函数调用 close() 函数的效果。
<a name="KwIm6"></a>
### connect()函数实现信号和槽
connect() 是 QObject 类中的一个静态成员函数，专门用来关联指定的信号函数和槽函数。<br />关联某个信号函数和槽函数，需要搞清楚以下 4 个问题：

- 信号发送者是谁？
- 哪个是信号函数？
- 信号的接收者是谁？
- 哪个是接收信号的槽函数？
<a name="Q3v5K"></a>
### 不同控件对应的信号

1. Qlabel控件(标签控件): linkHovered(滑过时触发)  linkActivated(单击时触发)
2. QLineEdit控件(输入框控件):textChanged(文本改变时触发),editingFinished(文本输入时触发)
3. QPushButton控件(普通按钮控件):clicked(单击按钮时触发)
4. QRadioButton控件(单选按钮控件):toggled(按钮被选中时触发)
5. QCheckBox控件(复选框控件![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647682554170-541ca9bc-e302-48ed-8dc1-a86eaf669074.png#clientId=u28f4b901-98ba-4&from=paste&height=94&id=tq8zp&originHeight=94&originWidth=180&originalType=binary&ratio=1&rotation=0&showTitle=false&size=19304&status=done&style=none&taskId=ua45a1d3d-5810-4379-87c8-d9ccc622bce&title=&width=180)):stateChanged(按钮状态改变时触发)
6. QComboBox控件(下拉列表控件):currentIndexChanged(列表选择改变时触发)
7. QSlider控件(滑块控件):valueChanged(当滑块的值改变时触发)
8. QSpinBox控件(计数器控件![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647693314236-d14be68e-7398-48ba-aafa-61a66e81cecf.png#clientId=u28f4b901-98ba-4&from=paste&height=30&id=zT6Fy&originHeight=30&originWidth=282&originalType=binary&ratio=1&rotation=0&showTitle=false&size=648&status=done&style=none&taskId=ub3619d59-9337-47a2-9e61-455477001d6&title=&width=282)):valueChanged(当计数器中的值改变时触发
9. QAction创建菜单栏中的菜单或者工具栏中的工具：triggered（当点击菜单时触发）
10. tb1 = self.addToolBar("File")创建的工具栏（是工具栏而不是工具）：actionTriggered  (当点击工具栏中的任意一个工具就会触发)
11. QListWidget() 扩展的列表控件 ：itemClicked  (当点击列表中的某一项时触发，触发时传参数是QListWidgetItem )
12. QListWidget() 扩展的列表控件：currentRowChanged（当改变选择的列表行时调用）
<a name="QQH4t"></a>
### 生成自定义信号pyqtSignal
通过生成pyqtSignal的实例（可自定义发送时的参数类型）（pyqtSignal是QObject中的方法因此需要在类中定义信号）<br />使用时需要先关联再通过emit发送参数

```python
from PyQt5.QtCore import *


class MyTypeSignal(QObject):
    '''自定义信号的类'''
    sendmsg = pyqtSignal(object)
    sendmsg1 = pyqtSignal(str, int, int)  # 发送三个带类型的参数。

    def run(self):
        '''自定义信号发送时传入的参数'''
        self.sendmsg.emit('Hello PyQt5')

    def run1(self):
        self.sendmsg1.emit('hello', 3, 4)


class MySlot(QObject):
    '''自定义槽'''

    def get(self, msg):
        print('信息：' + msg)

    def get1(self, msg, a, b):
        print(msg)
        print(a + b)


if __name__ == '__main__':
    send = MyTypeSignal()  # 创建信号的实例
    slot = MySlot()  # 创建槽的实例
    send.sendmsg.connect(slot.get)  # 连接信号与槽
    send.sendmsg1.connect(slot.get1)
    send.run()  # 发送信号：执行了：self.sendmsg.emit('Hello PyQt5')
    send.run1()   # 发送信号：执行了：self.sendmsg1.emit('hello', 3, 4)
    send.sendmsg.disconnect(slot.get)  # 断开连接
    send.run()  # 因为断开了连接而无法发送信号



```
输出：<br />信息：Hello PyQt5<br />hello<br />7
<a name="slxKI"></a>
### 为类添加多个信号
```python
from PyQt5.QtCore import *


class MultiSignal(QObject):
    signal1 = pyqtSignal()
    signal2 = pyqtSignal(int)
    signal3 = pyqtSignal(int, str)
    signal4 = pyqtSignal(list)
    signal5 = pyqtSignal(dict)
    signal6 = pyqtSignal([int, str], [str])  # 既可以存取int，str类型参数也可以只存取str类型参数

    def __init__(self):
        super(MultiSignal, self).__init__()
        self.signal1.connect(self.signalCall1)
        self.signal2.connect(self.signalCall2)
        self.signal3.connect(self.signalCall3)
        self.signal4.connect(self.signalCall4)
        self.signal5.connect(self.signalCall5)

        self.signal6[str].connect(self.signalCall6Overload)  # 将str类型的信号关联signalCall60verload
        self.signal6[int, str].connect(self.signalCall6)  # 将int,str类型的信号关联signalcall6

        self.signal1.emit()
        self.signal2.emit(10)
        self.signal3.emit(1, 'hello world')
        self.signal4.emit([1, 2, 3, 4, 5, 6])
        self.signal5.emit({"name": "Bill", "age": 30})
        self.signal6[str].emit("test")  # 发送str类型信号
        self.signal6[int, str].emit(100, "mytest")  # 发送int，str类型信号

    def signalCall1(self):
        print('signal1 emit')

    def signalCall2(self, val):
        print('signal2 emit,value:', val)

    def signalCall3(self, val, text):
        print('signal3 emit.value:', val, text)

    def signalCall4(self, val):
        print('signal4 emit,value:', val)

    def signalCall5(self, val):
        print('signal5 emit,value:', val)

    def signalCall6(self, val, text):
        print('signal6 emit,value:', val, text)

    def signalCall6Overload(self, val):
        print('signal6 overload emit,value:', val)


if __name__ == '__main__':
    multiSignal = MultiSignal()

```
输出：<br />signal1 emit<br />signal2 emit,value: 10<br />signal3 emit.value: 1 hello world<br />signal4 emit,value: [1, 2, 3, 4, 5, 6]<br />signal5 emit,value: {'name': 'Bill', 'age': 30}<br />signal6 overload emit,value: test<br />signal6 emit,value: 100 mytest
<a name="GXocG"></a>
### 信号和槽的N对N连接和断开连接
没什么需要讲的，就是定义的信号可以连接并发送给不同的槽，以及多个信号可以共用一个槽<br />断开连接上上一节已经使用过了，就是使用disconnect方法。
<a name="uQOd6"></a>
### 为窗口添加信号
```python
from PyQt5.QtWidgets import *
from PyQt5.QtCore import *
import sys


class WinSignal(QWidget):
    button_clicked_signal = pyqtSignal()  # 创建自定义信号

    def __init__(self):
        super(WinSignal, self).__init__()
        self.setWindowTitle('为窗口类增加信号')
        self.resize(300, 100)
        btn = QPushButton('关闭窗口', self)
        btn.clicked.connect(self.btn_clicked)
        # 将自定义信号与槽连接在一起
        self.button_clicked_signal.connect(self.btn_close)

    def btn_clicked(self):
        # 按钮被点击后进行发送自定义信号调用自定义信号的槽
        self.button_clicked_signal.emit()

    def btn_close(self):
        # 自定义信号调用的槽，功能是关闭窗口
        self.close()


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = WinSignal()
    main.show()
    sys.exit(app.exec_())

```
点击关闭窗口后调用自定义信号所绑定的槽实现关闭窗口的功能。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648263389005-de6b94c8-1268-4dd6-b3ff-15fbe3bf3430.png#clientId=uef9b1ee7-2eb1-4&from=paste&height=139&id=N2ZM9&originHeight=139&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4065&status=done&style=none&taskId=ud72e465b-765b-4f8d-866d-f3a6c1b6c57&title=&width=316)
<a name="EcJHj"></a>
### 多线程更新UI数据（在两个线程中传递数据）
```python
import sys
import time

from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class BackendThread(QThread):
    # 定义子线程,利用信号传递两个线程之间的数据
    update_date = pyqtSignal(str)

    def run(self):
        while True:
            data = QDateTime.currentDateTime()  # 获取当前时间
            currentTime = data.toString("yyyy-MM-dd hh:mm:ss")  # 设置时间的格式
            self.update_date.emit(str(currentTime))  # 发送信号
            time.sleep(1)  # 时间的跳跃间隔


class ThreadUpdateUI(QDialog):
    # 主进程
    def __init__(self):
        QDialog.__init__(self)
        self.setWindowTitle('多线程更新UI数据')
        self.resize(400, 100)
        self.input = QLineEdit(self)
        self.input.resize(400, 100)
        self.initUI()

    def initUI(self):
        self.backend = BackendThread()
        self.backend.update_date.connect(self.handleDisplay)
        self.backend.start()

    def handleDisplay(self, data):
        self.input.setText(data)  # 将输入框显示的文本改为data(时间)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = ThreadUpdateUI()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648265459411-b569de09-9fea-410b-94e9-65d30daecadb.png#clientId=uef9b1ee7-2eb1-4&from=paste&height=139&id=yx2R2&originHeight=139&originWidth=416&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4866&status=done&style=none&taskId=u9db9875a-d581-44cb-9874-394d4a5efb0&title=&width=416)
<a name="VFIzQ"></a>
### 信号与槽自动连接
```python
from PyQt5 import QtCore
from PyQt5.QtWidgets import QApplication, QWidget, QHBoxLayout, QPushButton
import sys


class AutoSignalSlot(QWidget):
    def __init__(self):
        super(AutoSignalSlot, self).__init__()
        self.okButton = QPushButton('ok', self)
        self.okButton.setObjectName('okButton') # 给按钮起一个名字
        self.okButton1 = QPushButton('cancel', self)
        self.okButton1.setObjectName('cancelButton')
        layout = QHBoxLayout()
        layout.addWidget(self.okButton)
        self.setLayout(layout)
        self.resize(200, 100)
        QtCore.QMetaObject.connectSlotsByName(self)  # 通过名字自动连接控件与槽
        # 传统手动绑定槽
        # self.okButton.clicked.connect(self.on_okButton_clicked)

    @QtCore.pyqtSlot() 
    def on_okButton_clicked(self): # 通过on_可以根据控件名字来自动连接控件与槽
        print('点击了ok按钮')

    @QtCore.pyqtSlot()
    def on_cancelButton_clicked(self):
        print('点击了cancel按钮')


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = AutoSignalSlot()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648274346996-39fe14ac-b7c4-41f7-bbfc-5cafcecd07ed.png#clientId=uef9b1ee7-2eb1-4&from=paste&height=137&id=q8htB&originHeight=137&originWidth=362&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5338&status=done&style=none&taskId=u3d5101ce-73ff-4adc-a954-7fc878fd206&title=&width=362)
<a name="qSx9n"></a>
### 用Lambda表达式为槽函数传递参数
先介绍一下Lambda表达式<br />Lambda表达式名字叫做匿名函数，就是没有名字的函数。<br />目前个人理解：  lambda中的冒号前面是输入参数，冒号后面是返回值。 lambda函数本身是一个函数，可以通过将lambda函数赋值给一个变量，然后就可以通过变量间接的调用lambda函数<br />使用介绍：<br />fun = lambda: print("hello world")<br />fun()# 不需要输入直接返回 hello world<br />fun1 = lambda x, y: print(x, y)<br />fun1("a", "b") # 输入两个参数x，y返回（x,y）<br />输出：<br />hello world<br />a b
```python
from PyQt5.QtWidgets import *
import sys


class LambdaSlotArg(QMainWindow):
    def __init__(self):
        super(LambdaSlotArg, self).__init__()
        self.setWindowTitle("使用Lambda表达式为槽函数传递参数")
        button1 = QPushButton("按钮1")
        button2 = QPushButton("按钮2")
        ok = 100  # 使用Lambda表达式可以接收外部的变量
        button1.clicked.connect(lambda: self.onButtonClick(10, ok))
        button2.clicked.connect(lambda: self.onButtonClick(ok, -20))
        button1.clicked.connect(lambda: QMessageBox.information(self, "结果", "单击了button1"))
        layout = QHBoxLayout()
        layout.addWidget(button1)
        layout.addWidget(button2)
        mainFrame = QWidget()
        mainFrame.setLayout(layout)
        self.setCentralWidget(mainFrame)

    def onButtonClick(self, m, n):
        print('m+n=', m + n)
        QMessageBox.information(self, '结果', str(m + n))


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = LambdaSlotArg()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648276363255-e0eced07-bd80-4c4d-8ee4-b9d3bdc5972f.png#clientId=uef9b1ee7-2eb1-4&from=paste&height=218&id=nhzWa&originHeight=218&originWidth=424&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14224&status=done&style=none&taskId=u9a90a8f7-3dda-404d-a04c-062e8a9731a&title=&width=424)
<a name="uP7FL"></a>
### 用partial对象为槽函数传递参数

partial介绍：和装饰器一样，它可以扩展函数的功能，但又不完成等价于装饰器。<br />使用时需要先导入partial模块<br />from functools import partial<br />partial使用：类func = functools.partial(func, *args, **keywords)  func为要增强的函数，args为元组类型数据（不需要在意名字，名字是什么无所谓，需要在意的是*），keywords为字典类型数据（不需要在意名字，名字是什么无所谓，需要在意的是**）   args和keywords这些数据为默认传入func的数据。<br />举例：<br />def add(*args):     <br />return sum(args) <br />add_100 = partial(add, 100)<br />print(add_100(1, 2, 3))  # 106<br />partial与lambda为槽函数传递参数的区别：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648277325580-a60917d7-5cfd-401a-915e-ac6c66b73f15.png#clientId=uef9b1ee7-2eb1-4&from=paste&height=52&id=Gf5D8&originHeight=52&originWidth=505&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9361&status=done&style=none&taskId=ue3fa3b31-5604-4c51-9aa5-d2631b3577d&title=&width=505)
<a name="tdmvU"></a>
### override(覆盖)槽函数
举例覆盖系统自带的槽函数：KeyPressEvent 按下键盘时执行事件：<br />这段代码的功能就是新增了两个键盘对应事件：<br />当按下esc键时关闭程序<br />当按下alt键时更改窗口标题名
```python
from PyQt5.QtWidgets import *
from PyQt5.QtCore import *
import sys

class OverrideSlot(QWidget) :
    def __init__(self):
        super(OverrideSlot, self).__init__()
        self.setWindowTitle("Override(覆盖)槽函数")

    def keyPressEvent(self,e) :  # 覆盖系统的keyPressEvent函数（根据键盘对应事件，默认是不做事件）
        if e.key() == Qt.Key_Escape : # 当按下ESC键时
            self.close()
        elif e.key() == Qt.Key_Alt :
            self.setWindowTitle("按下Alt键")

if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = OverrideSlot()
    main.show()
    sys.exit(app.exec_())

```
<a name="GRgvA"></a>
### 多窗口交互（1）：不使用信号与槽
多窗口交互介绍： 举例：在窗口1选择的内容在窗口2显示<br />如果不使用信号与槽那么就需要在窗口1直接调用窗口2的控件。<br />这种方法在编程方面更简单，但是缺点就是耦合性太强。
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class DateDialog(QDialog):
    """
    窗口1.显示日期
    """

    def __init__(self, parent=None):
        super(DateDialog, self).__init__(parent)
        self.setWindowTitle("DateDialog")
        layout = QVBoxLayout(self)
        self.datetime = QDateTimeEdit(self)
        self.datetime.setCalendarPopup(True)  # 设置下拉模块
        self.datetime.setDateTime(QDateTime.currentDateTime())  # 设置日期为当前日期
        layout.addWidget(self.datetime)
        # 使用按钮盒子类的实例
        buttons = QDialogButtonBox(QDialogButtonBox.Ok | QDialogButtonBox.Cancel, Qt.Horizontal, self)
        buttons.accepted.connect(self.accept)
        buttons.rejected.connect(self.reject)

        layout.addWidget(buttons)

    def dateTime(self):
        return self.datetime.dateTime()

    @staticmethod
    def getDateTime(parent=None):
        dialog = DateDialog(parent)
        result = dialog.exec()
        date = dialog.dateTime()
        return (date.date(), date.time(), result == QDialog.Accepted)


class MultiWindow1(QWidget):
    def __init__(self):
        super(MultiWindow1, self).__init__()
        self.setWindowTitle("多窗口交互（1）：不使用信号与槽")
        self.lineEdit = QLineEdit(self)
        self.button1 = QPushButton("弹出对话框1")
        self.button1.clicked.connect(self.onButton1Click)
        self.button2 = QPushButton('弹出对话框2')
        self.button2.clicked.connect(self.onButton2Click)

        gridLayout = QGridLayout()
        gridLayout.addWidget(self.lineEdit)
        gridLayout.addWidget(self.button1)
        gridLayout.addWidget(self.button2)
        self.setLayout(gridLayout)

    def onButton1Click(self):
        dialog = DateDialog(self)
        # 直接访问控件
        result = dialog.exec()
        date = dialog.dateTime()
        self.lineEdit.setText(date.date().toString())
        dialog.destroy()

    def onButton2Click(self):
        date, time, result = DateDialog.getDateTime()
        self.lineEdit.setText(date.toString())
        if result == QDialog.Accepted:
            print('点击确定按钮')
        else:
            print("点击取消按钮")


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = MultiWindow1()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648282956768-d10febfc-7333-4b4f-89b4-de7eebb0b74e.png#clientId=uef9b1ee7-2eb1-4&from=paste&height=152&id=J91fT&originHeight=152&originWidth=425&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11558&status=done&style=none&taskId=ua0e61a51-299a-4e9e-a027-94bbbbf7aab&title=&width=425)
<a name="LUCTe"></a>
### 多窗口交互（2）：使用信号与槽
如果一个窗口A和另一个窗口B交互，那么A尽量不要直接访问B窗口中的控件，应该访问B窗口中的信号，并指定与信号绑定的槽函数<br />例： 如果A直接访问B窗口的控件，一旦B窗口控件发生改变，那么A和B的代码都需要变化<br />如果A访问的是B中的信号，那么B中的控件发生了改变，只需要修改B中的代码即可。
```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *


class NewDateDialog(QDialog):
    Signal_OneParameter = pyqtSignal(str)

    def __init__(self, parent=None):
        super(NewDateDialog, self).__init__(parent)
        self.setWindowTitle('子窗口：用来发射信号')
        # 在布局中添加部件
        layout = QVBoxLayout(self)
        self.label = QLabel(self)
        self.label.setText('前者发射内置信号\n后者发射自定义信号')
        self.datetime_inner = QDateTimeEdit(self)
        self.datetime_inner.setCalendarPopup(True)
        self.datetime_inner.setDateTime(QDateTime.currentDateTime())
        self.datetime_emit = QDateTimeEdit(self)
        self.datetime_emit.setCalendarPopup(True)
        self.datetime_emit.setDateTime(QDateTime.currentDateTime())
        layout.addWidget(self.label)
        layout.addWidget(self.datetime_inner)
        layout.addWidget(self.datetime_emit)
        # 使用两个button(ok和cancel)分别连接accept()和reject()槽函数
        buttons = QDialogButtonBox(
            QDialogButtonBox.Ok | QDialogButtonBox.Cancel,
            Qt.Horizontal, self)
        buttons.accepted.connect(self.accept)
        buttons.rejected.connect(self.reject)
        layout.addWidget(buttons)
        self.datetime_emit.dateTimeChanged.connect(self.emit_signal)

    def emit_signal(self):
        date_str = self.datetime_emit.dateTime().toString()
        self.Signal_OneParameter.emit(date_str)


class MultiWindow2(QWidget):

    def __init__(self, parent=None):
        super(MultiWindow2, self).__init__(parent)
        self.resize(400, 90)
        self.setWindowTitle('多窗口交互（2）：使用信号与槽')
        self.open_btn = QPushButton('获取时间')
        self.lineEdit_inner = QLineEdit(self)
        self.lineEdit_emit = QLineEdit(self)
        self.open_btn.clicked.connect(self.openDialog)
        self.lineEdit_inner.setText('接收子窗口内置信号的时间')
        self.lineEdit_emit.setText('接收子窗口自定义信号的时间')
        grid = QGridLayout()
        grid.addWidget(self.lineEdit_inner)
        grid.addWidget(self.lineEdit_emit)
        grid.addWidget(self.open_btn)
        self.setLayout(grid)

    def openDialog(self):
        dialog = NewDateDialog(self)
        # 连接子窗口的内置信号与主窗口的槽函数
        dialog.datetime_inner.dateTimeChanged.connect(self.deal_inner_slot)
        # 连接子窗口的自定义信号与主窗口的槽函数
        dialog.Signal_OneParameter.connect(self.deal_emit_slot)
        dialog.show()

    def deal_inner_slot(self, date):
        self.lineEdit_inner.setText(date.toString())

    def deal_emit_slot(self, dateStr):
        self.lineEdit_emit.setText(dateStr)


if __name__ == "__main__":
    app = QApplication(sys.argv)
    form = MultiWindow2()
    form.show()
    sys.exit(app.exec_())

```
<a name="sykiC"></a>
## 开发第一个基于PyQt5的桌面应用
PyQt5的类都是以Q开头的。<br />开发时必须使用两个类：**QApplication**(这个代表整个应用程序)和**QWidget**(这个代表应用窗口,也可以用**QMainWindow**，**QDialog**代替，详情在下面有讲)。这两个类都在PyQt5.QtWidget这个模块中。
```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget

# if语句的作用是，只有在first模块这里运行才会执行下面的语句，如果在其他模块中导入此模块不会执行下方的代码
if __name__ == '__main__':
    # sys.argv是用来获得命令行参数的，这里是创建一个程序名字叫app
    app = QApplication(sys.argv)
    # 创建一个窗口
    w = QWidget()
    # 设置窗口的大小
    w.resize(400, 200)
    # 设置窗口的刚开始出现的位置
    w.move(300, 300)
    # 设置窗口的标题
    w.setWindowTitle("第一个基于PyQt5的桌面应用")
    # 显示窗口
    w.show()
    # 进入程序的主循环、并通过exit函数确保主循环安全结束
    sys.exit(app.exec_())

```
效果：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647260436304-b8cb00c3-e9d9-4f4a-a54a-f889af641c1e.png#clientId=u88a69422-e7a2-4&from=paste&height=239&id=emFxb&originHeight=239&originWidth=416&originalType=binary&ratio=1&rotation=0&showTitle=false&size=6666&status=done&style=none&taskId=u7237948c-a5ca-496f-943a-ba6c496f4c3&title=&width=416)
<a name="w5XG1"></a>
## 创建主窗口
有3种窗口<br />QMainWindow类生成的窗口自带菜单栏、工具栏和状态栏，中央区域还可以添加多个控件，常用来作为应用程序的主窗口<br />QWidget：所有的控件类都直接或者间接继承自 QWidget 类，它既可以用来制作窗口，也可以作为某个窗口上的控件。<br />QDialog：是对话窗口的基类，（对话窗口就是在主窗口里选择一个功能后，弹出的窗口，不关闭这个窗口是无法回到主窗口的。）没有菜单栏、工具栏、状态栏，但可以添加多个控件。<br />实际开发中，制作应用程序的主窗口可以用 QMainWindow 或者 QWdiget；制作一个提示信息的对话框就用 QDialog 或 QWidget；如果暂时无法决定，后续可能作为窗口，也可能作为控件，就选择 QWidget。
```python
import sys
from PyQt5.QtWidgets import QApplication, QMainWindow
from PyQt5.QtGui import QIcon


class FirstMainWin(QMainWindow):
    def __init__(self):
        super(FirstMainWin, self).__init__()
        # 设置主窗口的标题
        self.setWindowTitle("第一个主窗口应用")
        # 设置主窗口的大小
        self.resize(400, 300)
        # 设置状态栏
        self.status = self.statusBar()
        self.status.showMessage('只存在5秒的消息', 5000)


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # 设置软件窗口图标
    app.setWindowIcon(QIcon('./images/bool.png'))
    # main为窗口类的对象
    main = FirstMainWin()
    main.show()
    sys.exit(app.exec_())

```
效果：其中下面的标签栏只会显示5秒钟就消失了<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647260467438-57201bd3-3ea3-4cfa-b1f0-a9ea73c2a830.png#clientId=u88a69422-e7a2-4&from=paste&height=339&id=u7d386574&originHeight=339&originWidth=416&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9090&status=done&style=none&taskId=u23ee744b-3886-451e-8b4f-34a4d562e7f&title=&width=416)

<a name="RtJ28"></a>
## 退出应用程序
```python
import sys
from PyQt5.QtWidgets import QHBoxLayout, QMainWindow, QApplication, QPushButton, QWidget


class QuitApplication(QMainWindow):
    def __init__(self):
        super(QuitApplication, self).__init__()
        self.resize(300, 120)
        self.setWindowTitle("退出应用程序")

        # 添加button
        self.button1 = QPushButton('退出应用程序')
        # 将信号与槽关联
        self.button1.clicked.connect(self.onClick_Button)
        # 创建一个水平布局
        layout = QHBoxLayout()
        # 为布局添加按钮
        layout.addWidget(self.button1)
        # 创建主框架
        mainFrame = QWidget()
        # 将布局放到主框架上
        mainFrame.setLayout(layout)
        # 使主框架设置在中央
        self.setCentralWidget(mainFrame)

    # 按钮单击的事件（自定义的槽）
    def onClick_Button(self):
        # 得到发送信号的对象
        sender = self.sender()
        # sender.text为发送信号的对象的名字
        print(sender.text() + '按钮被按下')
        # 获取APP实例对象
        app = QApplication.instance()
        # 退出应用程序
        app.quit()


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = QuitApplication()
    main.show()
    sys.exit(app.exec_())
```
<a name="y7hpg"></a>
## 屏幕坐标系
```python
import sys
from PyQt5.QtWidgets import QHBoxLayout, QMainWindow, QApplication, QPushButton, QWidget

app = QApplication(sys.argv)


def onClicked_Button():
    print("1")
    print("widget.x()=%d" % widget.x())  # 250 窗口横坐标
    print("widget.y()=%d" % widget.y())  # 200 窗口纵坐标
    print("widget.width()=%d" % widget.width())  # 300 工作区宽度
    print("widget.height()=%d" % widget.height())  # 240 工作区高度

    print("2")
    print("widget.geometry().x() = %d" % widget.geometry().x())  # 251 工作区横坐标
    print("widget.geometry().y() = %d" % widget.geometry().y())  # 231 工作区纵坐标
    print("widget.geometry().width()=%d" % widget.geometry().width())  # 300 工作区高度
    print("widget.geometry().height()=%d" % widget.geometry().height())  # 240 工作区宽度

    print("3")
    print("widget.frameGeometry().x() = %d" % widget.frameGeometry().x())  # 250 窗口横坐标
    print("widget.frameGeometry().y() = %d" % widget.frameGeometry().y())  # 200 窗口纵坐标
    print("widget.frameGeometry().width()=%d" % widget.frameGeometry().width())  # 302 窗口宽度
    print("widget.frameGeometry().height()=%d" % widget.frameGeometry().height())  # 272 窗口高度


widget = QWidget()
btn = QPushButton(widget)
btn.setText("按钮")
btn.clicked.connect(onClicked_Button)
btn.move(24, 52)
widget.resize(300, 240)
widget.move(250, 200)
widget.setWindowTitle("屏幕坐标系")
widget.show()
sys.exit(app.exec_())
```
<a name="wOr0n"></a>
## 设置窗口和应用图标
```python
import sys
from PyQt5.QtWidgets import QApplication, QMainWindow
from PyQt5.QtGui import QIcon


class iconForm(QMainWindow):
    def __init__(self):
        super(iconForm, self).__init__()
        self.initUI()

    def initUI(self):
        # 设置主窗口的标题
        self.setWindowTitle("设置窗口图标")
        # 设置主窗口的xy轴坐标以及宽和高
        self.setGeometry(300, 300, 250, 250)
        # 设置窗口的图标
        self.setWindowIcon(QIcon('./images/bool.png'))


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = iconForm()
    main.show()
    sys.exit(app.exec_())

```
<a name="g2cqN"></a>
## 为控件添加提示信息
```python
# 显示提示消息
import sys
from PyQt5.QtWidgets import QHBoxLayout, QMainWindow, QApplication, QPushButton, QWidget, QToolTip
from PyQt5.QtGui import QFont


class TooltipForm(QMainWindow):
    def __init__(self):
        super(TooltipForm, self).__init__()
        self.initUI()

    def initUI(self):
        # 设置字体类型以及字号
        QToolTip.setFont(QFont('SansSerif', 12))
        # 设置提示信息，其中<b><\b>之间的内容用黑体字
        self.setToolTip("今天是<b>星期五<\b>")
        self.setGeometry(300, 300, 200, 300)
        self.setWindowTitle("显示控件提示消息")

        self.button1 = QPushButton("我的按钮")
        # 为按钮设置提示信息
        self.button1.setToolTip("提示：这是一个按钮")
        # 创建一个水平布局
        layout = QHBoxLayout()
        # 为布局添加按钮
        layout.addWidget(self.button1)
        # 创建主框架
        mainFrame = QWidget()
        # 将布局放到主框架上
        mainFrame.setLayout(layout)
        # 使主框架设置在中央
        self.setCentralWidget(mainFrame)

if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = TooltipForm()
    main.show()
    sys.exit(app.exec_())

```
效果：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647322741267-6b7b60af-033d-4746-9dec-0407eba4f7d3.png#clientId=uf114e347-edf6-4&from=paste&height=335&id=ucd4ec8a7&originHeight=335&originWidth=242&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10216&status=done&style=none&taskId=u4d5d63a5-a24b-4234-bb1b-303450c6620&title=&width=242)
<a name="LMMkD"></a>
## QLabel控件的基本用法
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647322924692-c67931a6-7c8c-4d3e-8f5a-b639e74ab496.png#clientId=uf114e347-edf6-4&from=paste&height=560&id=ud107c52b&originHeight=560&originWidth=542&originalType=binary&ratio=1&rotation=0&showTitle=false&size=174991&status=done&style=none&taskId=u2f246592-0605-46ca-b97e-f0fd5ffb03a&title=&width=542)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647323939979-08d2fb4f-60c5-44a8-80ce-14f699a7b35d.png#clientId=uf114e347-edf6-4&from=paste&height=119&id=ub74711d6&originHeight=119&originWidth=701&originalType=binary&ratio=1&rotation=0&showTitle=false&size=88398&status=done&style=none&taskId=ub6be560a-b934-42b0-9f15-d2c2dc67ad6&title=&width=701)
```python
import sys
from PyQt5.QtWidgets import QVBoxLayout, QMainWindow, QApplication, QWidget, QLabel
from PyQt5.QtGui import QPalette, QPixmap
from PyQt5.QtCore import Qt


class QLabelDemo(QWidget):
    def __init__(self):
        super(QLabelDemo, self).__init__()
        self.initUI()

    def initUI(self):
        # 创建标签
        label1 = QLabel(self)
        label2 = QLabel(self)
        label3 = QLabel(self)
        label4 = QLabel(self)
        # 为标签1添加文本信息
        label1.setText("<font color=yellow>这是一个文本标签。</font>")
        # 使标签填充背景
        label1.setAutoFillBackground(True)
        # 创建调色板
        palette = QPalette()
        # 设置背景色,设置颜色需要用到Qt，Qt需要from PyQt5.QtCore import Qt
        palette.setColor(QPalette.Window, Qt.blue)
        # 使标签1使用调色板的颜色
        label1.setPalette(palette)
        # 设置对齐方式：(居中)
        label1.setAlignment(Qt.AlignCenter)
        # 将标签2设置为超链接:超链接的写法：  a  href= 链接
        label2.setText("<a href='#'>欢迎使用Python GUI程序</a>")
        # 标签3为图片显示
        # 设置标签3为居中对齐
        label3.setAlignment(Qt.AlignCenter)
        # 设置标签3的提示
        label3.setToolTip('这是一个图片标签')
        # 设置标签3的图片
        label3.setPixmap(QPixmap("./images/bool.png"))
        # 为标签4设置扩展链接功能，为True时就允许跳转到超链接内容不连接槽函数，为False时就只连接槽函数
        label4.setOpenExternalLinks(True)
        label4.setText("<a href='https://wallhaven.cc'>壁纸网站</a>")
        # 将标签4对齐方式设置为向右对齐
        label4.setAlignment(Qt.AlignRight)
        label4.setToolTip("这是一个超级链接")

        # 创建一个垂直布局内容为4个标签
        vbox = QVBoxLayout()
        vbox.addWidget(label1)
        vbox.addWidget(label2)
        vbox.addWidget(label3)
        vbox.addWidget(label4)
        # 关联槽 linkHovered为滑动到时触发，linkActivated为点击时触发
        label2.linkHovered.connect(self.linkHovered)
        label4.linkActivated.connect(self.linkClicked)
        # 添加布局
        self.setLayout(vbox)
        self.setWindowTitle("QLabel控件演示")

    def linkHovered(self):
        print("鼠标滑动到了label2标签并触发了事件")

    def linkClicked(self):
        print("鼠标点击了label4标签并触发了事件")


if __name__ == "__main__":
    app = QApplication(sys.argv)
    main = QLabelDemo()
    main.show()
    sys.exit(app.exec_())

```
运行效果：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647332029683-3cccc7c1-4733-4589-9edc-2dbad23f3b93.png#clientId=uf114e347-edf6-4&from=paste&height=321&id=uf73d1243&originHeight=321&originWidth=238&originalType=binary&ratio=1&rotation=0&showTitle=false&size=19629&status=done&style=none&taskId=u105ac4f7-5915-4fde-a0eb-c9ca0fe473d&title=&width=238)
<a name="W5tbb"></a>
## QLabel与伙伴控件
```python
from PyQt5.QtWidgets import *
import sys


# 创建一个对话框类
class QlabelBuddy(QDialog):
    def __init__(self):
        super(QlabelBuddy, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("QLabel与伙伴控件")
        # &的作用是热键，使用窗口时按alt+n可以快速选中Name标签
        nameLabel = QLabel('&Name', self)
        # 添加一个文本输入框
        nameLineEdit = QLineEdit(self)
        # 将nameLineEdit设置为nameLabel的伙伴控件
        nameLabel.setBuddy(nameLineEdit)

        passwordnameLabel = QLabel('&password', self)
        passwordnameLineEdit = QLineEdit(self)
        passwordnameLabel.setBuddy(passwordnameLineEdit)

        # 创建按钮
        btnOK = QPushButton("&OK")
        btnCancel = QPushButton("&Cancel")

        # 创建栅格布局
        mainLayout = QGridLayout(self)
        # 设置栅格布局  addWidget后面的参数的意思： 第一个为控件名，第二个为创建的位置，数值为行列的下标，最后两个控制的是长度与宽度。
        mainLayout.addWidget(nameLabel, 0, 0)
        mainLayout.addWidget(nameLineEdit, 0, 1, 1, 2)
        mainLayout.addWidget(passwordnameLabel, 1, 0)
        mainLayout.addWidget(passwordnameLineEdit, 1, 1, 1, 2)
        mainLayout.addWidget(btnOK, 2, 1)
        mainLayout.addWidget(btnCancel, 2, 2)


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    main = QlabelBuddy()
    main.show()
    sys.exit(app.exec_())

```
效果：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647335276347-8744e246-c810-475d-a523-ff6582882290.png#clientId=uf114e347-edf6-4&from=paste&height=136&id=u744a9efa&originHeight=136&originWidth=248&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4084&status=done&style=none&taskId=u73285f56-9388-41f6-bd13-f5a96779720&title=&width=248)
<a name="oWzUx"></a>
## QLIneEdit
<a name="rFs3x"></a>
### QLineEdit控件和回显模式
QLineEdit控件上一节使用过，就是这个![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647340548242-61d3ebb1-b041-4dc3-a45b-0a515ead59e8.png#clientId=uf114e347-edf6-4&from=paste&height=70&id=u8cef439b&originHeight=70&originWidth=241&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1263&status=done&style=none&taskId=u2f912d74-e9d6-430d-b955-8295ec95e49&title=&width=241)生成可编辑的文字框。<br />EchoMode回显模式<br />回显模式有四种：<br />1.Normal 就是正常的输入后显示输出<br />2.NoEcho 意思是输入后什么都不显示在屏幕上，但是机器能够读取到。<br />3.Password 意思是输入后以符号表示输入。<br />4.PasswordEchoOnEdit 意思是编辑时显示正常，不编辑时显示符号。
```python
from PyQt5.QtWidgets import *
import sys


class QLineEditEchoMode(QWidget):
    def __init__(self):
        super(QLineEditEchoMode, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("文本输入框的回显模式")
        # 创建一个表单布局
        formLayout = QFormLayout()
        # 创建4个可输入文本框
        normalLineEdit = QLineEdit()
        noEchoLineEdit = QLineEdit()
        passworldLineEdit = QLineEdit()
        passwordEchoOnEditLineEdit = QLineEdit()
        # 为表单布局添加文字和可输入文本框
        formLayout.addRow("Normal", normalLineEdit)
        formLayout.addRow("NoEcho", noEchoLineEdit)
        formLayout.addRow("Passworld", passworldLineEdit)
        formLayout.addRow("PasswordEchoOnEdit", passwordEchoOnEditLineEdit)
        # 为文本框添加提示信息
        normalLineEdit.setPlaceholderText("Normal")
        noEchoLineEdit.setPlaceholderText("NoEcho")
        passworldLineEdit.setPlaceholderText("Password")
        passwordEchoOnEditLineEdit.setPlaceholderText("PasswordEchoOnEdit")
        # 为文本框设置回显模式
        normalLineEdit.setEchoMode(QLineEdit.Normal)
        noEchoLineEdit.setEchoMode(QLineEdit.NoEcho)
        passworldLineEdit.setEchoMode(QLineEdit.Password)
        passwordEchoOnEditLineEdit.setEchoMode(QLineEdit.PasswordEchoOnEdit)
        # 赋予布局
        self.setLayout(formLayout)


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = QLineEditEchoMode()
    main.show()
    sys.exit(app.exec_())

```
效果：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647344702540-17fd4432-be8d-40d7-9cae-6c9af0339174.png#clientId=uf114e347-edf6-4&from=paste&height=159&id=udbea8816&originHeight=159&originWidth=285&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9089&status=done&style=none&taskId=u612440e5-7533-48d9-8b0d-adee25d86a7&title=&width=285)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647344718175-1c00274b-5146-4c63-ad43-c293a76f44f4.png#clientId=uf114e347-edf6-4&from=paste&height=159&id=uce166ccf&originHeight=159&originWidth=285&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8596&status=done&style=none&taskId=u90024915-b0c3-4a16-84d0-cf8c07a26e7&title=&width=285)<br />其中passwordechoonedit是输入是为数字切换到其他框后就变成圆圈，noecho是已经输入了但是不显示在屏幕上
<a name="l7K1J"></a>
### 限制QLineEdit控件的输入（校验器）
限制举例： 只能输入整数、浮点数或满足一定条件的字符串
```python
# Validator翻译名字叫校验器，因此导入这三个分别是校验整型，模块，正则表达式的。
# QRegExp是正则表达式需要的
from PyQt5.QtWidgets import *
from PyQt5.QtGui import QIntValidator, QDoubleValidator, QRegExpValidator
from PyQt5.QtCore import QRegExp
import sys


class QLineEditValidator(QWidget):
    def __init__(self):
        super(QLineEditValidator, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("校验器")
        # 创建表单布局
        formLayout = QFormLayout()
        # 创建三个输入框
        intLineEdit = QLineEdit()
        doubleLineEdit = QLineEdit()
        validatorLineEdit = QLineEdit()
        # 为布局添加控件
        formLayout.addRow("整数类型", intLineEdit)
        formLayout.addRow("浮点类型", doubleLineEdit)
        formLayout.addRow("数字和字母", validatorLineEdit)
        # 为输入框添加提示信息
        intLineEdit.setPlaceholderText("整型")
        doubleLineEdit.setPlaceholderText("浮点型")
        validatorLineEdit.setPlaceholderText("字母和数字")
        # 创建校验器
        # 整数校验器 限制范围为1~99
        intValidator = QIntValidator()
        intValidator.setRange(1, 99)
        # 浮点校验器 限制范围为-360~360
        doubleValidator = QDoubleValidator()
        doubleValidator.setRange(-360, 360)
        # 设置浮点数显示模式为标准的模式
        doubleValidator.setNotation(QDoubleValidator.StandardNotation)
        # 设置浮点数精度为2位
        doubleValidator.setDecimals(2)
        # 数字和字母校验器
        # reg为正则表达式
        reg = QRegExp("[a-zA-Z0-9]+$")
        validator = QRegExpValidator()
        validator.setRegExp(reg)

        # 将校验器与输入框进行绑定
        intLineEdit.setValidator(intValidator)
        doubleLineEdit.setValidator(doubleValidator)
        validatorLineEdit.setValidator(validator)
        # 设置布局
        self.setLayout(formLayout)


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    main = QLineEditValidator()
    main.show()
    sys.exit(app.exec_())

```
 <br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647605511430-c77497f0-0f6a-47cd-90af-80a1221ae564.png#clientId=ub4e90a3e-b8bb-4&from=paste&height=133&id=u446c7ef2&originHeight=133&originWidth=237&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5380&status=done&style=none&taskId=ub7dec920-03c5-4062-9f9e-16239c206fa&title=&width=237)
<a name="mHpQu"></a>
### 使用掩码限制QLineEdit控件的输入
字符	含义<br />A	ASCII字母字符是必须输入的（A-Z，a-z）<br />a	ASCII字母字符是允许输入的，但不是必须输入的<br />N	ASCII字母字符是必须输入的（A-Z，a-z，0-9）<br />n	ASCII字母字符是允许输入的，但不是必须输入的<br />X	任何字符都是必须输入<br />x	任何字符都是允许输入的，但不是必须输入的<br />9	ASCII数字字符是必须输入的（0-9）<br />0	ASCII数字字符是允许输入的，但不是必须输入的<br />D	ASCII数字字符是必须输入的（1-9）<br />d	ASCII数字字符是允许输入的，但不是必须的（1-9）<br />#	ASCII数字字符与加减字符是允许输入的，但不是必须的<br />H	十六进制格式字符是必须输入的（A-F，a-f，0-9）<br />h	十六进制格式字符允许输入，但不是必须的<br />B	二进制格式字符是必须输入的（0,1）<br />b	二进制格式字符是允许输入的，但不是必须的<br />>	所有字母字符都大写<br /><	所有字母字符都小写<br />！	关闭大小写转换<br />\	使用‘\’转义上面列出的字符
```python
import sys
from PyQt5.QtWidgets import *


class QLIneEditMask(QWidget):
    def __init__(self):
        super(QLIneEditMask, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("用掩码限制QLineEdit控件的输入")
        formlayout = QFormLayout()

        ipLineEdit = QLineEdit()
        macLineEdit = QLineEdit()
        dateLineEdit = QLineEdit()
        licenseLineEdit = QLineEdit()
        # 为输入框设置掩码限制输入
        # 掩码中分号后面为当没有输入时默认的显示信息
        ipLineEdit.setInputMask('000.000.000.000;_')
        macLineEdit.setInputMask('HH:HH:HH:HH:HH:HH;_')
        dateLineEdit.setInputMask('0000-00-00')
        licenseLineEdit.setInputMask('>AAAAA-AAAAA-AAAAA-AAAAA-AAAAA;#')

        formlayout.addRow('数字掩码', ipLineEdit)
        formlayout.addRow('Mac掩码', macLineEdit)
        formlayout.addRow('日期掩码', dateLineEdit)
        formlayout.addRow('许可证掩码', licenseLineEdit)

        self.setLayout(formlayout)


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    main = QLIneEditMask()
    main.show()
    sys.exit(app.exec_())
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647606809007-851ef42c-6a0f-4b9a-8e27-6a9c469ece23.png#clientId=ub4e90a3e-b8bb-4&from=paste&height=159&id=udef11c6c&originHeight=159&originWidth=237&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7157&status=done&style=none&taskId=uca9aa79d-2463-428d-9a3f-3a01c6df5cd&title=&width=237)
<a name="NpcZh"></a>
### QLineEdit控件综合案例
```python
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import Qt
import sys


class QLineEditDemo(QWidget):
    def __init__(self):
        super(QLineEditDemo, self).__init__()
        self.initUI()

    def initUI(self):
        # 创建输入框1并使用int校验器
        edit1 = QLineEdit()
        edit1.setValidator(QIntValidator())
        edit1.setMaxLength(4)  # 设置最大位数
        edit1.setAlignment(Qt.AlignRight)  # 使输入框1的数值向右对齐
        edit1.setFont(QFont('Arial', 10))
        # 创建输入框2并使用double校验器
        # 这个教程中有bug，实测不能设置数字范围以及精度，因此改了一下
        # edit2.setValidator(QDoubleValidator(0.99,99,2,)) # 为输入框2设置校验器并提供数字范围以及精度为2(教程中讲的有bug)
        edit2 = QLineEdit()
        doubleValidator = QDoubleValidator()
        doubleValidator.setRange(0.99, 99)
        # 设置浮点数显示模式为标准的模式
        doubleValidator.setNotation(QDoubleValidator.StandardNotation)
        # 设置浮点数精度为2位
        doubleValidator.setDecimals(2)
        edit2.setValidator(doubleValidator)

        # 创建输入框3并使用掩码校验
        edit3 = QLineEdit()
        edit3.setInputMask("99_9999_999999;#")
        # 创建输入框4并与槽连接
        edit4 = QLineEdit()
        edit4.textChanged.connect(self.textChanged)  # 当文本改变的时候执行槽的方法
        # 创建输入框5并使用密码回显模式并与槽连接
        edit5 = QLineEdit()
        edit5.setEchoMode(QLineEdit.Password)
        edit5.editingFinished.connect(self.enterPress)  # 当文本输入时执行槽的方法
        # 创建输入框6并将输入框设置为只读模式
        edit6 = QLineEdit()
        edit6.setReadOnly(True)
        # 创建表单布局
        formlayout = QFormLayout()
        formlayout.addRow("整数校验", edit1)
        formlayout.addRow("浮点数校验", edit2)
        formlayout.addRow("Input Mask", edit3)
        formlayout.addRow("文本变化", edit4)
        formlayout.addRow("密码", edit5)
        formlayout.addRow("只读", edit6)
        self.setLayout(formlayout)
        self.setWindowTitle("QLineEdit综合案例")

    def textChanged(self, text):  # 当文本输入内容发生变化时执行
        print('输入的内容:' + text)

    def enterPress(self):
        print('已输入值')


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = QLineEditDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647611094512-9f599869-0e7e-4a33-a625-2442899e5e4a.png#clientId=ub4e90a3e-b8bb-4&from=paste&height=213&id=ub6644fee&originHeight=213&originWidth=254&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9618&status=done&style=none&taskId=u8f3467d7-1b75-404e-8395-3b41320dd60&title=&width=254)
<a name="RQfPd"></a>
## 使用QTextEdit控件输入多行文本
```python
from PyQt5.QtWidgets import *
import sys


class QTextEditDemo(QWidget):
    def __init__(self):
        super(QTextEditDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("QTextEdit控件演示")
        self.resize(300, 320)
        self.textEdit = QTextEdit()
        # 设置按钮 因为需要绑定信号与槽，所以需要使用self.来使槽能够调用属性
        buttonText = QPushButton("显示文本")
        buttonHTML = QPushButton("显示HTML")
        buttonToText = QPushButton("获取文本")
        buttonToHTML = QPushButton("获取HTML")
        # 设置垂直布局
        layout = QVBoxLayout()
        layout.addWidget(self.textEdit)
        layout.addWidget(buttonText)
        layout.addWidget(buttonToText)
        layout.addWidget(buttonHTML)
        layout.addWidget(buttonToHTML)
        self.setLayout(layout)
        # 绑定信号与槽
        buttonText.clicked.connect(self.onClick_ButtonText)
        buttonToText.clicked.connect(self.onClick_ButtonToText)
        buttonHTML.clicked.connect(self.onClick_ButtonHTML)
        buttonToHTML.clicked.connect(self.onClick_ButtonToHTML)

    def onClick_ButtonText(self):
        # 设置一般文本
        self.textEdit.setPlainText('Hello World,世界你好吗？')

    def onClick_ButtonToText(self):
        # 获取一般文本
        print(self.textEdit.toPlainText())

    def onClick_ButtonHTML(self):
        # 设置html文本 颜色为蓝色 大小为5 输出Hello World
        self.textEdit.setHtml('<font color="blue" size="5">Hello World</font>')

    def onClick_ButtonToHTML(self):
        # 获取html文本
        print(self.textEdit.toHtml())


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = QTextEditDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647666258725-6943fb4c-5e58-4542-99c9-589d525f5fcd.png#clientId=u28f4b901-98ba-4&from=paste&height=359&id=u8eace0f4&originHeight=359&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8597&status=done&style=none&taskId=u721cac9b-2515-4023-9fbf-d307f09f146&title=&width=316)
<a name="zczSK"></a>
## 按钮控件
按钮控件有<br />QPushButton 普通按钮<br />AToolButton 工具条按钮<br />QRadioButton 单选按钮<br />QCheckBox 复选框
<a name="lM0uU"></a>
### QPushButton
使用lambda表达式，可以在连接信号与槽时，将信号自身的信息作为参数传递给槽

也可以通过sender来获得信号自身的信息（这样还不需要定义为成员变量了。）<br />举例：<br />self.button1.clicked.connect(lambda: self.whichButton(self.button1))改成<br />button1.clicked.connect(self.whichButton)<br />whichButton函数中通过<br /># 得到发送信号的对象<br />sender = self.sender()<br /># sender.text为发送信号的对象的名字<br />print(sender.text() + '按钮被按下')<br />这里的from PyQt5.QtCore import *好像并没有什么用
```python
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *
import sys


class QPushButtonDemo(QDialog):
    def __init__(self):
        super(QPushButtonDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("QPushButtonDemo")
        layout = QVBoxLayout()
        # 创建按钮1,设置为成员变量是因为其他函数需要调用
        self.button1 = QPushButton('第一个按钮')
        self.button1.setText('First Button1')
        # 设置按钮1的check属性
        self.button1.setCheckable(True)
        # 设置按钮处于选中状态
        self.button1.toggle()
        # 单击按钮时调用方法
        self.button1.clicked.connect(self.buttonState)
        # 之所以使用lambda函数是因为clicked返回的是bool类型的，调用的方法使用的是字符串类型
        # 使用lamba函数可以将按钮的信息作为参数传给槽
        self.button1.clicked.connect(lambda: self.whichButton(self.button1))
        layout.addWidget(self.button1)
        # 创建按钮2
        button2 = QPushButton("图像按钮")
        # 教程中设置图像按钮时是button2.setIcon(QIcon(QPixmap('./images/bool.png')))但是跟这个没什么区别
        button2.setIcon(QIcon('./images/bool.png'))
        button2.clicked.connect(lambda: self.whichButton(button2))
        layout.addWidget(button2)
        # 创建按钮3 将按钮3设置为不可用的按钮
        button3 = QPushButton("不可用的按钮")
        button3.setEnabled(False)
        layout.addWidget(button3)
        # 创建按钮4 将按钮4设置为默认按钮并设置热键通过alt+m可以快速调用
        button4 = QPushButton("&MyButton")
        button4.setDefault(True)
        button4.clicked.connect(lambda: self.whichButton(button4))
        layout.addWidget(button4)
        self.setLayout(layout)
        self.resize(400, 300)

    def buttonState(self):
        if self.button1.isChecked():
            print('按钮1已经被选中')
        else:
            print('按钮1未被选中')

    def whichButton(self, btn):
        # btn为使用此方法的按钮信息，通过lambda函数传入
        print("被单击的按钮是<" + btn.text() + '>')


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = QPushButtonDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647673938430-c31da309-2dbc-49d7-9ae6-960285bacd1e.png#clientId=u28f4b901-98ba-4&from=paste&height=339&id=u63da6496&originHeight=339&originWidth=416&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11689&status=done&style=none&taskId=ud11314c3-130e-4dbc-9c84-add94d8fdd1&title=&width=416)
<a name="L4I75"></a>
### QRadioButton
<br />单选按钮：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647674234735-309c9635-df44-4d07-ae00-724b5dc6f3f4.png#clientId=u28f4b901-98ba-4&from=paste&height=109&id=uf21e659a&originHeight=109&originWidth=264&originalType=binary&ratio=1&rotation=0&showTitle=false&size=35253&status=done&style=none&taskId=u2c677f32-9091-4804-b6e5-e2a2f25159d&title=&width=264)<br />单选按钮需要放在一个容器里，这样它们之间才能产生联系<br />这里from PyQt5.QtGui import *<br />from PyQt5.QtCore import *<br />也是没什么用
```python
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *
import sys


class QRadioButtonDemo(QWidget):
    def __init__(self):
        super(QRadioButtonDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("QRadioButton")
        layout = QHBoxLayout()

        button1 = QRadioButton('单选按钮1')
        # 将单选按钮1设置为默认选中
        button1.setChecked(True)
        # 选中单选按钮1时执行buttonState方法
        button1.toggled.connect(self.buttonState)
        layout.addWidget(button1)

        button2 = QRadioButton("单选按钮2")
        button2.toggled.connect(self.buttonState)
        layout.addWidget(button2)
        self.setLayout(layout)

    def buttonState(self):
        # 使用radioButton变量存放发送者的信息
        radioButton = self.sender()
        if radioButton.isChecked() == True :
            print('<'+radioButton.text()+'>被选中')
        else :
            print('<'+radioButton.text()+'>被取消选中状态')


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = QRadioButtonDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647677957043-dcced7dc-d016-48de-b23b-3a1502390c6f.png#clientId=u28f4b901-98ba-4&from=paste&height=77&id=u541d5106&originHeight=77&originWidth=198&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3343&status=done&style=none&taskId=u59331d03-e94a-4d3a-8503-bafa1179d7d&title=&width=198)
<a name="aBRqm"></a>
### QCheckBox
QCheckBox控件有三种状态<br />未选中:0   半选中:1   选中:2<br />这三种状态可以通过checkState方法来获取到<br />要想拥有半选中状态需要为定义的复选框使用setTristate(True)方法.
```python
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *
import sys


class QCheckBoxDemo(QWidget):
    def __init__(self):
        super(QCheckBoxDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("复选框控件演示")
        # 创建水平布局
        layout = QHBoxLayout()
        # 创建复选框1
        self.checkBox1 = QCheckBox('复选框控件1')
        self.checkBox1.setChecked(True)
        self.checkBox1.stateChanged.connect(lambda: self.checkBoxState(self.checkBox1))
        layout.addWidget(self.checkBox1)
        # 创建复选框2
        self.checkBox2 = QCheckBox('复选框控件2')
        self.checkBox2.stateChanged.connect(lambda: self.checkBoxState(self.checkBox1))
        layout.addWidget(self.checkBox2)
        # 创建复选框3
        self.checkBox3 = QCheckBox('半选中')
        self.checkBox3.setTristate(True)  # 设置复选框3能够处于半选中状态
        self.checkBox3.setCheckState(Qt.PartiallyChecked)  # 设置复选框3初始为半选中状态
        self.checkBox3.stateChanged.connect(lambda: self.checkBoxState(self.checkBox1))
        layout.addWidget(self.checkBox3)

        self.setLayout(layout)

    def checkBoxState(self, cb):
        """
        输出三个复选框的的名字加上是否被选中加上选择的状态(0,1,2)
        :param cb:
        :return:
        """
        check1Status = self.checkBox1.text() + ',isChecked=' + str(self.checkBox1.isChecked()) + ',checkState=' + str(
            self.checkBox1.checkState()) + '\n'
        check2Status = self.checkBox2.text() + ',isChecked=' + str(self.checkBox2.isChecked()) + ',checkState=' + str(
            self.checkBox2.checkState()) + '\n'
        check3Status = self.checkBox3.text() + ',isChecked=' + str(self.checkBox3.isChecked()) + ',checkState=' + str(
            self.checkBox3.checkState()) + '\n'
        print(check1Status + check2Status + check3Status)


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = QCheckBoxDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647681221592-9a1414c8-a22e-47b2-a459-bb8f2666f237.png#clientId=u28f4b901-98ba-4&from=paste&height=77&id=u39dc109f&originHeight=77&originWidth=287&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4775&status=done&style=none&taskId=u647fa383-42d1-4659-9ce6-5abf6573b6d&title=&width=287)
<a name="B2ijm"></a>
## 下拉列表控件(QComboBox)
下拉列表属于这种![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647681358516-aa5cf54c-8d6a-476f-bb78-9d387bf4f12a.png#clientId=u28f4b901-98ba-4&from=paste&height=238&id=u543a692b&originHeight=238&originWidth=365&originalType=binary&ratio=1&rotation=0&showTitle=false&size=89913&status=done&style=none&taskId=udbe1e715-0b02-4a22-9d7b-afc5a11cdd7&title=&width=365)<br />这节学习

1. 如何将列表项添加到QComboBox控件中
2. 如何获取选中的列表项
```python
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *
import sys


class QCheckBoxDemo(QWidget):
    def __init__(self):
        super(QCheckBoxDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("下拉列表控件演示")
        self.resize(300, 100)
        layout = QVBoxLayout()
        self.label = QLabel("请选择编程语言")  # 标签的默认文本
        self.cb = QComboBox()  # 创建下拉列表
        # 为列表添加单项
        self.cb.addItem('C++')
        self.cb.addItem('Python')
        # 为列表添加多项
        self.cb.addItems(['Java', 'C#', 'Ruby'])
        # 当列表选项改变时发出信号执行槽
        self.cb.currentIndexChanged.connect(self.selectionChange)
        layout.addWidget(self.label)
        layout.addWidget(self.cb)
        self.setLayout(layout)

    def selectionChange(self, i):  # 默认传递两个参数,第二个i对应的是选项的索引值
        # 将标签设置为列表的当前选项文本并调整文字大小.
        self.label.setText(self.cb.currentText())
        self.label.adjustSize()
        for count in range(self.cb.count()):  # 遍历输出列表中的选项序号与文本
            print('item' + str(count) + '=' + self.cb.itemText(count))
        print('current index', i, 'selection changed', self.cb.currentText())  # 输出当前选择的选项文本


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = QCheckBoxDemo()
    main.show()
    sys.exit(app.exec_())

```
效果:<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647687903514-08797613-40a3-454f-9b8d-d89cfbe3fde1.png#clientId=u28f4b901-98ba-4&from=paste&height=139&id=ua94889d6&originHeight=139&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4976&status=done&style=none&taskId=u1a9cd5ed-5498-49d6-a7a0-b6ac308b95b&title=&width=316)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647687918905-ce231147-15a8-4117-9286-47f81ec969ea.png#clientId=u28f4b901-98ba-4&from=paste&height=196&id=u400ca2fa&originHeight=196&originWidth=582&originalType=binary&ratio=1&rotation=0&showTitle=false&size=21687&status=done&style=none&taskId=u6341eb52-6fe5-4107-8794-30cbb9479aa&title=&width=582)
<a name="DQh0H"></a>
## 滑块控件(QSlider)
```python
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *
import sys


class QSliderDemo(QWidget):
    def __init__(self):
        super(QSliderDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("滑块控件演示")
        self.resize(300, 700)
        layout = QVBoxLayout()
        self.label = QLabel('你好 PyQt5')
        self.label.setAlignment(Qt.AlignCenter)
        layout.addWidget(self.label)

        slider = QSlider(Qt.Horizontal)  # 创建水平滑块
        slider.setMinimum(12)  # 设置最小值
        slider.setMaximum(48)  # 设置最大值
        slider.setSingleStep(3)  # 设置步长
        slider.setValue(18)  # 设置初始值
        slider.setTickPosition(QSlider.TicksBelow)  # 设置刻度的位置在滑块下方
        slider.setTickInterval(6)  # 设置刻度的间隔
        slider.valueChanged.connect(self.valueChange)
        layout.addWidget(slider)

        slider1 = QSlider(Qt.Vertical)  # 创建竖直滑块
        slider1.setMinimum(10)
        slider1.setMaximum(60)
        slider1.setSingleStep(5)
        slider1.setValue(30)
        slider1.setTickPosition(QSlider.TicksLeft)  # 设置竖直滑块的刻度的位置在滑块左边
        slider1.setTickInterval(2)  # 设置刻度的间隔
        slider1.valueChanged.connect(self.valueChange)
        layout.addWidget(slider1)

        self.setLayout(layout)

    def valueChange(self):
        print('当前值:%s' % self.sender().value())
        size = self.sender().value()
        self.label.setFont(QFont('Arial', size))  # 通过滑块的值的改变来改变字体的大小


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = QSliderDemo()
    main.show()
    sys.exit(app.exec_())

```
效果:![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647690764835-6ed3c0db-a0d7-419d-9efa-5f9cf623c992.png#clientId=u28f4b901-98ba-4&from=paste&height=739&id=u8679cdc2&originHeight=739&originWidth=440&originalType=binary&ratio=1&rotation=0&showTitle=false&size=22247&status=done&style=none&taskId=u3dab22f9-0243-40bc-bcf5-14ecd6a967a&title=&width=440)竖直滑块和水平滑块都能够更改Qlabel(你好PyQt5)的大小
<a name="S5oPZ"></a>
## 计数器控件(QSpinBox)(翻译结果是选值框)


```python
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *
import sys


class QSpinBoxDemo(QWidget):
    def __init__(self):
        super(QSpinBoxDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("滑块控件演示")
        self.resize(300, 100)
        layout = QVBoxLayout()

        self.label = QLabel('当前值')
        self.label.setAlignment(Qt.AlignCenter)
        layout.addWidget(self.label)

        spinbox = QSpinBox()  # 创建计数器
        spinbox.setValue(18)  # 设置初始值
        spinbox.setRange(10, 999)  # 设置计数器的范围
        spinbox.setSingleStep(3)  # 设置步长
        spinbox.valueChanged.connect(self.valueChange)  # 当计数器数值改变时执行valueChange方法
        layout.addWidget(spinbox)

        self.setLayout(layout)

    def valueChange(self):
        self.label.setText('当前值:%s' % self.sender().value())


if __name__ == '__main__':
    # app为软件类的对象
    app = QApplication(sys.argv)
    # main为窗口类的对象
    main = QSpinBoxDemo()
    main.show()
    sys.exit(app.exec_())

```
效果:![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647692991619-40d975a6-0d7b-4afd-a980-11bfc3498eb2.png#clientId=u28f4b901-98ba-4&from=paste&height=135&id=ub775bccf&originHeight=135&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4294&status=done&style=none&taskId=u368719d1-cbb4-428e-ac2f-b3db56c2350&title=&width=316)
<a name="rlcBp"></a>
## 对话框
对话框的分类:

- QMessageBox 消息对话框
- QColorDialog 颜色对话框
- QFileDialog 文件的打开与保存
- QFontDialog 设置字体的对话框
- QInputDialog 获取用户输入信息的对话框

新建的对话框的类都需要继承QDialog<br />对话框的特点是没有菜单栏,对话框可以设置为执行时不能进行同一软件下对话框之外的操作
<a name="aKlYl"></a>
### 使用QDialog显示通用对话框
```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *


class QDialogDemo(QMainWindow):
    def __init__(self):
        super(QDialogDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle('QDialog案例')
        self.resize(300, 200)
        button = QPushButton(self)
        button.setText('弹出对话框')
        button.move(50, 50)
        button.clicked.connect(self.showDialog)


    def showDialog(self):
        # 创建对话框
        dialog = QDialog()
        button = QPushButton('确定', dialog)  # 为dialog（对话框）添加按钮控件
        button.clicked.connect(dialog.close)  # 点击对话框的按钮时关闭对话框
        button.move(50, 50)
        dialog.setWindowTitle('对话框')
        dialog.setWindowModality(Qt.ApplicationModal)  # 使出现对话框时，其他窗口不可使用
        dialog.exec()


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = QDialogDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647741798473-304c1759-7878-4540-b88b-fd28dccff625.png#clientId=u4e370659-cca8-4&from=paste&height=288&id=uae488d51&originHeight=288&originWidth=537&originalType=binary&ratio=1&rotation=0&showTitle=false&size=20282&status=done&style=none&taskId=u624b1c3e-8214-4ca7-be9e-9b9676a9bc0&title=&width=537)
<a name="qzS3i"></a>
### QMessageBox信息对话框
看这个知乎链接[https://zhuanlan.zhihu.com/p/29795495](https://zhuanlan.zhihu.com/p/29795495)比教程详细多了<br />有多种不同类型的对话框

- 关于对话框   QMessageBox.about
- 错误对话框   QMessageBox.critical
- 警告对话框   QMessageBox.warning
- 提问对话框   QMessageBox.question
- 消息对话框   QMessageBox.information

有两点差异

1. 显示的对话框图标可能不同
2. 显示的按钮是不一样的（关于对话框一般显示1个按钮，其他对话框一般显示2个）

```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *


class QMessageBoxDemo(QWidget):
    def __init__(self):
        super(QMessageBoxDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle('QDialog案例')
        self.resize(300, 400)
        layout = QVBoxLayout()

        button1 = QPushButton()
        button1.setText('显示关于对话框')
        button1.clicked.connect(self.showDialog)

        button2 = QPushButton()
        button2.setText('显示消息对话框')
        button2.clicked.connect(self.showDialog)

        button3 = QPushButton()
        button3.setText('显示警告对话框')
        button3.clicked.connect(self.showDialog)

        button4 = QPushButton()
        button4.setText('显示错误对话框')
        button4.clicked.connect(self.showDialog)

        button5 = QPushButton()
        button5.setText('显示提问对话框')
        button5.clicked.connect(self.showDialog)

        layout.addWidget(button1)
        layout.addWidget(button2)
        layout.addWidget(button3)
        layout.addWidget(button4)
        layout.addWidget(button5)

        self.setLayout(layout)

    def showDialog(self):
        text = self.sender().text()
        if text == "显示关于对话框":
            reply = QMessageBox.about(self, '关于', '这是一个关于对话框')  # 弹出一个关于对话框，第二个参数为对话框的标题，第三个参数为对话框的内容
            print(reply == QMessageBox.Yes)
        elif text == "显示消息对话框":
            QMessageBox.information(self, '消息', '这是一个消息对话框', QMessageBox.Yes | QMessageBox.No, QMessageBox.Yes)  # 这个QMessageBox.Yes | QMessageBox.No意思是他有Yes和No按钮，最后的QMessageBox.Yes的意思是默认选择Yes

        elif text == "显示警告对话框":
            QMessageBox.warning(self, '警告', '这是一个警告对话框', QMessageBox.Yes | QMessageBox.No, QMessageBox.Yes)

        elif text == "显示错误对话框":
            QMessageBox.critical(self, '错误', '这是一个错误对话框', QMessageBox.Yes | QMessageBox.No, QMessageBox.Yes)

        elif text == "显示提问对话框":
            QMessageBox.question(self, '提问', '这是一个提问对话框', QMessageBox.Yes | QMessageBox.No, QMessageBox.Yes)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = QMessageBoxDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647744675657-38e04312-6d78-4736-b387-d94c844aae1b.png#clientId=u4e370659-cca8-4&from=paste&height=439&id=u6aa76e96&originHeight=439&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12295&status=done&style=none&taskId=uc7bf08e8-d755-4bf8-98c0-861c5f5aceb&title=&width=316)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647744665719-d11a4070-2e87-4aa0-b421-84de38f8ae24.png#clientId=u4e370659-cca8-4&from=paste&height=124&id=u4735fea4&originHeight=124&originWidth=167&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4122&status=done&style=none&taskId=u9db41eee-e5b2-4889-801f-d3e7a5c3f4a&title=&width=167)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647744636330-1fa61872-5620-436f-b3d2-d3e6c3a79a6a.png#clientId=u4e370659-cca8-4&from=paste&height=133&id=u51e0392d&originHeight=133&originWidth=197&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5211&status=done&style=none&taskId=u262e5d4d-6027-40cd-bc53-beb2c6d61bd&title=&width=197)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647744650821-aa9632f1-b2fd-4f5b-8e9d-3550d6fa9809.png#clientId=u4e370659-cca8-4&from=paste&height=133&id=ud1708086&originHeight=133&originWidth=197&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4795&status=done&style=none&taskId=u46a9af48-89a3-4d14-acde-01f54d6b6c0&title=&width=197)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647744686758-64c78887-f3f0-42e6-848e-c87334ad87e9.png#clientId=u4e370659-cca8-4&from=paste&height=133&id=ud77c6196&originHeight=133&originWidth=197&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5094&status=done&style=none&taskId=u030437d5-a97a-4e63-8a85-e5af483005a&title=&width=197)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647744691455-7d25c925-f16a-4ce9-bd0c-1bd5aa2a56ef.png#clientId=u4e370659-cca8-4&from=paste&height=133&id=u0e42e3ce&originHeight=133&originWidth=197&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5758&status=done&style=none&taskId=u1145ecb2-47f8-40ec-a15b-47c94863224&title=&width=197)
<a name="cINki"></a>
### QInputDialog输入对话框
输入对话框，特点是允许显示带输入的控件，例如输入列表，输入文本，输入整数（计数器）

- QInputDialog.getItem 显示输入列表（QComboBox）
- QInputDialog.getText 显示输入文本
- QInputDialog.getInt 显示输入整数（计数器）
```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *


class QInputDialogDemo(QWidget):
    def __init__(self):
        super(QInputDialogDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle('输入对话框')
        layout = QFormLayout()

        button1 = QPushButton('获取列表中的选项')
        button1.clicked.connect(self.getItem)
        self.lineEdit1 = QLineEdit()
        layout.addRow(button1, self.lineEdit1)

        button2 = QPushButton('获取字符串')
        button2.clicked.connect(self.getText)
        self.lineEdit2 = QLineEdit()
        layout.addRow(button2, self.lineEdit2)

        button3 = QPushButton('获取整数')
        button3.clicked.connect(self.getInt)
        self.lineEdit3 = QLineEdit()
        layout.addRow(button3, self.lineEdit3)

        self.setLayout(layout)

    def getItem(self):
        items = ('C', 'C++', 'Ruby', 'Python', 'Java',)
        # 使用两个数接收QInputDialog.getItem的返回值，因为这个方法的返回值是一个元组，下方的同理
        item, ok = QInputDialog.getItem(self, '请选择编程语言', '语言列表', items)
        if ok and item:
            self.lineEdit1.setText(item)

    def getText(self):
        text, ok = QInputDialog.getText(self, '文本输入框', '输入姓名')
        if ok and text:
            self.lineEdit2.setText(text)

    def getInt(self):
        num, ok = QInputDialog.getInt(self, '整数输入框', '输入数字')
        if ok and num:
            self.lineEdit3.setText(str(num))



if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = QInputDialogDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647750584476-10029fd1-af45-455e-97b6-630f8623feac.png#clientId=u4e370659-cca8-4&from=paste&height=146&id=ud1c0fd75&originHeight=146&originWidth=457&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10933&status=done&style=none&taskId=uf5b7730f-3662-4dcc-a46e-4211c2b423d&title=&width=457)
<a name="rC3c8"></a>
### QFontDialog字体对话框
字体对话框，显示字体列表，用于进行字体的设置。
```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *
class QFontDialogDemo(QWidget):
    def __init__(self):
        super(QFontDialogDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle('Font Dialog例子')
        layout = QVBoxLayout()
        self.fontButton = QPushButton("选择字体")
        self.fontButton.clicked.connect(self.getFont)

        layout.addWidget(self.fontButton)

        self.fontLabel = QLabel("Hello,测试字体例子")

        layout.addWidget(self.fontLabel)

        self.setLayout(layout)
        self.resize(300,200)

    def getFont(self):
        # QFontDialog.getFont返回值为一个元组，第一个数为字体，第二个数为布尔类型。
        font, ok = QFontDialog.getFont()
        if ok :
            self.fontLabel.setFont(font)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = QFontDialogDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647752794901-d5404c4d-312d-4bbe-a346-00d47c7c056c.png#clientId=u4e370659-cca8-4&from=paste&height=401&id=u27b3dcfa&originHeight=401&originWidth=808&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33819&status=done&style=none&taskId=u25642424-1e4f-4208-8b23-66e084eb255&title=&width=808)
<a name="GbkBU"></a>
### QColorDialog 颜色对话框
```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *


class QFontDialogDemo(QWidget):
    def __init__(self):
        super(QFontDialogDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle('Color Dialog例子')
        layout = QVBoxLayout()

        self.colorButton = QPushButton('设置字体颜色')
        self.colorButton.clicked.connect(self.getColor)
        layout.addWidget(self.colorButton)

        self.colorButton1 = QPushButton('设置背景颜色')
        self.colorButton1.clicked.connect(self.getBGColor)
        layout.addWidget(self.colorButton1)

        self.colorlabel = QLabel('Hello,测试颜色例子')
        layout.addWidget(self.colorlabel)

        self.setLayout(layout)
        self.resize(300, 200)

    def getColor(self):
        color = QColorDialog.getColor()  # color为弹出选择的颜色对话框
        p = QPalette()  # 创建调色板对象
        p.setColor(QPalette.WindowText, color)  # 调色板存取颜色对话框中选择的颜色并将其应用于文字
        self.colorlabel.setPalette(p)  # 设置调色板应用的控件

    def getBGColor(self):
        color = QColorDialog.getColor()  # color为弹出选择的颜色对话框
        p = QPalette()  # 创建调色板对象
        p.setColor(QPalette.Window, color)  # 调色板存取颜色对话框中选择的颜色并将其应用于控件背景
        self.colorlabel.setAutoFillBackground(True)  # 设置标签控件背景能够被设置颜色
        self.colorlabel.setPalette(p)  # 设置调色板应用的控件


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = QFontDialogDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647759831393-b97cfeaf-fdde-47f9-923b-fd3ce889f0de.png#clientId=u4e370659-cca8-4&from=paste&height=429&id=u7f78f7c7&originHeight=429&originWidth=823&originalType=binary&ratio=1&rotation=0&showTitle=false&size=116263&status=done&style=none&taskId=uc1526a67-6b59-4e06-b8a1-2cc085d14ef&title=&width=823)
<a name="IEm5r"></a>
### QFileDialog 文件对话框
```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *


class QColorDialogDemo(QWidget):
    def __init__(self):
        super(QColorDialogDemo, self).__init__()
        self.initUI()

    def initUI(self):
        layout = QVBoxLayout()

        self.button1 = QPushButton('加载图片')
        self.button1.clicked.connect(self.loadImage)
        layout.addWidget(self.button1)

        self.imageLabel = QLabel()  # 负责显示选择的图标文件
        layout.addWidget(self.imageLabel)

        self.button2 = QPushButton('加载文本文件')
        self.button2.clicked.connect(self.loadText)
        layout.addWidget(self.button2)

        self.contents = QTextEdit()  # 负责显示文本文件 显示多行文本
        layout.addWidget(self.contents)

        self.setWindowTitle('文件对话框演示')
        self.setLayout(layout)

    def loadImage(self):
        # 其中'打开文件'设置的是文件框的窗口标题，'.'的意思是从默认初始路径为当前路径，第三个设置的是选用的文件格式（注释加格式）
        # getOpenFileName 返回的是两个值 第一个值为选择的路径，第二个值为文件格式（注释加格式）
        frame, _ = QFileDialog.getOpenFileName(self, '打开文件', '.', '图像文件(*.jpg *.png)')
        self.imageLabel.setPixmap(QPixmap(frame))

    def loadText(self):
        dialog = QFileDialog()
        dialog.setFileMode(QFileDialog.AnyFile)  # 设置文件的打开格式
        dialog.setFilter(QDir.Files)
        if dialog.exec():  # 显示对话框
            filenames = dialog.selectedFiles()  
            # f指定的是选中的文件中的第一个，编码为utf-8，模式是r
            f = open(filenames[0], encoding='utf-8', mode='r')  
            # 使用 with as 操作已经打开的文件对象（本身就是上下文管理器），
            # 无论期间是否抛出异常，都能保证 with as 语句执行完毕后自动关闭已经打开的文件。
            with f:  
                data = f.read()
                self.contents.setText(data)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = QColorDialogDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647764805681-988c3af1-4dee-4849-b1f9-476de90c6765.png#clientId=u4e370659-cca8-4&from=paste&height=524&id=u0157be5e&originHeight=524&originWidth=1269&originalType=binary&ratio=1&rotation=0&showTitle=false&size=83035&status=done&style=none&taskId=u96b03aec-8283-4eba-b859-d107c944518&title=&width=1269)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647763166488-5027d991-4de4-4399-8478-cf23db7c262b.png#clientId=u4e370659-cca8-4&from=paste&height=540&id=ua15c1b1f&originHeight=540&originWidth=960&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42346&status=done&style=none&taskId=ueb0bce77-bee5-4b3c-a04a-d376d706163&title=&width=960)
<a name="YgXBD"></a>
## 绘图API
绘图API包括

- 文本
- 各种图形（直线，点，椭圆，弧，扇形，多边形等）
- 图像

框架：<br />所有的方法都是在QPainter这个类中，因此框架就是<br />painter = QPainter（）

painter.bengin（）

绘制内容

painter.end（）

必须在painterEvent事件方法中绘制各种元素（当窗口放大和缩小时都需要重新绘制，窗口方法和缩小时都会自动调用painterEvent事件）
<a name="CdmTU"></a>
### DrawText在窗口上绘制文本
```python
import sys
from PyQt5.QtWidgets import QApplication,QWidget
from PyQt5.QtGui import QPainter,QColor,QFont
from PyQt5.QtCore import Qt

class DrawText(QWidget) :
    def __init__(self):
        super(DrawText, self).__init__()
        self.setWindowTitle('在窗口上绘制文本')
        self.resize(500,400)
        self.text = "Python从菜鸟到高手"

    def paintEvent(self, event):
        painter = QPainter(self)
        painter.begin(self)
        painter.setPen(QColor(150,43,5)) # 设置画笔
        painter.setFont(QFont('SimSun',25)) # 设置字体
        # 实现绘画字体的方法，第一个为绘制区域，第二个为绘制的对齐模式（居中），第三个为绘制的内容
        painter.drawText(event.rect(),Qt.AlignCenter,self.text)
        painter.end()

if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = DrawText()
    main.show()
    sys.exit(app.exec_())
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647767314230-fcaa2055-526c-4024-90c9-e1f8c9ebec69.png#clientId=u4e370659-cca8-4&from=paste&height=439&id=u06ff6d5e&originHeight=439&originWidth=516&originalType=binary&ratio=1&rotation=0&showTitle=false&size=15033&status=done&style=none&taskId=u97b34c7e-c726-4916-bc66-77528dfe7ea&title=&width=516)
<a name="Y2Fsg"></a>
### DrawPoint在窗口上绘制正弦曲线
```python
import sys, math
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import Qt


class DrawPoints(QWidget):
    def __init__(self):
        super(DrawPoints, self).__init__()
        self.resize(300, 300)
        self.setWindowTitle("在窗口上用像素点绘制两个周期的正弦曲线")

    def paintEvent(self, event):
        painter = QPainter()
        painter.begin(self)
        painter.setPen(Qt.blue)
        size = self.size()
        for i in range(1000):  # 1000次循环，绘制1000个点
            # 计算绘图点的坐标（x,y）
            x = int(100 * (-1 + 2.0 * i / 1000) + size.width() / 2.0)
            y = int(-50 * math.sin((x - size.width() / 2.0) * math.pi / 50) + size.height() / 2.0)
            painter.drawPoint(x, y)

        painter.end()


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = DrawPoints()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647780741419-ff4d4c54-22bb-4ac5-bbb4-65ee2fddd08a.png#clientId=u4e370659-cca8-4&from=paste&height=339&id=u8768c8ad&originHeight=339&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8291&status=done&style=none&taskId=u42252bea-bea1-48fc-bf31-f58963d8333&title=&width=316)
<a name="CX3Jr"></a>
## 拖动和剪贴板操作
**拖动：**<br />将A控件拖入到B： 将A设置为可拖动，将B设置为可以接收其他控件的拖动<br />A.setDragEnabled(True)<br />B.setAcceptDrops(True)<br />对于接收拖动的控件B需要两个事件<br />1.dragEnterEvent 将A拖到B触发<br />2.dropEvent         在B的区域放下A时触发
```python
import sys, math
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *

class MyComboBox(QComboBox) :  # 定义为可以接收拖拽的下拉列表控件
    def __init__(self):
        super(MyComboBox, self).__init__()
        self.setAcceptDrops(True)  #  将此控件设置为可接受拖动

    def dragEnterEvent(self, e):
        print(e)
        if e.mimeData().hasText():  # 判断拖拽内容是否存在文本
            e.accept()  # 接收文本
        else :
            e.ignore()  #  忽略
    def dropEvent(self, e):
        self.addItem(e.mimeData().text()) # 添加文本

class DrapDropDemo(QWidget) :
    def __init__(self):
        super(DrapDropDemo, self).__init__()
        formlayout = QFormLayout()
        formlayout.addRow(QLabel("请将左边的文本拖拽到右边的下拉列表中"))

        lineEdit = QLineEdit()
        lineEdit.setDragEnabled(True)  # 让文本输入框可被拖动
        combo = MyComboBox()
        formlayout.addRow(lineEdit,combo)
        self.setLayout(formlayout)
        self.setWindowTitle("拖拽案例")


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = DrapDropDemo()
    main.show()
    sys.exit(app.exec_())
```
效果：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647932457628-30bd9cbe-0913-45b0-b306-6b8d99b5a4eb.png#clientId=u633cd362-899e-4&from=paste&height=129&id=u7af95515&originHeight=129&originWidth=243&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5566&status=done&style=none&taskId=u5184f5a0-ba43-49d2-af4e-3e28bbfe4df&title=&width=243)<br />**使用剪贴板**
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class ClipBoard(QDialog):
    def __init__(self):
        super(ClipBoard, self).__init__()
        textCopyButton = QPushButton('复制文本')
        textPasteButton = QPushButton('粘贴文本')
        htmlCopyButton = QPushButton('复制HTML')
        htmlPasteButton = QPushButton('粘贴HTML')
        imageCopyButton = QPushButton('复制图像')
        imagePasteButton = QPushButton('粘贴图像')
        self.textLabel = QLabel('默认文本')
        self.imageLabel = QLabel()
        self.imageLabel.setPixmap(QPixmap('./images/bool.png'))

        layout = QGridLayout()
        layout.addWidget(textCopyButton, 0, 0)
        layout.addWidget(imageCopyButton, 0, 1)
        layout.addWidget(htmlCopyButton, 0, 2)
        layout.addWidget(textPasteButton, 1, 0)
        layout.addWidget(imagePasteButton, 1, 1)
        layout.addWidget(htmlPasteButton, 1, 2)
        layout.addWidget(self.textLabel, 2, 0, 1, 2)
        layout.addWidget(self.imageLabel, 2, 2)
        self.setLayout(layout)

        textCopyButton.clicked.connect(self.copyText)
        textPasteButton.clicked.connect(self.pasteText)
        htmlCopyButton.clicked.connect(self.copyHtml)
        htmlPasteButton.clicked.connect(self.pasteHtml)
        imageCopyButton.clicked.connect(self.copyImage)
        imagePasteButton.clicked.connect(self.pasteImage)
        self.setWindowTitle('剪贴板演示')

    def copyText(self):
        clipboard = QApplication.clipboard()  # 创建剪贴板对象
        clipboard.setText('hello world')  # 设置剪贴板的内容

    def pasteText(self):
        clipboard = QApplication.clipboard()
        self.textLabel.setText(clipboard.text())  # 将剪贴板内容赋予文字标签

    def copyImage(self):
        clipboard = QApplication.clipboard()
        clipboard.setPixmap(QPixmap('../images/bool.png')) # 教程中是一个“.”但是只有是“..”才能正常复制粘贴

    def pasteImage(self):
        clipboard = QApplication.clipboard()
        self.imageLabel.setPixmap(clipboard.pixmap())

    def copyHtml(self):
        mimeData = QMimeData()  # 创建特殊数据类型对象
        mimeData.setHtml('<b>Bold and <font color=red>Red</font></b>')
        clipboard = QApplication.clipboard()
        clipboard.setMimeData(mimeData)

    def pasteHtml(self):
        clipboard = QApplication.clipboard()
        mimeData = clipboard.mimeData()
        if mimeData.hasHtml():
            self.textLabel.setText(mimeData.html())


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = ClipBoard()
    main.show()
    sys.exit(app.exec_())

```


** **![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647947572643-536a80a1-64ea-4e9e-a3e1-6c50bd743c4d.png#clientId=uee23daa4-d12d-4&from=paste&height=319&id=u774e6f72&originHeight=319&originWidth=400&originalType=binary&ratio=1&rotation=0&showTitle=false&size=21320&status=done&style=none&taskId=u438e5d60-6d62-4a70-9d74-ebadda2d29a&title=&width=400)
<a name="Zq2O3"></a>
## 菜单栏、工具栏和状态栏
<a name="Mkc71"></a>
### 菜单栏
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class Menu(QMainWindow):
    def __init__(self):
        super(Menu, self).__init__()
        bar = self.menuBar()  # 得到窗口的菜单栏
        file = bar.addMenu("文件")  # 为菜单栏添加菜单
        file.addAction("新建")  # 为菜单添加子菜单
        save = QAction("保存", self)  # 另一种创建菜单的方式，self代表的是当前窗口
        save.setShortcut("Ctrl + S")  # 为菜单设置快捷键
        file.addAction(save)  # 将save设置为file的子菜单
        save.triggered.connect(self.process)  # 当触发save菜单时执行process
        quit = QAction("退出", self)
        file.addAction(quit)
        edit = bar.addMenu("Edit")
        edit.addAction("copy")
        edit.addAction("paste")
        self.resize(300, 200)

    def process(self, a):
        print(self.sender().text())


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = Menu()
    main.show()
    sys.exit(app.exec_())

```
效果：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647951107335-180f6843-86a1-4e80-87fe-d440fdf9f102.png#clientId=uee23daa4-d12d-4&from=paste&height=235&id=u124d5d69&originHeight=235&originWidth=352&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7917&status=done&style=none&taskId=udba9a388-9b50-4866-9a88-ac5f16f3601&title=&width=352)点击保存后会执行自定义的process函数输出“保存”
<a name="rDrsx"></a>
### 工具栏
工具栏是这样的![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647954376192-ec8a5f93-e51e-4a96-bac9-19ee9db06ec1.png#clientId=uee23daa4-d12d-4&from=paste&height=212&id=u6b3eaf18&originHeight=212&originWidth=364&originalType=binary&ratio=1&rotation=0&showTitle=false&size=43881&status=done&style=none&taskId=u441fd563-a655-4305-8806-300ead5c7a5&title=&width=364)<br />工具栏有三种显示方式

1. 只显示图标
2. 只显示文本
3. 同时显示文本和图标

ToolButtonIconOnly  只显示图标<br />ToolButtonTextOnly   只显示文本<br />ToolButtonTextBesideIcon   文本显示在图标旁边<br />ToolButtonTextUnderIcon   文本显示在图标下边<br />ToolButtonFollowStyle 默认模式，文本作为图标的提示出现<br />设置显示方式：<br />tb2.setToolButtonStyle(Qt.ToolButtonTextUnderIcon)
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class ToolBar(QMainWindow):
    def __init__(self):
        super(ToolBar, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle('工具栏例子')
        self.resize(300, 200)
        tb1 = self.addToolBar("File")  # 创建一个工具栏
        new = QAction(QIcon('../images/icon4.png'), "new", self)  # 为工具栏添加工具，第一个参数为图标，第二个参数为文本
        tb1.addAction(new)  # 将new工具添加到工具栏（tb1）上
        open = QAction(QIcon('../images/icon1.png'), "open", self)
        tb1.addAction(open)
        save = QAction(QIcon('../images/icon2.png'), "save", self)
        tb1.addAction(save)

        tb2 = self.addToolBar("File1")  # 创建第二个工具栏
        new1 = QAction(QIcon('../images/icon3.png'), "新建", self)
        tb2.addAction(new1)

        tb2.setToolButtonStyle(Qt.ToolButtonTextUnderIcon)  # 设置工具的显示方式（针对图标和文本）
        tb1.actionTriggered.connect(self.toolbtnpressed)  # 当触发工具时执行函数
        tb2.actionTriggered.connect(self.toolbtnpressed)

    def toolbtnpressed(self, a):
        print("按下的工具栏按钮是", a.text())


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = ToolBar()
    main.show()
    sys.exit(app.exec_())

```

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1647955724563-f8a2fdab-2a6d-4136-99fb-aafb29329646.png#clientId=uee23daa4-d12d-4&from=paste&height=244&id=u162996e1&originHeight=244&originWidth=503&originalType=binary&ratio=1&rotation=0&showTitle=false&size=17762&status=done&style=none&taskId=uad09a1e2-830c-437a-9bd7-a677711b366&title=&width=503)
<a name="ePggH"></a>
### 状态栏
状态栏是在窗口下方用来显示状态文本信息的。
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class StatusBar(QMainWindow):
    def __init__(self):
        super(StatusBar, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle('状态栏演示')
        self.resize(300, 200)
        bar = self.menuBar()
        file = bar.addMenu("File")
        file.addAction("show")
        file.triggered.connect(self.processTrigger)

        self.setCentralWidget(QTextEdit())  # 设置中心控件为文本框
        self.statusBar = QStatusBar()  # 创建状态栏
        self.setStatusBar(self.statusBar)  # 设置状态栏

    def processTrigger(self, q):
        if q.text() == "show":
            self.statusBar.showMessage(q.text() + '菜单被点击了', 5000)  # 设置状态栏的显示文本和时间（5s）


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = StatusBar()
    main.show()
    sys.exit(app.exec_())

```

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648001233589-16f827ad-d8a8-4bbc-9284-0f6b8ee67b76.png#clientId=uf7da44c7-654a-4&from=paste&height=239&id=u712c45b1&originHeight=239&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7525&status=done&style=none&taskId=uad0fca6d-7940-4c86-933e-a9408d596bb&title=&width=316)
<a name="Wc45g"></a>
## 表格布局
<a name="E7ejM"></a>
### QTableView控件 显示二维表数据
**显示二维表数据**<br />MCV数据处理方法： <br />M:Model   V: Viewer  C: Controller<br />将每个信息都分开创建再联系到一起，目的是将后端的数据和前端页面的耦合度降低，使一个数据可以被多次使用

声明表格模型，创建表格的首行标题，设置表格的数据，声明表格控件，关联表格控件与模型，最终将表格控件添加到布局中。<br />**总而言之就是根据数据创建模型，控件由模型构成。**
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class TableView(QWidget):
    def __init__(self):
        super(TableView, self).__init__()
        self.setWindowTitle('QTableView表格视图控件演示')
        self.resize(500, 300)
        self.model = QStandardItemModel(4, 3)  # 设置表格的行列
        self.model.setHorizontalHeaderLabels(['id', '姓名', '年龄'])  # 设置水平标题
        self.tableview = QTableView()  # 创建表格视图控件
        self.tableview.setModel(self.model)  # 关联表格视图控件和表格

        item11 = QStandardItem('10')  # 创建数据
        item12 = QStandardItem('雷神')
        item13 = QStandardItem('2000')
        self.model.setItem(0, 0, item11)  # 关联数据与表格
        self.model.setItem(0, 1, item12)
        self.model.setItem(0, 2, item13)

        item31 = QStandardItem('30')  # 创建数据
        item32 = QStandardItem('死亡女神')
        item33 = QStandardItem('3000')
        self.model.setItem(2, 0, item31)  # 关联数据与表格
        self.model.setItem(2, 1, item32)
        self.model.setItem(2, 2, item33)
        layout = QVBoxLayout()
        layout.addWidget(self.tableview)
        self.setLayout(layout)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = TableView()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648040018431-eb8dca1f-5f75-4747-bfa5-1d02f38cf801.png#clientId=ub98e5d78-2f47-4&from=paste&height=339&id=u82cedebe&originHeight=339&originWidth=516&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12172&status=done&style=none&taskId=uaccca19f-8001-460b-8834-5c23336027b&title=&width=516)
<a name="pOArw"></a>
### QTableWidget 扩展的表格控件
QTableWidget是QTableView的子类，相比父类添加了其他方法<br />每一个Cell（单元格）是一个QTableWidgetItem
```python
import sys
from PyQt5.QtWidgets import *


class TableWidgetDemo(QWidget):
    def __init__(self):
        super(TableWidgetDemo, self).__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle('QTableWidget演示')
        self.resize(430, 230)
        layout = QVBoxLayout()

        tablewidget = QTableWidget()
        tablewidget.setRowCount(4)  # 设置表格行数
        tablewidget.setColumnCount(3)  # 设置表格列数

        layout.addWidget(tablewidget)

        tablewidget.setHorizontalHeaderLabels(['姓名', '年龄', '籍贯'])  # 设置水平标题
        nameItem = QTableWidgetItem('小明')  # 创建表格的项
        tablewidget.setItem(0, 0, nameItem)  # 将项添加到表格中
        ageItem = QTableWidgetItem('24')
        tablewidget.setItem(0, 1, ageItem)
        jgItem = QTableWidgetItem('北京')
        tablewidget.setItem(0, 2, jgItem)
        # 设置表格为禁止编辑
        tablewidget.setEditTriggers(QAbstractItemView.NoEditTriggers)
        # 是选择表格项时是一行一行的选择的
        tablewidget.setSelectionBehavior(QAbstractItemView.SelectRows)
        # 设置表格的行与列的大小是根据项的内容自动匹配的
        tablewidget.resizeColumnsToContents()
        tablewidget.resizeRowsToContents()
        # 设置表格的水平标题与垂直标题不可见
        tablewidget.verticalHeader().setVisible(False)
        # tablewidget.horizontalHeader().setVisible(False)
        # 设置表格的垂直标题
        tablewidget.setVerticalHeaderLabels(['a', 'b'])
        # 隐藏表格线
        tablewidget.setShowGrid(False)
        self.setLayout(layout)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = TableWidgetDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648088448877-2b967c1f-088f-4b00-87ba-905c7e704b6c.png#clientId=u0a1365fb-5932-4&from=paste&height=269&id=ub36e29fc&originHeight=269&originWidth=446&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10326&status=done&style=none&taskId=uc4134548-8c79-4a2b-93c1-b23e92557b7&title=&width=446)
<a name="k0eYh"></a>
### QListView控件  显示列数据
先声明列数据控件，再声明列数据模型，然后声明列数据，然后将列数据与列数据模型关联起来，然后再把列数据控件与列数据模型关联起来。最终将列数据控件添加到布局中。<br />**总而言之就是根据数据创建模型，控件由模型构成。**
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class ListViewDemo(QWidget):
    def __init__(self):
        super(ListViewDemo, self).__init__()
        self.setWindowTitle('QListView 例子')
        self.resize(300, 270)
        layout = QVBoxLayout()
        listview = QListView()  # 创建列数据控件
        listModel = QStringListModel()  # 创建列数据模型
        self.list = ['列表项1', '列表项2', '列表项3']
        listModel.setStringList(self.list)  # 关联模型与数据
        listview.setModel(listModel)  # 关联控件和模型
        listview.clicked.connect(self.clicked)
        layout.addWidget(listview)
        self.setLayout(layout)

    def clicked(self, item):
        # 输出一个信息框，第一个意思是信息框属于QWidget类型，第二个设置信息框的标题，第三个为信息
        QMessageBox.information(self, 'QListView', '您选择了:' + self.list[item.row()])  


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = ListViewDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648041209428-4e27352f-2c72-494a-9d69-b8650be86ec6.png#clientId=ub98e5d78-2f47-4&from=paste&height=305&id=u356e8527&originHeight=305&originWidth=302&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13309&status=done&style=none&taskId=u98e194b6-3567-4284-b130-64c001c433e&title=&width=302)
<a name="tPESG"></a>
### QListWidget 扩展的列表控件
QListWidget是QListView的子类<br />子类在父类的基础上添加了很多API
```python
from PyQt5.QtWidgets import *
import sys


class ListWidgetDemo(QMainWindow):
    def __init__(self, parent=None):
        super(ListWidgetDemo, self).__init__()
        self.setWindowTitle('QListWidget 例子')
        self.resize(300, 270)

        self.listwidget = QListWidget()  # 创建ListWedget控件的实例
        self.listwidget.addItem('item1')  # 直接为实例添加数据
        self.listwidget.addItem('item2')
        self.listwidget.addItem('item3')
        self.listwidget.addItem('item4')
        self.listwidget.addItem('item5')
        self.listwidget.itemClicked.connect(self.clicked)
        self.setCentralWidget(self.listwidget)  # 将列表控件设置为中心控件

    def clicked(self, Index):
        QMessageBox.information(self, 'QListWidget', '您选择了：' + self.listwidget.item(self.listwidget.row(Index)).text())


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = ListWidgetDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648043406674-cdbcc6c4-ead8-49a3-85fd-d9c10552dbfa.png#clientId=ub98e5d78-2f47-4&from=paste&height=309&id=u606a7692&originHeight=309&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13411&status=done&style=none&taskId=u4ee368ec-57ac-4c52-ae47-8af03e38aa3&title=&width=316)
<a name="H200e"></a>
## 容器控件
<a name="ct1m0"></a>
### QTabWidget选项卡控件
QTabWidget被继承后，可以在QTabWidget容器中添加多个tab（选项卡），然后可以为不同选项卡设置不同的窗口。<br />选项卡控件介绍：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648089012732-a45c4cea-9eca-4fc0-ab6a-362765e8de93.png#clientId=u0a1365fb-5932-4&from=paste&height=704&id=ud9df96e9&originHeight=704&originWidth=924&originalType=binary&ratio=1&rotation=0&showTitle=false&size=181751&status=done&style=none&taskId=uf5f5d812-7091-43f6-a283-5fbbbce2626&title=&width=924)
```python
import sys
from PyQt5.QtWidgets import *


class TabWidgetDemo(QTabWidget):
    def __init__(self):
        super(TabWidgetDemo, self).__init__()
        self.setWindowTitle("选项卡控件：QTabWidget")
        self.resize(400, 300)
        # 创建选项卡窗口
        self.tab1 = QWidget()
        self.tab2 = QWidget()
        self.tab3 = QWidget()
        # 关联窗口和选项卡
        self.addTab(self.tab1, "选项卡1")
        self.addTab(self.tab2, "选项卡2")
        self.addTab(self.tab3, "选项卡3")
        # 设置窗口的属性
        self.tab1UI()
        self.tab2UI()
        self.tab3UI()

    def tab1UI(self):
        layout = QFormLayout()
        layout.addRow('姓名', QLineEdit())
        layout.addRow('地址', QLineEdit())
        self.setTabText(0, '联系方式')  # 设置下标为0的选项卡的标题
        self.tab1.setLayout(layout)  # 设置选项卡的布局

    def tab2UI(self):
        layout = QFormLayout()
        sex = QHBoxLayout()
        sex.addWidget(QRadioButton('男'))
        sex.addWidget(QRadioButton('女'))
        layout.addRow(QLabel('性别'), sex)
        layout.addRow('生日', QLineEdit())
        self.setTabText(1, '个人详细信息')
        self.tab2.setLayout(layout)

    def tab3UI(self):
        layout = QHBoxLayout()
        layout.addWidget(QLabel('科目'))
        layout.addWidget(QCheckBox('物理'))
        layout.addWidget(QCheckBox('高数'))
        self.setTabText(2, "教育程度")
        self.tab3.setLayout(layout)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = TabWidgetDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648090800485-7283343c-7ae1-4146-b441-a4956681fa47.png#clientId=u0a1365fb-5932-4&from=paste&height=339&id=u717d3c54&originHeight=339&originWidth=416&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8817&status=done&style=none&taskId=u58c21134-62b8-4cac-b572-eefbf0be8c9&title=&width=416)
<a name="HPQ5l"></a>
### QStackedWidget 堆栈窗口控件
堆栈窗口控件就是用来存放多个窗口的容器，然后可以通过setCurrentIndex(index)方法来显示对应序号的窗口
```python
import sys
from PyQt5.QtWidgets import *


class StackedExample(QWidget):
    def __init__(self):
        super(StackedExample, self).__init__()
        self.setGeometry(300, 50, 10, 10)
        self.setWindowTitle("堆栈窗口控件：QStackedWidget")
        self.resize(400, 300)

        self.list = QListWidget()
        self.list.insertItem(0, '联系方式')
        self.list.insertItem(1, '个人信息')
        self.list.insertItem(2, '教育程度')
        # 创建三个用来堆栈的窗口
        self.stack1 = QWidget()
        self.stack2 = QWidget()
        self.stack3 = QWidget()

        self.tab1UI()
        self.tab2UI()
        self.tab3UI()

        self.stack = QStackedWidget()  # 创建堆栈窗口控件
        self.stack.addWidget(self.stack1)  # 将创建的窗口放入堆栈窗口控件中
        self.stack.addWidget(self.stack2)
        self.stack.addWidget(self.stack3)
        # 创建水平布局左边为列表控件 右边为堆栈窗口控件
        hbox = QHBoxLayout()
        hbox.addWidget(self.list)
        hbox.addWidget(self.stack)
        self.setLayout(hbox)
        self.list.currentRowChanged.connect(self.display)  # 当改变选择的列表行时调用display函数，来显示对应的堆栈中的窗口

    def tab1UI(self):
        layout = QFormLayout()
        layout.addRow('姓名', QLineEdit())
        layout.addRow('地址', QLineEdit())
        self.stack1.setLayout(layout)  # 为stack1窗口添加布局

    def tab2UI(self):
        layout = QFormLayout()
        sex = QHBoxLayout()
        sex.addWidget(QRadioButton('男'))
        sex.addWidget(QRadioButton('女'))
        layout.addRow(QLabel('性别'), sex)
        layout.addRow('生日', QLineEdit())
        self.stack2.setLayout(layout)

    def tab3UI(self):
        layout = QHBoxLayout()
        layout.addWidget(QLabel('科目'))
        layout.addWidget(QCheckBox('物理'))
        layout.addWidget(QCheckBox('高数'))
        self.stack3.setLayout(layout)

    def display(self, index):
        self.stack.setCurrentIndex(index)  # 根据序号切换显示堆栈中的对应窗口


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = StackedExample()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648096644277-d9ed0652-90a8-44a5-8716-db535ad1db2b.png#clientId=u0a1365fb-5932-4&from=paste&height=339&id=u028fd2d4&originHeight=339&originWidth=416&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13718&status=done&style=none&taskId=u7c26c10f-f482-4cea-8156-1c757b2edbe&title=&width=416)
<a name="NwSni"></a>
### QDockWidget停靠控件
停靠控件用来创建那些平时使用的软件中的可以自由拖动与固定的那些窗口
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class DockDemo(QMainWindow):
    def __init__(self):
        super(DockDemo, self).__init__()
        self.setWindowTitle('停靠控件（QDockWidget）')
        self.resize(400, 300)
        layout = QHBoxLayout()
        self.items = QDockWidget('Dockable', self)  # 创建停靠窗口并设置名字
        self.listWidget = QListWidget()
        self.listWidget.addItem('item1')
        self.listWidget.addItem('item2')
        self.listWidget.addItem('item3')
        self.items.setWidget(self.listWidget)  # 将列表控件设置到停靠窗口上
        self.setCentralWidget(QLineEdit())  # 设置中心控件为文本框

        self.items.setFloating(True)  # 设置停靠窗口默认是悬浮状态

        self.addDockWidget(Qt.RightDockWidgetArea, self.items)  # 添加停靠窗口并设置为默认停靠右侧


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = DockDemo()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648098692621-5e5f163f-cd6f-46b1-850e-fa1b7858a81f.png#clientId=u0a1365fb-5932-4&from=paste&height=339&id=uc867dc67&originHeight=339&originWidth=416&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11483&status=done&style=none&taskId=u3c594ff8-a28f-4b6f-a14b-e50e71c4b69&title=&width=416)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648098700284-bf7a14b0-9520-424d-a8d2-8dcdacd46cc1.png#clientId=u0a1365fb-5932-4&from=paste&height=339&id=ucb7ed843&originHeight=339&originWidth=416&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11969&status=done&style=none&taskId=uac01a939-cf81-48d0-a2a9-3bdabc7cf97&title=&width=416)
<a name="viU6m"></a>
### 容纳多文档窗口
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class MultiWindows(QMainWindow):
    count = 0  # 记录窗口数

    def __init__(self, parent=None):
        super(MultiWindows, self).__init__(parent)
        self.setWindowTitle('容纳多文档的窗口')
        self.mdi = QMdiArea()  # 用来存放多文档的控件
        self.setCentralWidget(self.mdi)
        bar = self.menuBar()
        file = bar.addMenu('File')
        file.addAction('New')
        file.addAction('cascade')  # 用来设置层叠方式
        file.addAction('Tiled')  # 用来设置平铺方式
        file.triggered.connect(self.windowacation)

    def windowacation(self, q):
        print(q.text())
        if q.text() == "New":
            MultiWindows.count = MultiWindows.count + 1  # 用来统计创建的窗口个数
            sub = QMdiSubWindow()  # 创建子窗口对象
            sub.setWidget(QTextEdit())
            sub.setWindowTitle('子窗口' + str(MultiWindows.count))
            self.mdi.addSubWindow(sub)
            sub.show()
        elif q.text() == "cascade":
            self.mdi.cascadeSubWindows()
        elif q.text() == "Tiled":
            self.mdi.tileSubWindows()


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = MultiWindows()
    main.show()
    sys.exit(app.exec_())

```
new时：新建窗口![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648102793095-e5973c74-e66d-41ad-85c5-70d32913d4e0.png#clientId=u0a1365fb-5932-4&from=paste&height=759&id=ud0fddb13&originHeight=759&originWidth=1296&originalType=binary&ratio=1&rotation=0&showTitle=false&size=44400&status=done&style=none&taskId=u582a7f95-5bea-4b95-93c8-ac8a191b9b8&title=&width=1296)<br />cascade时： 层叠![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648102811665-6e66d50f-71f1-420b-8190-e972a59251a0.png#clientId=u0a1365fb-5932-4&from=paste&height=759&id=u576a177c&originHeight=759&originWidth=1296&originalType=binary&ratio=1&rotation=0&showTitle=false&size=45726&status=done&style=none&taskId=ue11a42f9-0d6b-4fd4-849e-ba9805657c8&title=&width=1296)<br />Tiled时  平铺<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648102832436-9c225cff-d611-4aab-8ab5-6c4b15484aea.png#clientId=u0a1365fb-5932-4&from=paste&height=759&id=u48907feb&originHeight=759&originWidth=1296&originalType=binary&ratio=1&rotation=0&showTitle=false&size=47111&status=done&style=none&taskId=u32c80d48-bb4d-4a85-9cdf-5cb01dec8f3&title=&width=1296)
<a name="tegeQ"></a>
### QScrollBar滚动条控件

1. 通过滚动条值的变化控制其他控件状态的变化
2. 通过滚动条值的变化控制控件位置的变化
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class ScrollBar(QWidget):
    def __init__(self):
        super(ScrollBar, self).__init__()
        self.initUI()

    def initUI(self):
        hbox = QHBoxLayout()
        self.label = QLabel('拖动滚动条去改变文字颜色')
        hbox.addWidget(self.label)
        self.scrollbar1 = QScrollBar()  # 创建滚动条
        self.scrollbar1.setMaximum(255)  # 设置滚动条尽头对应的最大值
        self.scrollbar1.sliderMoved.connect(self.sliderMoved)  # 当滚动条的滑块移动时触发

        self.scrollbar2 = QScrollBar()
        self.scrollbar2.setMaximum(255)
        self.scrollbar2.sliderMoved.connect(self.sliderMoved)

        self.scrollbar3 = QScrollBar()
        self.scrollbar3.setMaximum(255)
        self.scrollbar3.sliderMoved.connect(self.sliderMoved)

        self.scrollbar4 = QScrollBar()
        self.scrollbar4.setMaximum(255)
        self.scrollbar4.sliderMoved.connect(self.sliderMoved1)

        hbox.addWidget(self.scrollbar1)
        hbox.addWidget(self.scrollbar2)
        hbox.addWidget(self.scrollbar3)
        hbox.addWidget(self.scrollbar4)

        self.setGeometry(300, 300, 300, 200)  # 设置窗口的大小
        self.setLayout(hbox)
        self.y = self.label.pos().y()  # 保留当前标签的坐标

    def sliderMoved(self):
        print(self.scrollbar1.value(), self.scrollbar2.value(), self.scrollbar3.value())
        palette = QPalette()  # 创建调色板
        c = QColor(self.scrollbar1.value(), self.scrollbar2.value(), self.scrollbar3.value(), 255)  # c 用来存取颜色
        palette.setColor(QPalette.Foreground, c)
        self.label.setPalette(palette)

    def sliderMoved1(self):
        self.label.moce(self.label.x(), self.y + self.scrollbar4.value())  # 通过改变滑块改变标签的y坐标


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = ScrollBar()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648121419531-6276247b-f5d0-45e3-ae79-eda7ac8a7115.png#clientId=u7d3b531b-6483-4&from=paste&height=239&id=u3bc7edf0&originHeight=239&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7863&status=done&style=none&taskId=u5e6f2c03-a183-48b0-9483-007ac1e6493&title=&width=316)从左到右前三个滑块分别控制rgb三通道数值（0~255），第四个滑块控制标签的y坐标
<a name="qx90H"></a>
## 多线程与定时器
多线程的作用：对于比较耗时的任务如果使用单线程可能会造成阻塞，因此通过多线程可以使耗时的任务不影响其他任务的进行。
<a name="zqrW5"></a>
### QTimer定时器控件
定时器控件可以用来动态显示当前时间，每一秒都在调用函数更新。
```python
from PyQt5.QtWidgets import QWidget, QPushButton, QApplication, QListWidget, QGridLayout, QLabel
from PyQt5.QtCore import QTimer, QDateTime
import sys


class ShowTime(QWidget):
    def __init__(self):
        super(ShowTime, self).__init__()
        self.setWindowTitle('动态显示当前时间')
        self.label = QLabel('显示当前时间')
        self.startBtn = QPushButton('开始')
        self.endBtn = QPushButton('结束')
        layout = QGridLayout()  # 使用网格布局
        self.timer = QTimer()  # 创建定时器
        self.timer.timeout.connect(self.showTime)  # 定时器开启时调用showTime 需要手动开启

        layout.addWidget(self.label, 0, 0, 1, 2)
        layout.addWidget(self.startBtn, 1, 0)
        layout.addWidget(self.endBtn, 1, 1)

        self.startBtn.clicked.connect(self.startTimer)
        self.endBtn.clicked.connect(self.endTimer)

        self.setLayout(layout)
        self.resize(400, 300)

    def showTime(self):
        time = QDateTime.currentDateTime()  # 获取当前的时间
        # 设置时间显示的格式 年月日 时分秒 星期几（如果是ddd代表意思是周几）
        timeDisplay = time.toString("yyyy-MM-dd hh:mm:ss dddd")
        self.label.setText(timeDisplay)

    def startTimer(self):
        self.timer.start(1000)  # 经过1秒后开启定时器
        self.startBtn.setEnabled(False)  # 设置开始按钮不可用
        self.endBtn.setEnabled(True)  # 设置停止按钮可用

    def endTimer(self):
        self.timer.stop()  # 停止定时器
        self.startBtn.setEnabled(True)  # 设置开始按钮不可用
        self.endBtn.setEnabled(False)  # 设置停止按钮可用


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = ShowTime()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648125327315-e665ba98-47e5-4772-8d0b-6ee2923928bc.png#clientId=u7d3b531b-6483-4&from=paste&height=339&id=udcf63b4a&originHeight=339&originWidth=416&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9965&status=done&style=none&taskId=u0b6260ca-0cb7-408d-b037-b0fe8d090cb&title=&width=416)
<a name="lbFfY"></a>
### QTimer.singleShot让程序定时关闭
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *

if __name__ == '__main__':
    app = QApplication(sys.argv)
    label = QLabel('<font color=red size=140><b>Hello World,窗口在5秒后自动关闭！</b></font>')
    # 设置窗口样式
    label.setWindowFlags(Qt.SplashScreen | Qt.FramelessWindowHint)
    label.show()
    QTimer.singleShot(5000, app.quit)  # 5秒后自动关掉程序
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648126681626-3def3955-aed2-46b8-979c-af33dcc8dbd6.png#clientId=u7d3b531b-6483-4&from=paste&height=81&id=u82e33c09&originHeight=81&originWidth=537&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11401&status=done&style=none&taskId=ucdaad9e0-2579-464c-b123-a75c799af4e&title=&width=537)
<a name="Ge8mX"></a>
### QThread 线程类
线程类可以实现计数器<br />QLCDNumber ： 模拟LCD显示效果的控件<br />WorkThread(继承自QThread): 自定义信号，实现在不同线程中信息的交互。之前使用的都是空间变化的系统信号。
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *

sec = 0  # 用来计数


class WorkThread(QThread):  # 工作线程
    timer = pyqtSignal()  # 将timer设定为信号，每隔一秒发送
    end = pyqtSignal()  # 将end设定为信号，计数完成后发送

    def run(self):
        while True:
            self.sleep(1)  # 休眠一秒（每一秒中循环一次）
            if sec == 5:
                self.end.emit()  # 计数达到5时发送end信号
            self.timer.emit()  # 每秒发送一次timer信号


class Counter(QWidget):
    def __init__(self, parent=None):
        super(Counter, self).__init__(parent)
        self.setWindowTitle("使用线程类（QThread）编写计数器")
        self.resize(300, 120)
        layout = QVBoxLayout()
        self.lcdNumber = QLCDNumber()
        layout.addWidget(self.lcdNumber)
        button = QPushButton('开始计数')
        layout.addWidget(button)
        self.workThread = WorkThread()  # 创建工作线程类
        self.workThread.timer.connect(self.countTime)  # 将timer工作线程信号与countTime绑定
        self.workThread.end.connect(self.end)
        button.clicked.connect(self.work)
        self.setLayout(layout)

    def countTime(self):
        global sec  # 使用全局变量sec
        sec += 1
        self.lcdNumber.display(sec)
    def end(self):
        # 弹出对话框
        QMessageBox.information(self,'消息','计数结束',QMessageBox.Ok)
    def work(self):
        self.workThread.start()

if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = Counter()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648174750885-a4da1dfa-cf42-4acf-bd09-1ffb2be65381.png#clientId=u85b976bf-ff46-4&from=paste&height=162&id=u0174a0b1&originHeight=162&originWidth=431&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9383&status=done&style=none&taskId=ufa04bed6-08ee-4052-9b19-66186fdea9b&title=&width=431)
<a name="V1PZP"></a>
## 窗口
<a name="NQIV0"></a>
### 设置窗口风格
pyqt5窗口一共有三种风格<br />可以通过print(QStyleFactory.keys())来显示pyqt5窗口风格的种类：<br />'windowsvista', 'Windows', 'Fusion'<br />可以通过QApplication.setStyle(窗口风格)来设置窗口控件的风格。
```python
import sys
from PyQt5.QtCore import *
from PyQt5 import QtCore
from PyQt5.QtWidgets import *


class WindowStyle(QWidget):
    def __init__(self):
        super(WindowStyle, self).__init__()
        horizontalLayout = QHBoxLayout()
        self.styleLabel = QLabel('设置窗口风格：')
        self.styleComboBox = QComboBox()
        # 将三种风格添加到列表中
        self.styleComboBox.addItems(QStyleFactory.keys())
        # 输出当前的窗口风格
        print(QApplication.style().objectName())
        # 根据当前的窗口风格得到对应的序号
        index = self.styleComboBox.findText(QApplication.style().objectName(), QtCore.Qt.MatchFixedString)
        # 设置列表中默认对应的窗口风格
        self.styleComboBox.setCurrentIndex(index)
        self.styleComboBox.activated[str].connect(self.handleStyleChanged)
        horizontalLayout.addWidget(self.styleLabel)
        horizontalLayout.addWidget(self.styleComboBox)
        self.setLayout(horizontalLayout)
        self.resize(200, 100)

    def handleStyleChanged(self, style):
        QApplication.setStyle(style)  # 设置窗口风格


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = WindowStyle()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648292348729-480fe1e9-45ca-46c7-890c-3825fa95a2bf.png#clientId=uef9b1ee7-2eb1-4&from=paste&height=139&id=u35fd062b&originHeight=139&originWidth=230&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4941&status=done&style=none&taskId=u7adbd98f-4e40-41c2-9e27-22994fcab53&title=&width=230)
<a name="An0vE"></a>
### 设置窗口样式 setWindowFlags
窗口样式的调整主要针对窗口边框、标题栏以及窗口本身的样式<br />使用setWindowFlags设置窗口样式，可以使用参数介绍：<br />Qt.WindowMaximizeButtonHint(设置激活窗口的最大化按钮（右上角那个按钮）)<br />Qt.WindowCloseButtonHint(设置激活窗口的关闭按钮（右上角那个按钮）)<br />Qt.WindowMinimizeButtonHint(设置激活窗口的最小化按钮（右上角那个按钮）)<br />Qt.WindowStaysOnTopHint(设置窗口始终在窗口最前方显示)<br />Qt.FramelessWindowHint(设置窗口为无边框)
```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtWidgets import *


class WindowPattern(QMainWindow):
    def __init__(self):
        super(WindowPattern, self).__init__()
        self.setWindowTitle("设置窗口的样式")

        self.setWindowFlags(Qt.WindowMaximizeButtonHint | Qt.WindowStaysOnTopHint | Qt.FramelessWindowHint)
        self.setObjectName("MainWindow")
        # 通过类CSS语言设置窗口背景图片
        self.setStyleSheet("#MainWindow{border-image:url(../images/bool.png);}")


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = WindowPattern()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648293603816-08c8f46a-2594-448a-b532-1ed12cde9bd8.png#clientId=uef9b1ee7-2eb1-4&from=paste&height=137&id=ud3743a58&originHeight=137&originWidth=296&originalType=binary&ratio=1&rotation=0&showTitle=false&size=15892&status=done&style=none&taskId=uf7e17d95-167e-4db7-bd35-128f4a23aa1&title=&width=296)
<a name="WKnVs"></a>
### 用代码设置窗口的最大化和最小化
```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtWidgets import *


class WindowMaxMin(QWidget):
    def __init__(self, parent=None):
        super(WindowMaxMin, self).__init__(parent)
        self.resize(300, 400)
        self.setWindowTitle('用代码控制窗口的最大化和最小化')

        layout = QVBoxLayout()

        maxButton1 = QPushButton('窗口最大化1')
        maxButton1.clicked.connect(self.maximized1)  # 自定义的最大化方法，最大化的同时会将标题栏也覆盖掉
        maxButton2 = QPushButton('窗口最大化2')
        maxButton2.clicked.connect(self.showMaximized)  # 调用库中的最大化方法跟正常的最大化形式相同
        minButton = QPushButton('窗口最小化')
        minButton.clicked.connect(self.showMinimized)

        layout.addWidget(maxButton1)
        layout.addWidget(maxButton2)
        layout.addWidget(minButton)
        self.setLayout(layout)

    def maximized1(self):
        desktop = QApplication.desktop()  # 获取当前窗口
        rect = desktop.availableGeometry()  # 将窗口的最大区域大小赋予rect(0,0,1920,1040)
        self.setGeometry(rect)  # 设置工作区大小，也就是将工作区大小设置为最大（会导致标题栏无法显示在屏幕上）


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main = WindowMaxMin()
    main.show()
    sys.exit(app.exec_())

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648295805823-924a1f12-70de-45da-b275-4507602209be.png#clientId=uef9b1ee7-2eb1-4&from=paste&height=439&id=u13e1ba6d&originHeight=439&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10699&status=done&style=none&taskId=u862641aa-7fac-421a-bbf4-3a0fe8cc786&title=&width=316)
