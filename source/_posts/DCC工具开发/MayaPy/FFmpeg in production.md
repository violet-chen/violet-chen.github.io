---
title: FFmpeg in production
tags: FFmpeg
categories: DCC工具开发
abbrlink: b7b3d3ec
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

<a name="k62qS"></a>
# FFmpeg与ffmpeg的介绍
<a name="BR4Wx"></a>
## FFmpeg or ffmpeg
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673936833672-f709f7e7-0067-41dd-b0f5-9b2e2094084b.png#averageHue=%23111111&clientId=u2f19a3ad-c148-4&from=paste&height=229&id=u41085d30&originHeight=229&originWidth=2140&originalType=binary&ratio=1&rotation=0&showTitle=false&size=172285&status=done&style=none&taskId=u4a2bade5-fc04-429c-9ec8-233e211251c&title=&width=2140)
<a name="lF4l3"></a>
## FFmpeg tools
FFmpeg提供的所有工具： <br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673936885926-0187a839-8e1a-490f-b0a2-94d29a805769.png#averageHue=%23080808&clientId=u2f19a3ad-c148-4&from=paste&height=734&id=u1aa47442&originHeight=734&originWidth=2158&originalType=binary&ratio=1&rotation=0&showTitle=false&size=290899&status=done&style=none&taskId=u3722c923-c8e1-426a-8842-5c938f2ec7e&title=&width=2158)
<a name="eKf78"></a>
## FFmpeg libraries
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673937020238-2f9dd90e-64de-427b-8025-9728ee4aea55.png#averageHue=%23060606&clientId=u2f19a3ad-c148-4&from=paste&height=663&id=u7181e3f9&originHeight=663&originWidth=2165&originalType=binary&ratio=1&rotation=0&showTitle=false&size=215397&status=done&style=none&taskId=u095783ac-8635-4529-98cd-d5c7d8c1980&title=&width=2165)
<a name="x3R6c"></a>
## ffmpeg
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1673937128075-057b74f7-09f0-4c5f-bb6e-dd403aedd0d9.png#averageHue=%23060606&clientId=u2f19a3ad-c148-4&from=paste&height=534&id=u8f02f286&originHeight=534&originWidth=2209&originalType=binary&ratio=1&rotation=0&showTitle=false&size=231125&status=done&style=none&taskId=u5fa73875-6ec5-454e-89bb-c3b68590965&title=&width=2209)
<a name="pPYhz"></a>
# 安装ffmpeg
[https://github.com/BtbN/FFmpeg-Builds/releases](https://github.com/BtbN/FFmpeg-Builds/releases)<br />可以去这个github网站里下载构建版本
<a name="gSfxC"></a>
# ffmpeg基础语法
在powershell中使用<br />在![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686124834256-4b7dbe37-eeb5-4ba5-abf2-709f5cee50a5.png#averageHue=%23faf9f7&clientId=u6c33c667-b75d-4&from=paste&height=374&id=u5b17cf2d&originHeight=374&originWidth=707&originalType=binary&ratio=1&rotation=0&showTitle=false&size=45262&status=done&style=none&taskId=ua8de8cbd-3ca2-44a7-a7ef-24fe9834daf&title=&width=707)构建好的ffmpeg目录下的bin目录下按shift加鼠标右键然后按s快捷键即可在目录下打开powershell<br />前面是输入选项和路径，后面是输出选项和路径。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686130668081-50866e46-3ec5-460b-a5fc-e1886492c111.png#averageHue=%230c0c0c&clientId=u6c33c667-b75d-4&from=paste&height=108&id=u959cf2bb&originHeight=108&originWidth=1699&originalType=binary&ratio=1&rotation=0&showTitle=false&size=56375&status=done&style=none&taskId=u719581c8-fed6-4f10-bc3f-6137f8542c2&title=&width=1699)
<a name="X8L2Y"></a>
# 将图片序列转成视频
将 文件夹中符合img_seq.%04d的图片整合成24帧的视频序列，用h264编码：.\ffmpeg.exe -framerate 24 -i .\_image_sequences\img_seq\img_seq.%04d.png -c:v h264 output.mp4  <br />-c:v: h264 意思是使用h264编码视频流
<a name="ngldj"></a>
# ffmpeg与输出以及h264相关的option介绍
<a name="btBYo"></a>
## Constant Rate Factor （crf）输出质量
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686127869111-004de1e0-3998-4bce-8b84-695aa5590c60.png#averageHue=%230a0a0a&clientId=u6c33c667-b75d-4&from=paste&height=784&id=ua6c98757&originHeight=784&originWidth=1714&originalType=binary&ratio=1&rotation=0&showTitle=false&size=298300&status=done&style=none&taskId=ue1e4471e-ca2e-4359-ad3e-9c1f5615e0e&title=&width=1714)
<a name="FThoC"></a>
## Preset 编码速度预设
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686127978943-e0d1bed6-d116-43dd-8f5f-7351363cab76.png#averageHue=%23060606&clientId=u6c33c667-b75d-4&from=paste&height=896&id=uea4b45e7&originHeight=896&originWidth=1742&originalType=binary&ratio=1&rotation=0&showTitle=false&size=245348&status=done&style=none&taskId=ube678619-e57d-4e15-a3bd-72e07e482fa&title=&width=1742)
<a name="icEGW"></a>
## Tune（不经常使用）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686128368452-e0e78d2f-a4ff-417a-8303-b2be9484579f.png#averageHue=%230c0c0c&clientId=u6c33c667-b75d-4&from=paste&height=1019&id=uccaf701b&originHeight=1019&originWidth=1973&originalType=binary&ratio=1&rotation=0&showTitle=false&size=502036&status=done&style=none&taskId=udc054b92-eea8-488b-8174-6fa9665c1eb&title=&width=1973)
<a name="aI8qr"></a>
## Profile(-profile:v) and Level(-level)  (为了兼容旧设备才需要看这个)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686128887023-6b184a06-2784-47ae-bfb2-1a76cd304fc5.png#averageHue=%230a0a0a&clientId=u6c33c667-b75d-4&from=paste&height=938&id=ub5ef7475&originHeight=938&originWidth=1770&originalType=binary&ratio=1&rotation=0&showTitle=false&size=374321&status=done&style=none&taskId=u6789f85f-e2b7-414a-8e7b-c02f32a058a&title=&width=1770)
<a name="NKjmJ"></a>
## 更改输出的缩放比
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686129672761-7d028a0d-36f5-4129-9f22-8d18fe8b24ed.png#averageHue=%230a0a0a&clientId=u6c33c667-b75d-4&from=paste&height=864&id=u9ac301f7&originHeight=864&originWidth=1705&originalType=binary&ratio=1&rotation=0&showTitle=false&size=369264&status=done&style=none&taskId=u4375f99b-1cc7-47b0-aaee-c1b5d0b0cee&title=&width=1705)
<a name="w37pj"></a>
## 更改像素格式
可以通过ffmpeg -pix_fmts查看所有可用像素格式的列表<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686129977233-50ff5dc0-ff6f-4e2d-a91f-aa370a0fc671.png#averageHue=%23080808&clientId=u6c33c667-b75d-4&from=paste&height=1153&id=u7865d07c&originHeight=1153&originWidth=2477&originalType=binary&ratio=1&rotation=0&showTitle=false&size=532685&status=done&style=none&taskId=ubc7caf4c-0371-4669-a489-e88b78d0290&title=&width=2477)
<a name="j5wui"></a>
# 添加音频
<a name="uTuKy"></a>
## 图片序列转化成视频的同时添加音频文件到视频文件中
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686130405876-af47416a-f6fb-40b2-b5db-e34f738af46a.png#averageHue=%230f0f0f&clientId=u6c33c667-b75d-4&from=paste&height=852&id=u1410c803&originHeight=852&originWidth=2364&originalType=binary&ratio=1&rotation=0&showTitle=false&size=533660&status=done&style=none&taskId=u4d1db221-1f51-4f12-8a3c-d7c387dac4a&title=&width=2364)
<a name="ATFEi"></a>
## 设置输出的音频的选项
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686130874110-84c2e473-ad7c-4b05-9c9c-1acb50e1830f.png#averageHue=%230b0b0b&clientId=u6c33c667-b75d-4&from=paste&height=992&id=oNVIM&originHeight=992&originWidth=2369&originalType=binary&ratio=1&rotation=0&showTitle=false&size=516865&status=done&style=none&taskId=u48322327-df09-4cc1-b951-ddbaec0a5a5&title=&width=2369)
<a name="vzbSp"></a>
## 当音频长度比视频长度要长时，如何舍弃掉多余的视频
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686132160801-b3febdd4-1f01-40e5-8ccb-f4679871af4d.png#averageHue=%230a0a0a&clientId=u6c33c667-b75d-4&from=paste&height=901&id=u6594224c&originHeight=901&originWidth=2365&originalType=binary&ratio=1&rotation=0&showTitle=false&size=392659&status=done&style=none&taskId=u73a43970-1547-47ba-a471-35734b06daa&title=&width=2365)
<a name="yZrJq"></a>
## 当音频长度比视频长度短时
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686132288036-bf8fb09d-93f9-4713-b7c8-c8ee95926413.png#averageHue=%23080808&clientId=u6c33c667-b75d-4&from=paste&height=1037&id=u0ecf5fcc&originHeight=1037&originWidth=2433&originalType=binary&ratio=1&rotation=0&showTitle=false&size=446558&status=done&style=none&taskId=u2d13a6dc-4b3f-4740-bdfe-770199092a8&title=&width=2433)
<a name="dj98o"></a>
# Codecs and Containers 编码解码器与容器
<a name="kv4cp"></a>
## codec(编码解码器)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686190062804-425ffdb1-4c3c-4659-adbd-0d83c7ca4530.png#averageHue=%230c0c0c&clientId=uf7add6b9-7201-4&from=paste&height=776&id=ucc93652e&originHeight=776&originWidth=2250&originalType=binary&ratio=1&rotation=0&showTitle=false&size=422925&status=done&style=none&taskId=u50a6ad35-7470-414c-a503-daabf0aac43&title=&width=2250)
<a name="oHy6l"></a>
## Container（容器，指文件格式）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686190174798-0fd4fa3d-0650-4c8a-8abe-53aa1cd3a247.png#averageHue=%23080808&clientId=uf7add6b9-7201-4&from=paste&height=1067&id=uc8b50c2c&originHeight=1067&originWidth=1974&originalType=binary&ratio=1&rotation=0&showTitle=false&size=315549&status=done&style=none&taskId=u48544d8c-1c81-49c0-b0cb-62d7a2ffeff&title=&width=1974)
<a name="gd6ma"></a>
## file encoding（文件编码）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686190317542-311861f5-5390-41d8-ada3-cfdd2061eeb5.png#averageHue=%23090909&clientId=uf7add6b9-7201-4&from=paste&height=694&id=ua45cb5fa&originHeight=694&originWidth=1754&originalType=binary&ratio=1&rotation=0&showTitle=false&size=234212&status=done&style=none&taskId=u0222d8b4-8476-433e-b545-1eff4edf0a5&title=&width=1754)
<a name="bvkkE"></a>
## Converting Containers 转换文件格式
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686190621098-bb317d51-0319-47e4-ac07-3657edaf30a1.png#averageHue=%230e0e0e&clientId=uf7add6b9-7201-4&from=paste&height=481&id=u1e8581a9&originHeight=481&originWidth=1541&originalType=binary&ratio=1&rotation=0&showTitle=false&size=206584&status=done&style=none&taskId=ue6256960-625a-4fd4-96b8-d465f2c949c&title=&width=1541)
<a name="Jo1VZ"></a>
## Transcoding转码
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686190600115-0c09d4d5-06b6-484e-8398-d839ccc02664.png#averageHue=%230c0c0c&clientId=uf7add6b9-7201-4&from=paste&height=788&id=u231eea2b&originHeight=788&originWidth=2420&originalType=binary&ratio=1&rotation=0&showTitle=false&size=427805&status=done&style=none&taskId=u86262856-2ed1-4152-a3a5-092b0b9d9da&title=&width=2420)
<a name="PTy14"></a>
# Converting and transcoding 转码
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686191116971-5d909224-2fca-4f71-a0b0-34e45a1156ab.png#averageHue=%230a0a0a&clientId=uf7add6b9-7201-4&from=paste&height=1087&id=u48eecded&originHeight=1087&originWidth=2119&originalType=binary&ratio=1&rotation=0&showTitle=false&size=494248&status=done&style=none&taskId=u29ffa33b-745a-42a2-8b9d-80122b2f02a&title=&width=2119)
<a name="xuN0e"></a>
# Generating an Image Sequence生成图像序列
图像序列转成视频：![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686194214627-7968db08-35de-4e93-ae01-140887c3cbe7.png#averageHue=%230e2d5c&clientId=uff736556-ac5a-4&from=paste&height=58&id=u429bbf67&originHeight=58&originWidth=770&originalType=binary&ratio=1&rotation=0&showTitle=false&size=37111&status=done&style=none&taskId=u667f26b6-369d-41dc-b5aa-ee825dd3dca&title=&width=770)<br />视频转成图像序列（PNG）：![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686194433526-204c6bce-0b27-4c2f-a119-fb65fc8d592b.png#averageHue=%23102e5d&clientId=uff736556-ac5a-4&from=paste&height=49&id=u3fbf9dc8&originHeight=49&originWidth=684&originalType=binary&ratio=1&rotation=0&showTitle=false&size=32421&status=done&style=none&taskId=ubaf72023-63af-4794-8034-efbe6d68366&title=&width=684)  png格式文件大小更大，生成质量更高<br />视频转成图像序列（JPG）：![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686194832660-8cdb14c5-6c12-487b-87d8-1284a35d7d01.png#averageHue=%2312305e&clientId=uff736556-ac5a-4&from=paste&height=39&id=u39b57b48&originHeight=39&originWidth=821&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36686&status=done&style=none&taskId=uba9284bc-6da1-4485-a605-b81e40e3793&title=&width=821) jpg格式文件大小很小，默认生成质量低，但是可以通过 -qscale:v 4  来提高质量， 数值为（1-31）数值越小质量越高。
<a name="Gp8kS"></a>
# 控制是否覆盖
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686206387464-34aab456-d2c6-42eb-b0ec-054e3c10f61d.png#averageHue=%23c2c7cc&clientId=uff736556-ac5a-4&from=paste&height=96&id=u1e3663bb&originHeight=96&originWidth=482&originalType=binary&ratio=1&rotation=0&showTitle=false&size=47058&status=done&style=none&taskId=u71aace21-91de-497f-991d-32ca517ce2d&title=&width=482)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686206317187-2d0b3598-3a77-4f3f-83a5-7906aa9eda7a.png#averageHue=%2314305c&clientId=uff736556-ac5a-4&from=paste&height=34&id=ub34239bf&originHeight=34&originWidth=697&originalType=binary&ratio=1&rotation=0&showTitle=false&size=26946&status=done&style=none&taskId=u2c59d3a2-6931-4f20-af8a-0e1eea36da3&title=&width=697)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686206376676-d456302e-ad81-404f-9788-5d55e48f2d99.png#averageHue=%23183562&clientId=uff736556-ac5a-4&from=paste&height=23&id=u8fd13bb1&originHeight=23&originWidth=668&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25471&status=done&style=none&taskId=ud3831a4a-f21b-4fa5-8452-5877189da09&title=&width=668)
<a name="AWNE1"></a>
# 通过python调用ffmpeg
```python
import subprocess


FFMPEG_PATH = "D:/ffmpeg-master-latest-win64-gpl-shared/bin/ffmpeg.exe"


def encode_image_sequence(image_seq_path, output_path, framerate=24, crf=21, preset="ultrafast", audio_path=None):


    ffmpeg_cmd = FFMPEG_PATH
    ffmpeg_cmd += ' -y'
    ffmpeg_cmd += ' -framerate {0}'.format(framerate)
    ffmpeg_cmd += ' -i {0}'.format(image_seq_path)
    if audio_path:
        ffmpeg_cmd += ' -i {0}'.format(audio_path)
    
    ffmpeg_cmd += ' -c:v libx264 -crf {0} -preset {1}'.format(crf,preset)
    if audio_path:
        ffmpeg_cmd += ' -c:a aac -filter_complex "[1:0] apad" -shortest'
    
    ffmpeg_cmd += ' {0}'.format(output_path)
    
    print(ffmpeg_cmd)
    subprocess.call(ffmpeg_cmd)



if __name__ == "__main__":


    img_seq_path = "D:/ffmpeg-master-latest-win64-gpl-shared/bin/_image_sequences/tears_of_steel_100_frames/overrun.%04d.png"    
    audio_path = "D:/ffmpeg-master-latest-win64-gpl-shared/bin/_audio/overrun.wav"
    output_path = "D:/ffmpeg-master-latest-win64-gpl-shared/bin/overrun.mp4"


    encode_image_sequence(img_seq_path,output_path,audio_path=audio_path)
```
<a name="h02ZQ"></a>
# 使用Pyside2制作带界面的视频转换工具
```python
import os
import subprocess
import sys
from PySide2 import QtGui
from PySide2 import QtWidgets


class TranscodeWindow(QtWidgets.QWidget):


    FFMPEG_PATH = "D:/ffmpeg-master-latest-win64-gpl-shared/bin/ffmpeg.exe"


    QUALITY_OPTIONS = [
        ["very high", "18"], # combobox item label, crf value
        ["high", "20"],
        ["medium", "23"],
        ["low", "26"]
    ]
    QUALITY_DEFAULT = "medium"


    PRESETS = [
        ["very slow", "veryslow"], # combobox item label, preset value
        ["slower", "slower"],
        ["slow", "slow"],
        ["medium", "medium"],
        ["fast", "fast"],
        ["faster", "faster"],
        ["very fast", "veryfast"],
        ["ultra fast", "ultrafast"]
    ]
    PRESET_DEFAULT = "medium"



    def __init__(self):
        super(TranscodeWindow, self).__init__(parent=None)


        self.setWindowTitle("FFmpeg Transcoder")
        self.setMinimumSize(400, 300)


        self.create_widgets()
        self.create_layout()
        self.create_connections()


    def create_widgets(self):
        self.input_path_le = QtWidgets.QLineEdit()
        self.input_path_btn = QtWidgets.QPushButton("...")
        self.input_path_btn.setFixedWidth(30)


        self.output_path_le = QtWidgets.QLineEdit()
        self.output_path_btn = QtWidgets.QPushButton("...")
        self.output_path_btn.setFixedWidth(30)


        self.video_codec_combo = QtWidgets.QComboBox()
        self.video_codec_combo.addItem("h264", "libx264")


        self.quality_combo = QtWidgets.QComboBox()
        for quality_option in self.QUALITY_OPTIONS:
            self.quality_combo.addItem(quality_option[0], quality_option[1])
        self.quality_combo.setCurrentText(self.QUALITY_DEFAULT)


        self.preset_combo = QtWidgets.QComboBox()
        for preset in self.PRESETS:
            self.preset_combo.addItem(preset[0], preset[1])
        self.preset_combo.setCurrentText(self.PRESET_DEFAULT)


        self.audio_codec_combo = QtWidgets.QComboBox()
        self.audio_codec_combo.addItem("aac", "aac")


        self.transcode_btn = QtWidgets.QPushButton("Transcode")
        self.cancel_btn = QtWidgets.QPushButton("Cancel")


    def create_layout(self):


        input_grp = QtWidgets.QGroupBox("Input Path")
        input_grp_layout = QtWidgets.QHBoxLayout()
        input_grp_layout.addWidget(self.input_path_le)
        input_grp_layout.addWidget(self.input_path_btn)
        input_grp.setLayout(input_grp_layout)


        output_grp = QtWidgets.QGroupBox("Output Path")
        output_grp_layout = QtWidgets.QHBoxLayout()
        output_grp_layout.addWidget(self.output_path_le)
        output_grp_layout.addWidget(self.output_path_btn)
        output_grp.setLayout(output_grp_layout)


        video_options_grp = QtWidgets.QGroupBox("Video Options")
        video_options_grp_layout = QtWidgets.QFormLayout()
        video_options_grp.setLayout(video_options_grp_layout)


        video_codec_layout = QtWidgets.QHBoxLayout()
        video_codec_layout.addWidget(self.video_codec_combo)
        video_codec_layout.addStretch()
        video_options_grp_layout.addRow("Video Codec:", video_codec_layout)


        quality_layout = QtWidgets.QHBoxLayout()
        quality_layout.addWidget(self.quality_combo)
        quality_layout.ad
        quality_layout.addStretch()
        video_options_grp_layout.addRow("Quality:", quality_layout)


        preset_layout = QtWidgets.QHBoxLayout()
        preset_layout.addWidget(self.preset_combo)
        preset_layout.addStretch()
        video_options_grp_layout.addRow("Preset:", preset_layout)


        audio_options_grp = QtWidgets.QGroupBox("Audio Options")
        audio_options_grp_layout = QtWidgets.QFormLayout()
        audio_options_grp.setLayout(audio_options_grp_layout)


        audio_codec_layout = QtWidgets.QHBoxLayout()
        audio_codec_layout.addWidget(self.audio_codec_combo)
        audio_codec_layout.addStretch()
        audio_options_grp_layout.addRow("Audio Codec:", audio_codec_layout)
        
        options_layout = QtWidgets.QHBoxLayout()
        options_layout.addWidget(video_options_grp)
        options_layout.addWidget(audio_options_grp)


        button_layout = QtWidgets.QHBoxLayout()
        button_layout.addStretch()
        button_layout.addWidget(self.transcode_btn)
        button_layout.addWidget(self.cancel_btn)


        main_layout = QtWidgets.QVBoxLayout(self)
        main_layout.addWidget(input_grp)
        main_layout.addWidget(output_grp)
        main_layout.addLayout(options_layout)
        main_layout.addStretch()
        main_layout.addLayout(button_layout)


    def create_connections(self):
        self.input_path_btn.clicked.connect(self.set_input_path)
        self.output_path_btn.clicked.connect(self.set_output_path)


        self.transcode_btn.clicked.connect(self.transcode)
        self.cancel_btn.clicked.connect(self.close)


    def set_input_path(self):
        filters = ""
        selected_filter = ""


        input_path, selected_filter = QtWidgets.QFileDialog.getOpenFileName(self, "Select an Input File", "", filters, selected_filter)
        if input_path:
            self.input_path_le.setText(input_path)


    def set_output_path(self):
        filters = "*.mp4"
        selected_filter = "*.mp4"


        output_path, selected_filter = QtWidgets.QFileDialog.getSaveFileName(self, "Save File As", "", filters, selected_filter)
        if output_path:
            self.output_path_le.setText(output_path)


    def transcode(self):
        
        input_path = self.input_path_le.text()
        if not input_path:
            QtWidgets.QMessageBox.critical(self, "Transcode Error", "Input path not set")
            return
        if not os.path.exists(input_path):
            QtWidgets.QMessageBox.critical(self, "Transcode Error", "Input path does not exist")
            return


        output_path = self.output_path_le.text()
        if not output_path:
            QtWidgets.QMessageBox.critical(self, "Transcode Error", "Output path not set")
            return


        video_codec = self.video_codec_combo.currentData()
        crf = self.quality_combo.currentData()
        preset = self.preset_combo.currentData()


        audio_codec = self.audio_codec_combo.currentData()


        args = [self.FFMPEG_PATH]                                             # executable path
        args.extend(["-hide_banner", "-y"])                                   # global options
        args.extend(["-i", input_path])                                       # input path
        args.extend(["-c:v", video_codec, "-crf", crf, "-preset", preset])    # video output options
        args.extend(["-c:a", audio_codec])                                    # audio output options
        args.append(output_path)                                              # output path


        subprocess.call(args)


        QtWidgets.QMessageBox.information(self, "Transcode Complete", "File transcode operation complete.")



if __name__ == "__main__":
    app = QtWidgets.QApplication(sys.argv)


    window = TranscodeWindow()
    window.show()


    app.exec_()
```
<a name="wxhmb"></a>
# 修剪视频
<a name="n6eyl"></a>
## 舍弃前面的视频内容
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686300194202-542b1d59-9fe0-4a2e-9f41-46fdd21e46a5.png#averageHue=%23090909&clientId=u3813901e-6645-4&from=paste&height=896&id=u9d04f701&originHeight=896&originWidth=2383&originalType=binary&ratio=1&rotation=0&showTitle=false&size=396214&status=done&style=none&taskId=ue363f098-0bf3-4660-b6fb-c1a2ebdcfb6&title=&width=2383)
<a name="rpVUA"></a>
## 舍弃最后或中间的视频内容
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686300292895-ab2f1585-7da6-4d84-a29c-cb5183d9ca08.png#averageHue=%23080808&clientId=u3813901e-6645-4&from=paste&height=1086&id=u1e938456&originHeight=1086&originWidth=2122&originalType=binary&ratio=1&rotation=0&showTitle=false&size=380639&status=done&style=none&taskId=ue9b618ec-c23c-460e-8cbe-6e54ea8f712&title=&width=2122)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686301468647-c81def59-c870-4984-9281-4cbeae89f43d.png#averageHue=%23173159&clientId=u3813901e-6645-4&from=paste&height=38&id=u7d8e8d6e&originHeight=38&originWidth=1179&originalType=binary&ratio=1&rotation=0&showTitle=false&size=54594&status=done&style=none&taskId=u0851f117-2246-4b95-9a00-ed5c94fdfd8&title=&width=1179)
<a name="FyRSV"></a>
## 输出指定时间的视频
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686300686892-f137b300-3d65-4dc2-af60-e7c56175fd02.png#averageHue=%23070707&clientId=u3813901e-6645-4&from=paste&height=729&id=u64b10927&originHeight=729&originWidth=2366&originalType=binary&ratio=1&rotation=0&showTitle=false&size=228416&status=done&style=none&taskId=uf643b9b5-4e3a-4ab5-a5cf-2f6bd6ca01c&title=&width=2366)
<a name="VBigi"></a>
## 警告
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686300777026-a3422b34-c23a-4155-bbd0-60065c2237a9.png#averageHue=%23090909&clientId=u3813901e-6645-4&from=paste&height=909&id=u5f2e2afa&originHeight=909&originWidth=1900&originalType=binary&ratio=1&rotation=0&showTitle=false&size=334576&status=done&style=none&taskId=u1b88ae88-1ca2-421f-bf9d-fc0cf6c2a40&title=&width=1900)
<a name="qa6ga"></a>
# 提取视频的第一帧的图片
获得视频的第一帧的图片：![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686302638281-804ddb84-1921-4383-a272-8ccec992fa64.png#averageHue=%23102c57&clientId=u3813901e-6645-4&from=paste&height=53&id=ue9d0966c&originHeight=53&originWidth=924&originalType=binary&ratio=1&rotation=0&showTitle=false&size=37484&status=done&style=none&taskId=u22801a7e-ea0a-47ec-9339-37e4618236f&title=&width=924)
<a name="Obkj2"></a>
# 提取视频的中间处的一帧图片
其中ffprobe.exe是FFmpeg提供的用来查看视频信息的exe文件
```python
import subprocess


FFMPEG_PATH = "D:/ffmpeg/ffmpeg-4.2.1/bin/ffmpeg.exe"
FFPROBE_PATH = "D:/ffmpeg/ffmpeg-4.2.1/bin/ffprobe.exe"



def extract_middle_image(source_path, output_path):


    ffprobe_cmd = FFPROBE_PATH
    ffprobe_cmd += ' -v error -show_entries format=duration -of default=noprint_wrappers=1:nokey=1 '
    ffprobe_cmd += source_path


    duration = float(subprocess.check_output(ffprobe_cmd))


    ffmpeg_cmd = FFMPEG_PATH
    ffmpeg_cmd += ' -y -i {0} -ss {1} -frames:v 1 {2}'.format(source_path, duration/2.0, output_path)


    print(ffmpeg_cmd)
    subprocess.call(ffmpeg_cmd)



def encode_image_sequence(image_seq_path, output_path, framerate=24, crf=21, preset="ultrafast", audio_path=None):


    ffmpeg_cmd = FFMPEG_PATH
    ffmpeg_cmd += ' -y '
    ffmpeg_cmd += ' -framerate {0}'.format(framerate)
    ffmpeg_cmd += ' -i {0}'.format(image_seq_path)
    if audio_path:
        ffmpeg_cmd += ' -i {0}'.format(audio_path)


    ffmpeg_cmd += ' -c:v libx264 -crf {0} -preset {1}'.format(crf, preset)
    if audio_path:
        ffmpeg_cmd += ' -c:a aac -filter_complex "[1:0] apad" -shortest'


    ffmpeg_cmd += ' {0}'.format(output_path)


    print(ffmpeg_cmd)
    subprocess.call(ffmpeg_cmd)



if __name__ == "__main__":


    source_path = "D:/ffmpeg/ffmpeg-4.2.1/bin/bbb_shot_060.mp4"
    output_path = "D:/ffmpeg/ffmpeg-4.2.1/bin/middle_frame.png"


    extract_middle_image(source_path, output_path)
```
<a name="MWVt3"></a>
# 通过过滤器添加水印
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686304228275-5e64f1b7-abdd-417d-af1d-ea5fe7c97b85.png#averageHue=%23080808&clientId=u3813901e-6645-4&from=paste&height=992&id=ua5f5a6a7&originHeight=992&originWidth=2417&originalType=binary&ratio=1&rotation=0&showTitle=false&size=350093&status=done&style=none&taskId=u848aa727-8b57-486f-934b-f1f4e7b6b4f&title=&width=2417)<br />举例：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686304577780-2882741d-e0d7-4853-ade7-d17a496a50d6.png#averageHue=%23213d67&clientId=u3813901e-6645-4&from=paste&height=32&id=uc62a5349&originHeight=32&originWidth=1120&originalType=binary&ratio=1&rotation=0&showTitle=false&size=44893&status=done&style=none&taskId=u5ad1e4b0-c799-4958-adab-0c8e8681621&title=&width=1120)<br />将图片放到视频的右下角<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686304584475-f26b6af6-78e9-4a13-a504-31e1a2c5b011.png#averageHue=%23244471&clientId=u3813901e-6645-4&from=paste&height=38&id=uae6f2beb&originHeight=38&originWidth=185&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8030&status=done&style=none&taskId=u636266ba-2555-4cd5-9365-fe2769603c1&title=&width=185)这里的[0][1]可以不要，然后(W-w-20):(H-h-20)的意思是水印的位置，水印的位置左边如图所示：W为视频的宽度，w为图片的宽度<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686304684459-6ec4506d-337a-43d2-ab30-b8a3234f5dd6.png#averageHue=%238da355&clientId=u3813901e-6645-4&from=paste&height=756&id=u499b5bd7&originHeight=756&originWidth=1140&originalType=binary&ratio=1&rotation=0&showTitle=false&size=853210&status=done&style=none&taskId=u8459d329-1180-4f83-a877-a3680fff499&title=&width=1140)																																										
<a name="HIx7i"></a>
# 通过过滤器调整添加的水印的大小的透明度
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686536873938-20b89753-bac8-4824-9507-fceecc57a21b.png#averageHue=%23163562&clientId=u3813901e-6645-4&from=paste&height=46&id=ud34da61d&originHeight=46&originWidth=1964&originalType=binary&ratio=1&rotation=0&showTitle=false&size=84264&status=done&style=none&taskId=u0c432a9c-76ae-4e91-a53d-910228f8d05&title=&width=1964)<br />过滤器为蓝色的字体， [1]scale 是指将前面的输入中的第二个进行缩放。  iw为原图片的像素大小。 iw也可以换成数字代指像素，h=-1的意思是让ffmpeg根据前面的宽度w的大小自动调整高度h的大小。然后后面的[image_scaled]的意思是通过过滤器修改后的图片的名字（因为后面要用到这个更改过缩放的图片，因此先定义一个暂时的名字），[image_scaled]lut=a=val*0.4[image_final];的意思是在原来的基础上将alpha通道的大小调整为原来的0.4倍，然后再给个修改后的名字[image_final]，这个名字是自定义的。然后[0][image_final]overlay=(W-w-20):(H-h-20)为添加水印。
<a name="s4cNX"></a>
# 刻录时间码
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1686633394546-2439f3e8-dcf0-457c-bf4e-6ab6ee27e461.png#averageHue=%23244470&clientId=u2a7e5a9c-aa6d-4&from=paste&height=44&id=uebf751ac&originHeight=44&originWidth=2087&originalType=binary&ratio=1&rotation=0&showTitle=false&size=91397&status=done&style=none&taskId=ua56ab983-5706-4f7c-b436-06f70a2a668&title=&width=2087)
