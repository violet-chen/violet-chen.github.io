---
title: Maya后台执行脚本
tags: MayaPy
categories: DCC工具开发
abbrlink: 5d346a9c
date: 2023-10-09 16:09:00
---

# 不带界面的后台执行脚本方法
这里提供一下后台执行python脚本的脚本模板
使用方法: 
1. 将想要对maya后台执行的操作的命令写到模板文件的 # TODO:function content下面
2. win+r然后输入cmd打开命令行窗口
3. 找到maya程序文件夹下的mayapy.exe文件,拖入到命令行窗口
4. 打个空格,将后台执行的python脚本拖入到命令行窗口
5. 因为模板里有通过sys.argv[1]来得到参数,模板的main函数中想要得到的参数是存放maya文件的文件夹路径,因此打个空格让后把文件夹拖入到命令行窗口中
6. 按下回车,就可以遍历文件夹下的所有maya文件,然后执行你写的操作命令.
7. 成功打开maya的列表信息会放到存放maya文件夹下的successful_open_files.json中,没有后台打开的maya文件信息会放到unsuccessful_open_files.json中.

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
import os
import sys
import logging
import re
import maya.standalone
import maya.cmds as cmds
import json
maya.standalone.initialize()

logging.basicConfig(format="%(asctime)s %(levelname)-8s %(message)s",
                    level=logging.WARNING, datefmt="%Y-%m-%d %H:%M:%S")

def main(maya_file_dir_path):
    # create json file.
    successful_json_info = {}
    unsuccessful_json_info = {}
    successful_json_path = os.path.join(maya_file_dir_path,"successful_open_files.json").replace("\\","/")
    unsuccessful_json_path = os.path.join(maya_file_dir_path,"unsuccessful_open_files.json").replace("\\","/")
    load_successful_files = []
    load_unsuccessful_files = []
    # get maya file path list.
    maya_file_path_list = []
    maya_file_name_list = os.listdir(maya_file_dir_path)
    if maya_file_name_list:
        for file_name in maya_file_name_list:
            if file_name.endswith(".ma"):
                maya_file_path = os.path.join(maya_file_dir_path,file_name).replace("\\","/")
                maya_file_path_list.append(maya_file_path)
    
    for maya_file_path in maya_file_path_list:
        try:
            cmds.file(maya_file_path, open=True, pmt=False)
            logging.info("load file:{}".format(maya_file_path))
            load_successful_files.append(maya_file_path)
        except:
            load_unsuccessful_files.append(maya_file_path)
            continue

        # TODO:function content


    successful_json_info["load_file"] = load_successful_files
    unsuccessful_json_info["unload_file"] = load_unsuccessful_files
    with open(successful_json_path,'w') as f:
        json.dump(successful_json_info,f,indent=4)
    with open(unsuccessful_json_path,'w') as f:
        json.dump(unsuccessful_json_info,f,indent=4)
        
# maya.standalone.uninitialize()

if __name__ == "__main__":
    main(sys.argv[1])
```

---
# 带界面的后台执行脚本方法

## 需要注意的点:
1. 不能直接在脚本文件的顶部导入maya的模块(导入的其他模块中也不能包含maya的模块)
2. 需要通过mayapy来执行窗口的建立，不然用其他解释器没有maya的模块
3. 不能通过多线程的start功能来进行后台任务具体的步骤
4. 通过窗口类来创建启动任务的子线程（可以用start），然后通过启动任务的子线程来执行后台操作（不可以用start，需要用run）
5. 在用于启动后台操作的类中导入 maya.standalone 并执行 maya.standalone.initialize()
6. 后台打开文件需要用pymel模块的openFile方法并且加上force=True，例如：pm.openFile(file_path,open=True,force=True)

## 大概步骤
1. 先正常通过pyside2写窗口的代码.
2. 当需要调用后台执行操作的时候,就通过多线程来进行.
3. 所有东西写完以后可以将所用东西进行打包成程序即可使用了.

## 子线程的类的定义:
这里的import MainWork as mainWork 是自定义的执行后台操作内容的脚本模块
```python
class StartWork(threading.Thread):
    def __init__(self,path_item_dict,thread_lock):
        threading.Thread.__init__(self)
        self.path_item_dict = path_item_dict
        self.thread_lock = thread_lock

    def run(self):
        self.thread_lock.acquire()
        self.startWork()
        self.thread_lock.release()
        
    def startWork(self):
        import maya.standalone
        maya.standalone.initialize()
        import MainWork as mainWork
        for path,item in self.path_item_dict.items():
            thread_lock = threading.Lock()
            work_thread = mainWork.MainWork(path,thread_lock,item,my_signals)
            work_thread.run()
```
## 调用子线程
这里的StartWork就是刚才定义的线程类

thread_lock = threading.Lock()
work_th = StartWork(path_item_dict, thread_lock)
work_th.start()