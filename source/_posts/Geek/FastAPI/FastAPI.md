---
title: FastAPI
tags: FastAPI
categories: Geek
abbrlink: e7d3ad81
date: 2024-03-15 10:51:00
---

# 开始
官方文档:https://fastapi.tiangolo.com/python-types/
## 第一步
文件夹里创建一个main.py文件
运行实时服务器(代码更新时服务器也会自动更新):
uvicorn main:app --reload
有可能会报错,报错的话一般就是8000端口被占用了,需要处理一下
## 代码内容
```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/") # HTTP方法
async def root():
    return {"message": "Hello World"}
```
## api文档链接
交互式API文档链接(原链接基础上加/docs):http://127.0.0.1:8000/docs
替代API文档链接(原链接基础上加/redoc):http://127.0.0.1:8000/redoc
## HTTP方法
post:创建数据
get:读取数据
put:更新数据
delete:删除数据

# 接口路由的类型
## 路径带有参数
```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/items/{item_id}") # item_id可以作为参数
async def read_item(item_id):
    return {"item_id": item_id}

```
## 路径参数带有类型
```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}
```

## 如何让带参数的路径与固定路径共存
例如既需要@app.get("/users/me")又需要@app.get("/users/{user_id}")时
只需要将@app.get("/users/me")声明放到@app.get("/users/{user_id}")前面即可
举例:
```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/users/me")
async def read_user_me():
    return {"user_id": "the current user"}


@app.get("/users/{user_id}")
async def read_user(user_id: str):
    return {"user_id": user_id}
```

## 通过枚举来让一个函数实现多个路径
通过继承str和enum来创建string类型的枚举类
```python
from enum import Enum

from fastapi import FastAPI


class ModelName(str, Enum):
    alexnet = "alexnet"
    resnet = "resnet"
    lenet = "lenet"


app = FastAPI()


@app.get("/models/{model_name}")
async def get_model(model_name: ModelName):
    if model_name is ModelName.alexnet:
        return {"model_name": model_name, "message": "Deep Learning FTW!"}

    if model_name.value == "lenet":
        return {"model_name": model_name, "message": "LeCNN all the images"}

    return {"model_name": model_name, "message": "Have some residuals"}
```

## 包含路径的路径参数
在本例中，参数的名称是 file_path ，最后一部分 :path 告诉它该参数应该匹配任何路径。
```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/files/{file_path:path}")
async def read_file(file_path: str):
    return {"file_path": file_path}
```

# 查询参数