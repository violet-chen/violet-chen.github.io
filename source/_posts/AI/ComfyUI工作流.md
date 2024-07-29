---
title: ComfyUI工作流
tags: ComfyUI
categories: AI
abbrlink: 3f58fa1c
date: 2024-01-08 18:21:00
---
# 工作流的参考方法
方法一:将图片拖拽进ComfyUI中
方法二:复制json内容粘贴至ComfyUI

# ipadapter配合controlnet
![Alt text](ipadapter_and_controlnet.png)

# 只需要通过一个节点就可以负责Lora一个或多个的添加
![Alt text](image.png)
工作流解析:
通过设置节点参数来使用一个或多个Lora
![Alt text](image-1.png)

# 局部重绘
![Alt text](image-2.png)
省流版:
其中VAE Encode(for Inpainting) 和 Set Latent Noise Mask效果差不多,可以都测试测试看哪个效果好.
![Alt text](image-4.png)

# PS投屏实时绘画
```json
{
  "last_node_id": 169,
  "last_link_id": 326,
  "nodes": [
    {
      "id": 107,
      "type": "Note",
      "pos": [
        292.05923012390133,
        649.03209475708
      ],
      "size": {
        "0": 293.3884582519531,
        "1": 158.1380615234375
      },
      "flags": {},
      "order": 0,
      "mode": 0,
      "title": "采样器数值说明",
      "properties": {
        "text": ""
      },
      "widgets_values": [
        "1.seed:值为-1时每次出图都是随机的\n2.steps:意思是步数,值越高质量越高,相应的出图速度越慢,实时绘画建议4~8.\n3.cfg:cfg越大生成的图就越符合提示词内容,由于使用了LCM来加速了实时绘画出图的速度因此需要控制在1~2最好.\n4.sampler_name:采样器dpmpp对应SDWebUI的dmp++\n5.scheduler: 采样调度,一般选择karras或者normal即可                        \n6.denoise:重绘幅度,值越大重绘幅度越大\n7.preview_method:预览方法,不重要,跟出图效果无关\n8.vae_decode:控制如何使用vae,保持默认即可"
      ],
      "color": "#432",
      "bgcolor": "#653"
    },
    {
      "id": 108,
      "type": "Note",
      "pos": [
        -949.0268085632321,
        1128.7023533935537
      ],
      "size": {
        "0": 322.2235107421875,
        "1": 107.0997085571289
      },
      "flags": {},
      "order": 1,
      "mode": 0,
      "title": "如何设置PS与ComfyUI连接",
      "properties": {
        "text": ""
      },
      "widgets_values": [
        "1.点击ShareScreen按钮,会弹出一个窗口,有三种模式,分别是Chrome标签页,窗口,整个屏幕.选择窗口模式,然后找到要与Comfyui连接的PS项目.点击选中并点击分享按钮.\n2.点击SetArea按钮,在弹出的窗口中框住画布区域,可以理解为框住的画布区域就是图生图流程中提供的参考图.\n3.点击LiveRun按钮"
      ],
      "color": "#432",
      "bgcolor": "#653"
    },
    {
      "id": 109,
      "type": "LoraLoader",
      "pos": [
        -1307,
        802
      ],
      "size": {
        "0": 337.1312255859375,
        "1": 126
      },
      "flags": {
        "collapsed": false
      },
      "order": 9,
      "mode": 4,
      "inputs": [
        {
          "name": "model",
          "type": "MODEL",
          "link": 177,
          "label": "model"
        },
        {
          "name": "clip",
          "type": "CLIP",
          "link": 178,
          "label": "clip",
          "slot_index": 1
        }
      ],
      "outputs": [
        {
          "name": "MODEL",
          "type": "MODEL",
          "links": [
            179
          ],
          "shape": 3,
          "label": "MODEL",
          "slot_index": 0
        },
        {
          "name": "CLIP",
          "type": "CLIP",
          "links": [
            180
          ],
          "shape": 3,
          "label": "CLIP",
          "slot_index": 1
        }
      ],
      "properties": {
        "Node name for S&R": "LoraLoader"
      },
      "widgets_values": [
        "add_detail.safetensors",
        1,
        1
      ]
    },
    {
      "id": 10,
      "type": "VAELoader",
      "pos": [
        -488,
        1192
      ],
      "size": {
        "0": 348.7921447753906,
        "1": 58
      },
      "flags": {
        "collapsed": false
      },
      "order": 2,
      "mode": 0,
      "outputs": [
        {
          "name": "VAE",
          "type": "VAE",
          "links": [
            30,
            144
          ],
          "shape": 3,
          "label": "VAE",
          "slot_index": 0
        }
      ],
      "title": "加载VAE",
      "properties": {
        "Node name for S&R": "VAELoader"
      },
      "widgets_values": [
        "Anything-V3.0.vae.pt"
      ]
    },
    {
      "id": 82,
      "type": "ModelSamplingDiscrete",
      "pos": [
        -476,
        556
      ],
      "size": {
        "0": 315,
        "1": 82
      },
      "flags": {
        "collapsed": false
      },
      "order": 12,
      "mode": 0,
      "inputs": [
        {
          "name": "model",
          "type": "MODEL",
          "link": 181,
          "label": "model",
          "slot_index": 0
        }
      ],
      "outputs": [
        {
          "name": "MODEL",
          "type": "MODEL",
          "links": [
            140
          ],
          "shape": 3,
          "slot_index": 0,
          "label": "MODEL"
        }
      ],
      "properties": {
        "Node name for S&R": "ModelSamplingDiscrete"
      },
      "widgets_values": [
        "lcm",
        false
      ]
    },
    {
      "id": 5,
      "type": "CLIPTextEncode",
      "pos": [
        -495,
        954
      ],
      "size": {
        "0": 380.93463134765625,
        "1": 185.83177185058594
      },
      "flags": {
        "collapsed": false
      },
      "order": 14,
      "mode": 0,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 183,
          "label": "clip"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            142
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "反向提示词",
      "properties": {
        "Node name for S&R": "CLIPTextEncode"
      },
      "widgets_values": [
        "lowres, bad anatomy, bad hands, text, error, missing fingers, extra digit, fewer digits, cropped, worst quality, low quality, normal quality, jpeg artifacts, signature, watermark, username, blurry"
      ]
    },
    {
      "id": 3,
      "type": "CheckpointLoaderSimple",
      "pos": [
        -2230,
        810
      ],
      "size": {
        "0": 321.88446044921875,
        "1": 98
      },
      "flags": {
        "collapsed": false
      },
      "order": 3,
      "mode": 0,
      "outputs": [
        {
          "name": "MODEL",
          "type": "MODEL",
          "links": [
            14
          ],
          "shape": 3,
          "label": "MODEL",
          "slot_index": 0
        },
        {
          "name": "CLIP",
          "type": "CLIP",
          "links": [
            16
          ],
          "shape": 3,
          "label": "CLIP",
          "slot_index": 1
        },
        {
          "name": "VAE",
          "type": "VAE",
          "links": null,
          "shape": 3,
          "label": "VAE"
        }
      ],
      "title": "加载模型",
      "properties": {
        "Node name for S&R": "CheckpointLoaderSimple"
      },
      "widgets_values": [
        "cardosAnimated_v30.safetensors"
      ]
    },
    {
      "id": 4,
      "type": "CLIPTextEncode",
      "pos": [
        -494,
        718
      ],
      "size": {
        "0": 382.7315368652344,
        "1": 166.9505615234375
      },
      "flags": {},
      "order": 13,
      "mode": 0,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 182,
          "label": "clip"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            141
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "正向提示词",
      "properties": {
        "Node name for S&R": "CLIPTextEncode"
      },
      "widgets_values": [
        "natural light, incandescent light, fiber optic,\nmorning light,Moody Lighting, edge light, movie\nlighting, studio lighting, soft lighting, Distorted\nenergy flow,quantitative, Contra Jour, beautiful\nlighting,emphasizing lighting,global lighting,\nscreen space global lighting,ray tracing global\nlighting, optics，scattering,\nluminescence，shadows,\nroughness,flash, incremental detail and integration,\nultra maximum, element, ultra realistic,ultra\ndetailed"
      ]
    },
    {
      "id": 100,
      "type": "ScreenShare",
      "pos": [
        -947.0268085632321,
        1284.7023533935537
      ],
      "size": {
        "0": 372.8167724609375,
        "1": 276.5818786621094
      },
      "flags": {},
      "order": 4,
      "mode": 0,
      "outputs": [
        {
          "name": "IMAGE",
          "type": "IMAGE",
          "links": [
            175
          ],
          "shape": 3,
          "label": "IMAGE",
          "slot_index": 0
        },
        {
          "name": "MASK",
          "type": "MASK",
          "links": [],
          "shape": 3,
          "label": "MASK"
        },
        {
          "name": "STRING",
          "type": "STRING",
          "links": null,
          "shape": 3,
          "label": "STRING"
        },
        {
          "name": "INT",
          "type": "INT",
          "links": null,
          "shape": 3,
          "label": "INT"
        }
      ],
      "title": "设置如何共享屏幕",
      "properties": {
        "Node name for S&R": "ScreenShare"
      },
      "widgets_values": [
        null,
        null,
        null,
        null,
        null
      ]
    },
    {
      "id": 21,
      "type": "VAEEncode",
      "pos": [
        -71,
        1293
      ],
      "size": {
        "0": 210,
        "1": 46
      },
      "flags": {
        "collapsed": false
      },
      "order": 10,
      "mode": 0,
      "inputs": [
        {
          "name": "pixels",
          "type": "IMAGE",
          "link": 263,
          "label": "pixels"
        },
        {
          "name": "vae",
          "type": "VAE",
          "link": 30,
          "label": "vae",
          "slot_index": 1
        }
      ],
      "outputs": [
        {
          "name": "LATENT",
          "type": "LATENT",
          "links": [
            301
          ],
          "shape": 3,
          "label": "LATENT",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "VAEEncode"
      }
    },
    {
      "id": 13,
      "type": "LoraLoader",
      "pos": [
        -1840,
        810
      ],
      "size": {
        "0": 337.1312255859375,
        "1": 126
      },
      "flags": {
        "collapsed": false
      },
      "order": 7,
      "mode": 0,
      "inputs": [
        {
          "name": "model",
          "type": "MODEL",
          "link": 14,
          "label": "model"
        },
        {
          "name": "clip",
          "type": "CLIP",
          "link": 16,
          "label": "clip",
          "slot_index": 1
        }
      ],
      "outputs": [
        {
          "name": "MODEL",
          "type": "MODEL",
          "links": [
            177
          ],
          "shape": 3,
          "label": "MODEL",
          "slot_index": 0
        },
        {
          "name": "CLIP",
          "type": "CLIP",
          "links": [
            178
          ],
          "shape": 3,
          "label": "CLIP",
          "slot_index": 1
        }
      ],
      "properties": {
        "Node name for S&R": "LoraLoader"
      },
      "widgets_values": [
        "LCM_LoRA_SD15.safetensors",
        1,
        1
      ]
    },
    {
      "id": 28,
      "type": "ImageScale",
      "pos": [
        -476,
        1305
      ],
      "size": {
        "0": 324.6936340332031,
        "1": 130
      },
      "flags": {},
      "order": 8,
      "mode": 0,
      "inputs": [
        {
          "name": "image",
          "type": "IMAGE",
          "link": 175,
          "label": "image"
        }
      ],
      "outputs": [
        {
          "name": "IMAGE",
          "type": "IMAGE",
          "links": [
            263
          ],
          "shape": 3,
          "label": "IMAGE",
          "slot_index": 0
        }
      ],
      "title": "设置图片分辨率大小",
      "properties": {
        "Node name for S&R": "ImageScale"
      },
      "widgets_values": [
        "nearest-exact",
        576,
        603,
        "disabled"
      ]
    },
    {
      "id": 89,
      "type": "KSampler (Efficient)",
      "pos": [
        222,
        871
      ],
      "size": [
        438.64739990234375,
        579.5003051757812
      ],
      "flags": {},
      "order": 17,
      "mode": 0,
      "inputs": [
        {
          "name": "model",
          "type": "MODEL",
          "link": 140,
          "label": "model",
          "slot_index": 0
        },
        {
          "name": "positive",
          "type": "CONDITIONING",
          "link": 141,
          "label": "positive",
          "slot_index": 1
        },
        {
          "name": "negative",
          "type": "CONDITIONING",
          "link": 142,
          "label": "negative",
          "slot_index": 2
        },
        {
          "name": "latent_image",
          "type": "LATENT",
          "link": 301,
          "label": "latent_image",
          "slot_index": 3
        },
        {
          "name": "optional_vae",
          "type": "VAE",
          "link": 144,
          "label": "optional_vae",
          "slot_index": 4
        },
        {
          "name": "script",
          "type": "SCRIPT",
          "link": null,
          "label": "script"
        }
      ],
      "outputs": [
        {
          "name": "MODEL",
          "type": "MODEL",
          "links": [
            241
          ],
          "shape": 3,
          "label": "MODEL",
          "slot_index": 0
        },
        {
          "name": "CONDITIONING+",
          "type": "CONDITIONING",
          "links": [
            324
          ],
          "shape": 3,
          "label": "CONDITIONING+",
          "slot_index": 1
        },
        {
          "name": "CONDITIONING-",
          "type": "CONDITIONING",
          "links": [
            313
          ],
          "shape": 3,
          "label": "CONDITIONING-",
          "slot_index": 2
        },
        {
          "name": "LATENT",
          "type": "LATENT",
          "links": [],
          "shape": 3,
          "label": "LATENT",
          "slot_index": 3
        },
        {
          "name": "VAE",
          "type": "VAE",
          "links": [
            245,
            280
          ],
          "shape": 3,
          "label": "VAE",
          "slot_index": 4
        },
        {
          "name": "IMAGE",
          "type": "IMAGE",
          "links": [
            176,
            186
          ],
          "shape": 3,
          "label": "IMAGE",
          "slot_index": 5
        }
      ],
      "title": "采样器",
      "properties": {
        "Node name for S&R": "KSampler (Efficient)"
      },
      "widgets_values": [
        863389622127326,
        null,
        7,
        1.5,
        "dpmpp_sde_gpu",
        "karras",
        0.33,
        "auto",
        "true"
      ],
      "color": "#332222",
      "bgcolor": "#553333",
      "shape": 1
    },
    {
      "id": 110,
      "type": "LoraLoader",
      "pos": [
        -947,
        802
      ],
      "size": {
        "0": 315,
        "1": 126
      },
      "flags": {},
      "order": 11,
      "mode": 4,
      "inputs": [
        {
          "name": "model",
          "type": "MODEL",
          "link": 179,
          "label": "model"
        },
        {
          "name": "clip",
          "type": "CLIP",
          "link": 180,
          "label": "clip",
          "slot_index": 1
        }
      ],
      "outputs": [
        {
          "name": "MODEL",
          "type": "MODEL",
          "links": [
            181
          ],
          "shape": 3,
          "label": "MODEL",
          "slot_index": 0
        },
        {
          "name": "CLIP",
          "type": "CLIP",
          "links": [
            182,
            183,
            325,
            326
          ],
          "shape": 3,
          "label": "CLIP",
          "slot_index": 1
        }
      ],
      "properties": {
        "Node name for S&R": "LoraLoader"
      },
      "widgets_values": [
        "animeoutlineV4_16.safetensors",
        1,
        1
      ]
    },
    {
      "id": 106,
      "type": "FloatingVideo",
      "pos": [
        -27,
        1601
      ],
      "size": [
        749.3804321289062,
        58
      ],
      "flags": {
        "collapsed": false
      },
      "order": 18,
      "mode": 0,
      "inputs": [
        {
          "name": "images",
          "type": "IMAGE",
          "link": 176,
          "label": "images"
        }
      ],
      "properties": {
        "Node name for S&R": "FloatingVideo"
      },
      "widgets_values": [
        null
      ]
    },
    {
      "id": 166,
      "type": "CLIPTextEncode",
      "pos": [
        786,
        917
      ],
      "size": {
        "0": 400,
        "1": 200
      },
      "flags": {},
      "order": 15,
      "mode": 4,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 325,
          "label": "clip"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            322
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "新增调节的正向提示词",
      "properties": {
        "Node name for S&R": "CLIPTextEncode"
      },
      "widgets_values": [
        ""
      ]
    },
    {
      "id": 167,
      "type": "CLIPTextEncode",
      "pos": [
        790,
        1165
      ],
      "size": {
        "0": 400,
        "1": 200
      },
      "flags": {},
      "order": 16,
      "mode": 4,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 326,
          "label": "clip",
          "slot_index": 0
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            317
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "新增调节的反向提示词",
      "properties": {
        "Node name for S&R": "CLIPTextEncode"
      },
      "widgets_values": [
        ""
      ]
    },
    {
      "id": 168,
      "type": "ConditioningCombine",
      "pos": [
        1258,
        1172
      ],
      "size": {
        "0": 342.5999755859375,
        "1": 46
      },
      "flags": {
        "collapsed": true
      },
      "order": 25,
      "mode": 4,
      "inputs": [
        {
          "name": "conditioning_1",
          "type": "CONDITIONING",
          "link": 319,
          "label": "conditioning_1",
          "slot_index": 0
        },
        {
          "name": "conditioning_2",
          "type": "CONDITIONING",
          "link": 317,
          "label": "conditioning_2",
          "slot_index": 1
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            320
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "ConditioningCombine"
      }
    },
    {
      "id": 169,
      "type": "ConditioningConcat",
      "pos": [
        1255,
        958
      ],
      "size": {
        "0": 380.4000244140625,
        "1": 46
      },
      "flags": {
        "collapsed": true
      },
      "order": 24,
      "mode": 4,
      "inputs": [
        {
          "name": "conditioning_to",
          "type": "CONDITIONING",
          "link": 321,
          "label": "conditioning_to"
        },
        {
          "name": "conditioning_from",
          "type": "CONDITIONING",
          "link": 322,
          "label": "conditioning_from"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            323
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "ConditioningConcat"
      }
    },
    {
      "id": 137,
      "type": "KSampler",
      "pos": [
        1522,
        1003
      ],
      "size": [
        294.13656779296934,
        273.1279147644045
      ],
      "flags": {},
      "order": 26,
      "mode": 4,
      "inputs": [
        {
          "name": "model",
          "type": "MODEL",
          "link": 241,
          "label": "model",
          "slot_index": 0
        },
        {
          "name": "positive",
          "type": "CONDITIONING",
          "link": 323,
          "label": "positive"
        },
        {
          "name": "negative",
          "type": "CONDITIONING",
          "link": 320,
          "label": "negative",
          "slot_index": 2
        },
        {
          "name": "latent_image",
          "type": "LATENT",
          "link": 246,
          "label": "latent_image"
        }
      ],
      "outputs": [
        {
          "name": "LATENT",
          "type": "LATENT",
          "links": [
            279
          ],
          "shape": 3,
          "label": "LATENT",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "KSampler"
      },
      "widgets_values": [
        982036911888596,
        "randomize",
        12,
        1.6,
        "dpmpp_sde_gpu",
        "karras",
        0.3
      ]
    },
    {
      "id": 115,
      "type": "UpscaleModelLoader",
      "pos": [
        777,
        487
      ],
      "size": {
        "0": 315,
        "1": 58
      },
      "flags": {},
      "order": 5,
      "mode": 4,
      "outputs": [
        {
          "name": "UPSCALE_MODEL",
          "type": "UPSCALE_MODEL",
          "links": [
            184
          ],
          "shape": 3,
          "label": "UPSCALE_MODEL"
        }
      ],
      "properties": {
        "Node name for S&R": "UpscaleModelLoader"
      },
      "widgets_values": [
        "4x-UltraSharp.pth"
      ]
    },
    {
      "id": 133,
      "type": "ImageScaleBy",
      "pos": [
        779,
        602
      ],
      "size": {
        "0": 315,
        "1": 82
      },
      "flags": {},
      "order": 20,
      "mode": 4,
      "inputs": [
        {
          "name": "image",
          "type": "IMAGE",
          "link": 231,
          "label": "image"
        }
      ],
      "outputs": [
        {
          "name": "IMAGE",
          "type": "IMAGE",
          "links": [
            244,
            303
          ],
          "shape": 3,
          "label": "IMAGE",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "ImageScaleBy"
      },
      "widgets_values": [
        "nearest-exact",
        0.5
      ]
    },
    {
      "id": 163,
      "type": "TilePreprocessor",
      "pos": [
        1164,
        585
      ],
      "size": {
        "0": 315,
        "1": 82
      },
      "flags": {},
      "order": 22,
      "mode": 4,
      "inputs": [
        {
          "name": "image",
          "type": "IMAGE",
          "link": 303,
          "label": "image"
        }
      ],
      "outputs": [
        {
          "name": "IMAGE",
          "type": "IMAGE",
          "links": [
            304
          ],
          "shape": 3,
          "label": "IMAGE",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "TilePreprocessor"
      },
      "widgets_values": [
        3,
        512
      ]
    },
    {
      "id": 138,
      "type": "VAEEncode",
      "pos": [
        814,
        800
      ],
      "size": {
        "0": 210,
        "1": 46
      },
      "flags": {
        "collapsed": true
      },
      "order": 21,
      "mode": 4,
      "inputs": [
        {
          "name": "pixels",
          "type": "IMAGE",
          "link": 244,
          "label": "pixels"
        },
        {
          "name": "vae",
          "type": "VAE",
          "link": 245,
          "label": "vae",
          "slot_index": 1
        }
      ],
      "outputs": [
        {
          "name": "LATENT",
          "type": "LATENT",
          "links": [
            246
          ],
          "shape": 3,
          "label": "LATENT",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "VAEEncode"
      }
    },
    {
      "id": 165,
      "type": "ControlNetLoader",
      "pos": [
        796,
        759
      ],
      "size": {
        "0": 315,
        "1": 58
      },
      "flags": {
        "collapsed": true
      },
      "order": 6,
      "mode": 4,
      "outputs": [
        {
          "name": "CONTROL_NET",
          "type": "CONTROL_NET",
          "links": [
            307
          ],
          "shape": 3,
          "label": "CONTROL_NET"
        }
      ],
      "properties": {
        "Node name for S&R": "ControlNetLoader"
      },
      "widgets_values": [
        "ControlNet-v1-1/control_v11f1e_sd15_tile.pth"
      ]
    },
    {
      "id": 164,
      "type": "ControlNetApplyAdvanced",
      "pos": [
        1161,
        710
      ],
      "size": {
        "0": 315,
        "1": 166
      },
      "flags": {},
      "order": 23,
      "mode": 4,
      "inputs": [
        {
          "name": "positive",
          "type": "CONDITIONING",
          "link": 324,
          "label": "positive",
          "slot_index": 0
        },
        {
          "name": "negative",
          "type": "CONDITIONING",
          "link": 313,
          "label": "negative"
        },
        {
          "name": "control_net",
          "type": "CONTROL_NET",
          "link": 307,
          "label": "control_net",
          "slot_index": 2
        },
        {
          "name": "image",
          "type": "IMAGE",
          "link": 304,
          "label": "image"
        }
      ],
      "outputs": [
        {
          "name": "positive",
          "type": "CONDITIONING",
          "links": [
            321
          ],
          "shape": 3,
          "label": "positive",
          "slot_index": 0
        },
        {
          "name": "negative",
          "type": "CONDITIONING",
          "links": [
            319
          ],
          "shape": 3,
          "label": "negative",
          "slot_index": 1
        }
      ],
      "properties": {
        "Node name for S&R": "ControlNetApplyAdvanced"
      },
      "widgets_values": [
        0.4,
        0,
        1
      ]
    },
    {
      "id": 157,
      "type": "VAEDecode",
      "pos": [
        1911,
        938
      ],
      "size": {
        "0": 210,
        "1": 46
      },
      "flags": {
        "collapsed": true
      },
      "order": 27,
      "mode": 0,
      "inputs": [
        {
          "name": "samples",
          "type": "LATENT",
          "link": 279,
          "label": "samples"
        },
        {
          "name": "vae",
          "type": "VAE",
          "link": 280,
          "label": "vae",
          "slot_index": 1
        }
      ],
      "outputs": [
        {
          "name": "IMAGE",
          "type": "IMAGE",
          "links": [
            282
          ],
          "shape": 3,
          "label": "IMAGE",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "VAEDecode"
      }
    },
    {
      "id": 114,
      "type": "ImageUpscaleWithModel",
      "pos": [
        1145,
        477
      ],
      "size": {
        "0": 241.79998779296875,
        "1": 46
      },
      "flags": {
        "collapsed": false
      },
      "order": 19,
      "mode": 4,
      "inputs": [
        {
          "name": "upscale_model",
          "type": "UPSCALE_MODEL",
          "link": 184,
          "label": "upscale_model",
          "slot_index": 0
        },
        {
          "name": "image",
          "type": "IMAGE",
          "link": 186,
          "label": "image",
          "slot_index": 1
        }
      ],
      "outputs": [
        {
          "name": "IMAGE",
          "type": "IMAGE",
          "links": [
            231
          ],
          "shape": 3,
          "label": "IMAGE",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "ImageUpscaleWithModel"
      }
    },
    {
      "id": 158,
      "type": "PreviewImage",
      "pos": [
        785,
        1624
      ],
      "size": [
        750.4013947012313,
        832.9999910122001
      ],
      "flags": {},
      "order": 28,
      "mode": 4,
      "inputs": [
        {
          "name": "images",
          "type": "IMAGE",
          "link": 282,
          "label": "images"
        }
      ],
      "properties": {
        "Node name for S&R": "PreviewImage"
      }
    }
  ],
  "links": [
    [
      14,
      3,
      0,
      13,
      0,
      "MODEL"
    ],
    [
      16,
      3,
      1,
      13,
      1,
      "CLIP"
    ],
    [
      30,
      10,
      0,
      21,
      1,
      "VAE"
    ],
    [
      140,
      82,
      0,
      89,
      0,
      "MODEL"
    ],
    [
      141,
      4,
      0,
      89,
      1,
      "CONDITIONING"
    ],
    [
      142,
      5,
      0,
      89,
      2,
      "CONDITIONING"
    ],
    [
      144,
      10,
      0,
      89,
      4,
      "VAE"
    ],
    [
      175,
      100,
      0,
      28,
      0,
      "IMAGE"
    ],
    [
      176,
      89,
      5,
      106,
      0,
      "IMAGE"
    ],
    [
      177,
      13,
      0,
      109,
      0,
      "MODEL"
    ],
    [
      178,
      13,
      1,
      109,
      1,
      "CLIP"
    ],
    [
      179,
      109,
      0,
      110,
      0,
      "MODEL"
    ],
    [
      180,
      109,
      1,
      110,
      1,
      "CLIP"
    ],
    [
      181,
      110,
      0,
      82,
      0,
      "MODEL"
    ],
    [
      182,
      110,
      1,
      4,
      0,
      "CLIP"
    ],
    [
      183,
      110,
      1,
      5,
      0,
      "CLIP"
    ],
    [
      184,
      115,
      0,
      114,
      0,
      "UPSCALE_MODEL"
    ],
    [
      186,
      89,
      5,
      114,
      1,
      "IMAGE"
    ],
    [
      231,
      114,
      0,
      133,
      0,
      "IMAGE"
    ],
    [
      241,
      89,
      0,
      137,
      0,
      "MODEL"
    ],
    [
      244,
      133,
      0,
      138,
      0,
      "IMAGE"
    ],
    [
      245,
      89,
      4,
      138,
      1,
      "VAE"
    ],
    [
      246,
      138,
      0,
      137,
      3,
      "LATENT"
    ],
    [
      263,
      28,
      0,
      21,
      0,
      "IMAGE"
    ],
    [
      279,
      137,
      0,
      157,
      0,
      "LATENT"
    ],
    [
      280,
      89,
      4,
      157,
      1,
      "VAE"
    ],
    [
      282,
      157,
      0,
      158,
      0,
      "IMAGE"
    ],
    [
      301,
      21,
      0,
      89,
      3,
      "LATENT"
    ],
    [
      303,
      133,
      0,
      163,
      0,
      "IMAGE"
    ],
    [
      304,
      163,
      0,
      164,
      3,
      "IMAGE"
    ],
    [
      307,
      165,
      0,
      164,
      2,
      "CONTROL_NET"
    ],
    [
      313,
      89,
      2,
      164,
      1,
      "CONDITIONING"
    ],
    [
      317,
      167,
      0,
      168,
      1,
      "CONDITIONING"
    ],
    [
      319,
      164,
      1,
      168,
      0,
      "CONDITIONING"
    ],
    [
      320,
      168,
      0,
      137,
      2,
      "CONDITIONING"
    ],
    [
      321,
      164,
      0,
      169,
      0,
      "CONDITIONING"
    ],
    [
      322,
      166,
      0,
      169,
      1,
      "CONDITIONING"
    ],
    [
      323,
      169,
      0,
      137,
      1,
      "CONDITIONING"
    ],
    [
      324,
      89,
      1,
      164,
      0,
      "CONDITIONING"
    ],
    [
      325,
      110,
      1,
      166,
      0,
      "CLIP"
    ],
    [
      326,
      110,
      1,
      167,
      0,
      "CLIP"
    ]
  ],
  "groups": [
    {
      "title": "第一步",
      "bounding": [
        -1004,
        1062,
        493,
        917
      ],
      "color": "#3f789e",
      "font_size": 24,
      "locked": false
    },
    {
      "title": "设置出图的效果",
      "bounding": [
        135,
        530,
        600,
        998
      ],
      "color": "#3f789e",
      "font_size": 24,
      "locked": false
    },
    {
      "title": "图片放大",
      "bounding": [
        767,
        304,
        1357,
        2185
      ],
      "color": "#3f789e",
      "font_size": 24,
      "locked": false
    }
  ],
  "config": {},
  "extra": {},
  "version": 0.4
}
```

# SVD图生视频
```json
{
  "last_node_id": 24,
  "last_link_id": 42,
  "nodes": [
    {
      "id": 17,
      "type": "KSampler",
      "pos": [
        802.4000122070315,
        566.4000274658204
      ],
      "size": {
        "0": 315,
        "1": 474
      },
      "flags": {},
      "order": 8,
      "mode": 0,
      "inputs": [
        {
          "name": "model",
          "type": "MODEL",
          "link": 28,
          "label": "model"
        },
        {
          "name": "positive",
          "type": "CONDITIONING",
          "link": 30,
          "label": "positive"
        },
        {
          "name": "negative",
          "type": "CONDITIONING",
          "link": 32,
          "label": "negative"
        },
        {
          "name": "latent_image",
          "type": "LATENT",
          "link": 37,
          "slot_index": 3,
          "label": "latent_image"
        }
      ],
      "outputs": [
        {
          "name": "LATENT",
          "type": "LATENT",
          "links": [
            33
          ],
          "shape": 3,
          "slot_index": 0,
          "label": "LATENT"
        }
      ],
      "properties": {
        "Node name for S&R": "KSampler"
      },
      "widgets_values": [
        870215885552051,
        "randomize",
        15,
        8,
        "uni_pc_bh2",
        "normal",
        1
      ]
    },
    {
      "id": 22,
      "type": "EmptyLatentImage",
      "pos": [
        422.4000122070312,
        866.4000274658204
      ],
      "size": {
        "0": 310,
        "1": 110
      },
      "flags": {},
      "order": 0,
      "mode": 0,
      "outputs": [
        {
          "name": "LATENT",
          "type": "LATENT",
          "links": [
            37
          ],
          "shape": 3,
          "label": "LATENT"
        }
      ],
      "properties": {
        "Node name for S&R": "EmptyLatentImage"
      },
      "widgets_values": [
        1024,
        576,
        1
      ]
    },
    {
      "id": 8,
      "type": "VAEDecode",
      "pos": [
        2635.0480407592772,
        634
      ],
      "size": {
        "0": 210,
        "1": 46
      },
      "flags": {},
      "order": 13,
      "mode": 0,
      "inputs": [
        {
          "name": "samples",
          "type": "LATENT",
          "link": 7,
          "label": "samples"
        },
        {
          "name": "vae",
          "type": "VAE",
          "link": 26,
          "label": "vae"
        }
      ],
      "outputs": [
        {
          "name": "IMAGE",
          "type": "IMAGE",
          "links": [
            10
          ],
          "slot_index": 0,
          "label": "IMAGE"
        }
      ],
      "properties": {
        "Node name for S&R": "VAEDecode"
      }
    },
    {
      "id": 14,
      "type": "VideoLinearCFGGuidance",
      "pos": [
        1896.0480407592775,
        578
      ],
      "size": {
        "0": 315,
        "1": 58
      },
      "flags": {},
      "order": 5,
      "mode": 0,
      "inputs": [
        {
          "name": "model",
          "type": "MODEL",
          "link": 23,
          "label": "model"
        }
      ],
      "outputs": [
        {
          "name": "MODEL",
          "type": "MODEL",
          "links": [
            39
          ],
          "shape": 3,
          "slot_index": 0,
          "label": "MODEL"
        }
      ],
      "properties": {
        "Node name for S&R": "VideoLinearCFGGuidance"
      },
      "widgets_values": [
        1
      ]
    },
    {
      "id": 20,
      "type": "VAEDecode",
      "pos": [
        1179,
        581
      ],
      "size": {
        "0": 210,
        "1": 46
      },
      "flags": {},
      "order": 9,
      "mode": 0,
      "inputs": [
        {
          "name": "samples",
          "type": "LATENT",
          "link": 33,
          "label": "samples"
        },
        {
          "name": "vae",
          "type": "VAE",
          "link": 34,
          "slot_index": 1,
          "label": "vae"
        }
      ],
      "outputs": [
        {
          "name": "IMAGE",
          "type": "IMAGE",
          "links": [
            36,
            42
          ],
          "shape": 3,
          "slot_index": 0,
          "label": "IMAGE"
        }
      ],
      "properties": {
        "Node name for S&R": "VAEDecode"
      }
    },
    {
      "id": 18,
      "type": "CLIPTextEncode",
      "pos": [
        342.4000122070312,
        516.4000274658204
      ],
      "size": {
        "0": 390,
        "1": 130
      },
      "flags": {},
      "order": 6,
      "mode": 0,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 29,
          "label": "clip"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            30
          ],
          "shape": 3,
          "slot_index": 0,
          "label": "CONDITIONING"
        }
      ],
      "properties": {
        "Node name for S&R": "CLIPTextEncode"
      },
      "widgets_values": [
        "photograph beautiful scenery nature mountains alps river rapids snow sky cumulus clouds"
      ]
    },
    {
      "id": 3,
      "type": "KSampler",
      "pos": [
        2268.0480407592772,
        629
      ],
      "size": {
        "0": 294.6124267578125,
        "1": 474
      },
      "flags": {},
      "order": 12,
      "mode": 0,
      "inputs": [
        {
          "name": "model",
          "type": "MODEL",
          "link": 39,
          "label": "model"
        },
        {
          "name": "positive",
          "type": "CONDITIONING",
          "link": 40,
          "label": "positive"
        },
        {
          "name": "negative",
          "type": "CONDITIONING",
          "link": 17,
          "label": "negative"
        },
        {
          "name": "latent_image",
          "type": "LATENT",
          "link": 18,
          "label": "latent_image"
        }
      ],
      "outputs": [
        {
          "name": "LATENT",
          "type": "LATENT",
          "links": [
            7
          ],
          "slot_index": 0,
          "label": "LATENT"
        }
      ],
      "properties": {
        "Node name for S&R": "KSampler"
      },
      "widgets_values": [
        1064761774727342,
        "randomize",
        20,
        2.5,
        "euler",
        "karras",
        1
      ]
    },
    {
      "id": 15,
      "type": "ImageOnlyCheckpointLoader",
      "pos": [
        1495,
        397
      ],
      "size": {
        "0": 369.6000061035156,
        "1": 98
      },
      "flags": {},
      "order": 1,
      "mode": 0,
      "outputs": [
        {
          "name": "MODEL",
          "type": "MODEL",
          "links": [
            23
          ],
          "shape": 3,
          "slot_index": 0,
          "label": "MODEL"
        },
        {
          "name": "CLIP_VISION",
          "type": "CLIP_VISION",
          "links": [
            24
          ],
          "shape": 3,
          "slot_index": 1,
          "label": "CLIP_VISION"
        },
        {
          "name": "VAE",
          "type": "VAE",
          "links": [
            25,
            26
          ],
          "shape": 3,
          "slot_index": 2,
          "label": "VAE"
        }
      ],
      "properties": {
        "Node name for S&R": "ImageOnlyCheckpointLoader"
      },
      "widgets_values": [
        "svd_xt.safetensors"
      ]
    },
    {
      "id": 21,
      "type": "PreviewImage",
      "pos": [
        1155,
        727
      ],
      "size": {
        "0": 275.9453125,
        "1": 246
      },
      "flags": {},
      "order": 10,
      "mode": 0,
      "inputs": [
        {
          "name": "images",
          "type": "IMAGE",
          "link": 36,
          "label": "images"
        }
      ],
      "properties": {
        "Node name for S&R": "PreviewImage"
      }
    },
    {
      "id": 23,
      "type": "LoadImage",
      "pos": [
        1045,
        1119
      ],
      "size": {
        "0": 315,
        "1": 314
      },
      "flags": {},
      "order": 2,
      "mode": 0,
      "outputs": [
        {
          "name": "IMAGE",
          "type": "IMAGE",
          "links": [],
          "shape": 3,
          "label": "IMAGE",
          "slot_index": 0
        },
        {
          "name": "MASK",
          "type": "MASK",
          "links": null,
          "shape": 3,
          "label": "MASK"
        }
      ],
      "properties": {
        "Node name for S&R": "LoadImage"
      },
      "widgets_values": [
        "ComfyUI_00140_.png",
        "image"
      ]
    },
    {
      "id": 16,
      "type": "CheckpointLoaderSimple",
      "pos": [
        -87,
        510
      ],
      "size": {
        "0": 315,
        "1": 98
      },
      "flags": {},
      "order": 3,
      "mode": 0,
      "outputs": [
        {
          "name": "MODEL",
          "type": "MODEL",
          "links": [
            28
          ],
          "shape": 3,
          "slot_index": 0,
          "label": "MODEL"
        },
        {
          "name": "CLIP",
          "type": "CLIP",
          "links": [
            29,
            31
          ],
          "shape": 3,
          "slot_index": 1,
          "label": "CLIP"
        },
        {
          "name": "VAE",
          "type": "VAE",
          "links": [
            34
          ],
          "shape": 3,
          "label": "VAE"
        }
      ],
      "properties": {
        "Node name for S&R": "CheckpointLoaderSimple"
      },
      "widgets_values": [
        "dreamshaper_7.safetensors"
      ]
    },
    {
      "id": 12,
      "type": "SVD_img2vid_Conditioning",
      "pos": [
        1906.0480407592775,
        689
      ],
      "size": {
        "0": 315,
        "1": 218
      },
      "flags": {},
      "order": 11,
      "mode": 0,
      "inputs": [
        {
          "name": "clip_vision",
          "type": "CLIP_VISION",
          "link": 24,
          "label": "clip_vision"
        },
        {
          "name": "init_image",
          "type": "IMAGE",
          "link": 42,
          "slot_index": 1,
          "label": "init_image"
        },
        {
          "name": "vae",
          "type": "VAE",
          "link": 25,
          "label": "vae"
        }
      ],
      "outputs": [
        {
          "name": "positive",
          "type": "CONDITIONING",
          "links": [
            40
          ],
          "shape": 3,
          "slot_index": 0,
          "label": "positive"
        },
        {
          "name": "negative",
          "type": "CONDITIONING",
          "links": [
            17
          ],
          "shape": 3,
          "slot_index": 1,
          "label": "negative"
        },
        {
          "name": "latent",
          "type": "LATENT",
          "links": [
            18
          ],
          "shape": 3,
          "slot_index": 2,
          "label": "latent"
        }
      ],
      "properties": {
        "Node name for S&R": "SVD_img2vid_Conditioning"
      },
      "widgets_values": [
        1024,
        576,
        25,
        87,
        6,
        0.05
      ]
    },
    {
      "id": 24,
      "type": "Note",
      "pos": [
        1896,
        929
      ],
      "size": {
        "0": 356.2646484375,
        "1": 103.78158569335938
      },
      "flags": {},
      "order": 4,
      "mode": 0,
      "properties": {
        "text": ""
      },
      "widgets_values": [
        "width:生成视频的宽度\nheight:生成视频的高度\nvideo_frames:生成的运动总帧数(建议最大25)\nMotion_bucket_id:数值越大运动幅度越大(建议100以内,不超过200)\nFPS:视频的每秒帧数(6或8)\nAugmentation_level:添加到图像的噪声量(0.1以内,不超过0.5)"
      ],
      "color": "#432",
      "bgcolor": "#653"
    },
    {
      "id": 19,
      "type": "CLIPTextEncode",
      "pos": [
        342,
        691
      ],
      "size": {
        "0": 390,
        "1": 130
      },
      "flags": {},
      "order": 7,
      "mode": 0,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 31,
          "label": "clip"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            32
          ],
          "shape": 3,
          "slot_index": 0,
          "label": "CONDITIONING"
        }
      ],
      "properties": {
        "Node name for S&R": "CLIPTextEncode"
      },
      "widgets_values": [
        "text, watermark"
      ]
    },
    {
      "id": 10,
      "type": "SaveAnimatedWEBP",
      "pos": [
        2907,
        405
      ],
      "size": {
        "0": 708.6719970703125,
        "1": 843.7864379882812
      },
      "flags": {},
      "order": 14,
      "mode": 0,
      "inputs": [
        {
          "name": "images",
          "type": "IMAGE",
          "link": 10,
          "label": "images"
        }
      ],
      "properties": {
        "Node name for S&R": "SaveAnimatedWEBP"
      },
      "widgets_values": [
        "ComfyUI",
        10,
        false,
        85,
        "default",
        null
      ]
    }
  ],
  "links": [
    [
      7,
      3,
      0,
      8,
      0,
      "LATENT"
    ],
    [
      10,
      8,
      0,
      10,
      0,
      "IMAGE"
    ],
    [
      17,
      12,
      1,
      3,
      2,
      "CONDITIONING"
    ],
    [
      18,
      12,
      2,
      3,
      3,
      "LATENT"
    ],
    [
      23,
      15,
      0,
      14,
      0,
      "MODEL"
    ],
    [
      24,
      15,
      1,
      12,
      0,
      "CLIP_VISION"
    ],
    [
      25,
      15,
      2,
      12,
      2,
      "VAE"
    ],
    [
      26,
      15,
      2,
      8,
      1,
      "VAE"
    ],
    [
      28,
      16,
      0,
      17,
      0,
      "MODEL"
    ],
    [
      29,
      16,
      1,
      18,
      0,
      "CLIP"
    ],
    [
      30,
      18,
      0,
      17,
      1,
      "CONDITIONING"
    ],
    [
      31,
      16,
      1,
      19,
      0,
      "CLIP"
    ],
    [
      32,
      19,
      0,
      17,
      2,
      "CONDITIONING"
    ],
    [
      33,
      17,
      0,
      20,
      0,
      "LATENT"
    ],
    [
      34,
      16,
      2,
      20,
      1,
      "VAE"
    ],
    [
      36,
      20,
      0,
      21,
      0,
      "IMAGE"
    ],
    [
      37,
      22,
      0,
      17,
      3,
      "LATENT"
    ],
    [
      39,
      14,
      0,
      3,
      0,
      "MODEL"
    ],
    [
      40,
      12,
      0,
      3,
      1,
      "CONDITIONING"
    ],
    [
      42,
      20,
      0,
      12,
      1,
      "IMAGE"
    ]
  ],
  "groups": [
    {
      "title": "SVD",
      "bounding": [
        1453,
        297,
        2203,
        1015
      ],
      "color": "#8A8",
      "font_size": 24
    },
    {
      "title": "txt2img",
      "bounding": [
        332,
        442,
        1106,
        635
      ],
      "color": "#3f789e",
      "font_size": 24
    }
  ],
  "config": {},
  "extra": {},
  "version": 0.4
}
```
# 分区域写提示词
```json
{
  "last_node_id": 190,
  "last_link_id": 178,
  "nodes": [
    {
      "id": 180,
      "type": "ConditioningSetArea",
      "pos": [
        956,
        3076
      ],
      "size": {
        "0": 317.4000244140625,
        "1": 154
      },
      "flags": {},
      "order": 13,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning",
          "type": "CONDITIONING",
          "link": 153,
          "label": "conditioning",
          "slot_index": 0
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            162
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "二张视图的整体区域",
      "properties": {
        "Node name for S&R": "ConditioningSetArea"
      },
      "widgets_values": [
        2048,
        1536,
        0,
        0,
        1
      ]
    },
    {
      "id": 124,
      "type": "ConditioningSetArea",
      "pos": [
        955,
        3285
      ],
      "size": {
        "0": 317.4000244140625,
        "1": 154
      },
      "flags": {},
      "order": 12,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning",
          "type": "CONDITIONING",
          "link": 36,
          "label": "conditioning"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            165
          ],
          "shape": 3,
          "label": "CONDITIONING"
        }
      ],
      "title": "三张视图的整体区域",
      "properties": {
        "Node name for S&R": "ConditioningSetArea"
      },
      "widgets_values": [
        3072,
        1536,
        0,
        0,
        1
      ]
    },
    {
      "id": 118,
      "type": "ConditioningSetArea",
      "pos": [
        943,
        2383
      ],
      "size": {
        "0": 317.4000244140625,
        "1": 154
      },
      "flags": {},
      "order": 10,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning",
          "type": "CONDITIONING",
          "link": 30,
          "label": "conditioning"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            29
          ],
          "shape": 3,
          "label": "CONDITIONING"
        }
      ],
      "title": "控制第二张视图的区域",
      "properties": {
        "Node name for S&R": "ConditioningSetArea"
      },
      "widgets_values": [
        1024,
        1536,
        1024,
        0,
        0.8
      ]
    },
    {
      "id": 116,
      "type": "ConditioningSetArea",
      "pos": [
        943,
        2091
      ],
      "size": {
        "0": 317.4000244140625,
        "1": 154
      },
      "flags": {},
      "order": 9,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning",
          "type": "CONDITIONING",
          "link": 27,
          "label": "conditioning"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            28,
            171
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "控制第一张视图的区域",
      "properties": {
        "Node name for S&R": "ConditioningSetArea"
      },
      "widgets_values": [
        1024,
        1536,
        0,
        0,
        0.8
      ]
    },
    {
      "id": 173,
      "type": "Logic Boolean",
      "pos": [
        -142,
        2673
      ],
      "size": {
        "0": 315,
        "1": 78
      },
      "flags": {},
      "order": 0,
      "mode": 0,
      "outputs": [
        {
          "name": "NUMBER",
          "type": "NUMBER",
          "links": [
            174,
            176
          ],
          "shape": 3,
          "label": "NUMBER",
          "slot_index": 0
        },
        {
          "name": "INT",
          "type": "INT",
          "links": null,
          "shape": 3,
          "label": "INT"
        }
      ],
      "title": "是否是三张视图",
      "properties": {
        "Node name for S&R": "Logic Boolean"
      },
      "widgets_values": [
        1
      ]
    },
    {
      "id": 120,
      "type": "ConditioningSetArea",
      "pos": [
        953,
        2605
      ],
      "size": {
        "0": 317.4000244140625,
        "1": 154
      },
      "flags": {},
      "order": 11,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning",
          "type": "CONDITIONING",
          "link": 33,
          "label": "conditioning"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            32
          ],
          "shape": 3,
          "label": "CONDITIONING"
        }
      ],
      "title": "控制第三张视图的区域",
      "properties": {
        "Node name for S&R": "ConditioningSetArea"
      },
      "widgets_values": [
        1024,
        1536,
        2048,
        0,
        0.8
      ]
    },
    {
      "id": 183,
      "type": "ConditioningSetArea",
      "pos": [
        960,
        2873
      ],
      "size": {
        "0": 317.4000244140625,
        "1": 154
      },
      "flags": {},
      "order": 14,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning",
          "type": "CONDITIONING",
          "link": 160,
          "label": "conditioning",
          "slot_index": 0
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            161
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "一张视图的整体区域",
      "properties": {
        "Node name for S&R": "ConditioningSetArea"
      },
      "widgets_values": [
        1024,
        1536,
        0,
        0,
        1
      ]
    },
    {
      "id": 117,
      "type": "ConditioningCombine",
      "pos": [
        1358,
        2096
      ],
      "size": {
        "0": 342.5999755859375,
        "1": 46
      },
      "flags": {
        "collapsed": false
      },
      "order": 15,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning_1",
          "type": "CONDITIONING",
          "link": 28,
          "label": "conditioning_1"
        },
        {
          "name": "conditioning_2",
          "type": "CONDITIONING",
          "link": 29,
          "label": "conditioning_2"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            172
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "结合第一张视图与第二张视图",
      "properties": {
        "Node name for S&R": "ConditioningCombine"
      }
    },
    {
      "id": 187,
      "type": "Conditioning Input Switch",
      "pos": [
        1409,
        2207
      ],
      "size": {
        "0": 342.5999755859375,
        "1": 66
      },
      "flags": {},
      "order": 17,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning_a",
          "type": "CONDITIONING",
          "link": 172,
          "label": "conditioning_a",
          "slot_index": 0
        },
        {
          "name": "conditioning_b",
          "type": "CONDITIONING",
          "link": 171,
          "label": "conditioning_b",
          "slot_index": 1
        },
        {
          "name": "boolean_number",
          "type": "NUMBER",
          "link": 173,
          "label": "boolean_number",
          "slot_index": 2
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            170,
            175
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "Conditioning Input Switch"
      }
    },
    {
      "id": 119,
      "type": "ConditioningCombine",
      "pos": [
        1788,
        2221
      ],
      "size": {
        "0": 342.5999755859375,
        "1": 46
      },
      "flags": {},
      "order": 19,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning_1",
          "type": "CONDITIONING",
          "link": 170,
          "label": "conditioning_1"
        },
        {
          "name": "conditioning_2",
          "type": "CONDITIONING",
          "link": 32,
          "label": "conditioning_2"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            168
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "结合第二张视图与第三张视图",
      "properties": {
        "Node name for S&R": "ConditioningCombine"
      }
    },
    {
      "id": 186,
      "type": "Conditioning Input Switch",
      "pos": [
        1988,
        2316
      ],
      "size": {
        "0": 342.5999755859375,
        "1": 66
      },
      "flags": {},
      "order": 20,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning_a",
          "type": "CONDITIONING",
          "link": 168,
          "label": "conditioning_a",
          "slot_index": 0
        },
        {
          "name": "conditioning_b",
          "type": "CONDITIONING",
          "link": 175,
          "label": "conditioning_b",
          "slot_index": 1
        },
        {
          "name": "boolean_number",
          "type": "NUMBER",
          "link": 174,
          "label": "boolean_number",
          "slot_index": 2
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            169
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "Conditioning Input Switch"
      }
    },
    {
      "id": 122,
      "type": "ConditioningCombine",
      "pos": [
        2367,
        2318
      ],
      "size": {
        "0": 342.5999755859375,
        "1": 46
      },
      "flags": {},
      "order": 21,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning_1",
          "type": "CONDITIONING",
          "link": 169,
          "label": "conditioning_1"
        },
        {
          "name": "conditioning_2",
          "type": "CONDITIONING",
          "link": 166,
          "label": "conditioning_2"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            156
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "结合控制整体区域",
      "properties": {
        "Node name for S&R": "ConditioningCombine"
      }
    },
    {
      "id": 125,
      "type": "ConditioningCombine",
      "pos": [
        2734,
        2402
      ],
      "size": {
        "0": 342.5999755859375,
        "1": 46
      },
      "flags": {},
      "order": 22,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning_1",
          "type": "CONDITIONING",
          "link": 156,
          "label": "conditioning_1"
        },
        {
          "name": "conditioning_2",
          "type": "CONDITIONING",
          "link": 38,
          "label": "conditioning_2"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "结合控制整体",
      "properties": {
        "Node name for S&R": "ConditioningCombine"
      }
    },
    {
      "id": 142,
      "type": "CLIPSetLastLayer",
      "pos": [
        9,
        2275
      ],
      "size": {
        "0": 315,
        "1": 58
      },
      "flags": {},
      "order": 1,
      "mode": 0,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": null,
          "label": "clip",
          "slot_index": 0
        }
      ],
      "outputs": [
        {
          "name": "CLIP",
          "type": "CLIP",
          "links": [
            66,
            67,
            68,
            69,
            70,
            71
          ],
          "shape": 3,
          "label": "CLIP",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "CLIPSetLastLayer"
      },
      "widgets_values": [
        -2
      ]
    },
    {
      "id": 133,
      "type": "BNK_CLIPTextEncodeAdvanced",
      "pos": [
        488,
        2093
      ],
      "size": {
        "0": 400,
        "1": 200
      },
      "flags": {},
      "order": 4,
      "mode": 0,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 67,
          "label": "clip"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            27
          ],
          "shape": 3,
          "label": "CONDITIONING"
        }
      ],
      "title": "第一张视图的提示词",
      "properties": {
        "Node name for S&R": "BNK_CLIPTextEncodeAdvanced"
      },
      "widgets_values": [
        "",
        "none",
        "A1111"
      ]
    },
    {
      "id": 134,
      "type": "BNK_CLIPTextEncodeAdvanced",
      "pos": [
        488,
        2383
      ],
      "size": {
        "0": 400,
        "1": 200
      },
      "flags": {},
      "order": 5,
      "mode": 0,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 68,
          "label": "clip"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            30
          ],
          "shape": 3,
          "label": "CONDITIONING"
        }
      ],
      "title": "第二张视图的提示词",
      "properties": {
        "Node name for S&R": "BNK_CLIPTextEncodeAdvanced"
      },
      "widgets_values": [
        "",
        "none",
        "A1111"
      ]
    },
    {
      "id": 135,
      "type": "BNK_CLIPTextEncodeAdvanced",
      "pos": [
        479,
        2640
      ],
      "size": {
        "0": 400,
        "1": 200
      },
      "flags": {},
      "order": 6,
      "mode": 0,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 69,
          "label": "clip"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            33
          ],
          "shape": 3,
          "label": "CONDITIONING"
        }
      ],
      "title": "第三张视图的提示词",
      "properties": {
        "Node name for S&R": "BNK_CLIPTextEncodeAdvanced"
      },
      "widgets_values": [
        "",
        "none",
        "A1111"
      ]
    },
    {
      "id": 136,
      "type": "BNK_CLIPTextEncodeAdvanced",
      "pos": [
        474,
        2916
      ],
      "size": {
        "0": 400,
        "1": 200
      },
      "flags": {},
      "order": 7,
      "mode": 0,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 70,
          "label": "clip"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            36,
            153,
            160
          ],
          "shape": 3,
          "label": "CONDITIONING"
        }
      ],
      "title": "控制整体区域的提示词",
      "properties": {
        "Node name for S&R": "BNK_CLIPTextEncodeAdvanced"
      },
      "widgets_values": [
        "",
        "none",
        "A1111"
      ]
    },
    {
      "id": 137,
      "type": "CLIPTextEncode",
      "pos": [
        471,
        3233
      ],
      "size": {
        "0": 400,
        "1": 200
      },
      "flags": {},
      "order": 8,
      "mode": 0,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 71,
          "label": "clip"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            38
          ],
          "shape": 3,
          "label": "CONDITIONING"
        }
      ],
      "title": "使整张图统一,可以不填提示词",
      "properties": {
        "Node name for S&R": "CLIPTextEncode"
      },
      "widgets_values": [
        ""
      ]
    },
    {
      "id": 184,
      "type": "Conditioning Input Switch",
      "pos": [
        1337,
        2941
      ],
      "size": {
        "0": 342.5999755859375,
        "1": 66
      },
      "flags": {},
      "order": 16,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning_a",
          "type": "CONDITIONING",
          "link": 162,
          "label": "conditioning_a",
          "slot_index": 0
        },
        {
          "name": "conditioning_b",
          "type": "CONDITIONING",
          "link": 161,
          "label": "conditioning_b"
        },
        {
          "name": "boolean_number",
          "type": "NUMBER",
          "link": 163,
          "label": "boolean_number",
          "slot_index": 2
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            164
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "Conditioning Input Switch"
      }
    },
    {
      "id": 185,
      "type": "Conditioning Input Switch",
      "pos": [
        1756,
        2957
      ],
      "size": {
        "0": 342.5999755859375,
        "1": 66
      },
      "flags": {},
      "order": 18,
      "mode": 0,
      "inputs": [
        {
          "name": "conditioning_a",
          "type": "CONDITIONING",
          "link": 165,
          "label": "conditioning_a",
          "slot_index": 0
        },
        {
          "name": "conditioning_b",
          "type": "CONDITIONING",
          "link": 164,
          "label": "conditioning_b"
        },
        {
          "name": "boolean_number",
          "type": "NUMBER",
          "link": 176,
          "label": "boolean_number",
          "slot_index": 2
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [
            166
          ],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "properties": {
        "Node name for S&R": "Conditioning Input Switch"
      }
    },
    {
      "id": 176,
      "type": "Logic Boolean",
      "pos": [
        -148,
        2509
      ],
      "size": {
        "0": 315,
        "1": 78
      },
      "flags": {
        "collapsed": false
      },
      "order": 2,
      "mode": 0,
      "outputs": [
        {
          "name": "NUMBER",
          "type": "NUMBER",
          "links": [
            163,
            173
          ],
          "shape": 3,
          "label": "NUMBER",
          "slot_index": 0
        },
        {
          "name": "INT",
          "type": "INT",
          "links": null,
          "shape": 3,
          "label": "INT"
        }
      ],
      "title": "是否是两张视图",
      "properties": {
        "Node name for S&R": "Logic Boolean"
      },
      "widgets_values": [
        0
      ]
    },
    {
      "id": 140,
      "type": "BNK_CLIPTextEncodeAdvanced",
      "pos": [
        487,
        1832
      ],
      "size": {
        "0": 400,
        "1": 200
      },
      "flags": {},
      "order": 3,
      "mode": 0,
      "inputs": [
        {
          "name": "clip",
          "type": "CLIP",
          "link": 66,
          "label": "clip"
        }
      ],
      "outputs": [
        {
          "name": "CONDITIONING",
          "type": "CONDITIONING",
          "links": [],
          "shape": 3,
          "label": "CONDITIONING",
          "slot_index": 0
        }
      ],
      "title": "反向提示词",
      "properties": {
        "Node name for S&R": "BNK_CLIPTextEncodeAdvanced"
      },
      "widgets_values": [
        "",
        "none",
        "comfy"
      ]
    }
  ],
  "links": [
    [
      27,
      133,
      0,
      116,
      0,
      "CONDITIONING"
    ],
    [
      28,
      116,
      0,
      117,
      0,
      "CONDITIONING"
    ],
    [
      29,
      118,
      0,
      117,
      1,
      "CONDITIONING"
    ],
    [
      30,
      134,
      0,
      118,
      0,
      "CONDITIONING"
    ],
    [
      32,
      120,
      0,
      119,
      1,
      "CONDITIONING"
    ],
    [
      33,
      135,
      0,
      120,
      0,
      "CONDITIONING"
    ],
    [
      36,
      136,
      0,
      124,
      0,
      "CONDITIONING"
    ],
    [
      38,
      137,
      0,
      125,
      1,
      "CONDITIONING"
    ],
    [
      66,
      142,
      0,
      140,
      0,
      "CLIP"
    ],
    [
      67,
      142,
      0,
      133,
      0,
      "CLIP"
    ],
    [
      68,
      142,
      0,
      134,
      0,
      "CLIP"
    ],
    [
      69,
      142,
      0,
      135,
      0,
      "CLIP"
    ],
    [
      70,
      142,
      0,
      136,
      0,
      "CLIP"
    ],
    [
      71,
      142,
      0,
      137,
      0,
      "CLIP"
    ],
    [
      153,
      136,
      0,
      180,
      0,
      "CONDITIONING"
    ],
    [
      156,
      122,
      0,
      125,
      0,
      "CONDITIONING"
    ],
    [
      160,
      136,
      0,
      183,
      0,
      "CONDITIONING"
    ],
    [
      161,
      183,
      0,
      184,
      1,
      "CONDITIONING"
    ],
    [
      162,
      180,
      0,
      184,
      0,
      "CONDITIONING"
    ],
    [
      163,
      176,
      0,
      184,
      2,
      "NUMBER"
    ],
    [
      164,
      184,
      0,
      185,
      1,
      "CONDITIONING"
    ],
    [
      165,
      124,
      0,
      185,
      0,
      "CONDITIONING"
    ],
    [
      166,
      185,
      0,
      122,
      1,
      "CONDITIONING"
    ],
    [
      168,
      119,
      0,
      186,
      0,
      "CONDITIONING"
    ],
    [
      169,
      186,
      0,
      122,
      0,
      "CONDITIONING"
    ],
    [
      170,
      187,
      0,
      119,
      0,
      "CONDITIONING"
    ],
    [
      171,
      116,
      0,
      187,
      1,
      "CONDITIONING"
    ],
    [
      172,
      117,
      0,
      187,
      0,
      "CONDITIONING"
    ],
    [
      173,
      176,
      0,
      187,
      2,
      "NUMBER"
    ],
    [
      174,
      173,
      0,
      186,
      2,
      "NUMBER"
    ],
    [
      175,
      187,
      0,
      186,
      1,
      "CONDITIONING"
    ],
    [
      176,
      173,
      0,
      185,
      2,
      "NUMBER"
    ]
  ],
  "groups": [],
  "config": {},
  "extra": {},
  "version": 0.4
}
```
