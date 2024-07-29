---
title: Command的使用
tags: Command
categories: Geek
abbrlink: 3b4a10c4
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

视频地址：[https://www.bilibili.com/video/BV1zz411b7tk/?spm_id_from=333.788&vd_source=b1de3fe38e887eb40fc55a5485724480](https://www.bilibili.com/video/BV1zz411b7tk/?spm_id_from=333.788&vd_source=b1de3fe38e887eb40fc55a5485724480)<br />ppt：[commadn.pptx](https://www.yuque.com/attachments/yuque/0/2022/pptx/2623605/1668496289369-5d1784db-b184-40e0-a5a9-3663ece40931.pptx?_lake_card=%7B%22src%22%3A%22https%3A%2F%2Fwww.yuque.com%2Fattachments%2Fyuque%2F0%2F2022%2Fpptx%2F2623605%2F1668496289369-5d1784db-b184-40e0-a5a9-3663ece40931.pptx%22%2C%22name%22%3A%22commadn.pptx%22%2C%22size%22%3A371572%2C%22type%22%3A%22application%2Fvnd.openxmlformats-officedocument.presentationml.presentation%22%2C%22ext%22%3A%22pptx%22%2C%22source%22%3A%22%22%2C%22status%22%3A%22done%22%2C%22mode%22%3A%22title%22%2C%22download%22%3Atrue%2C%22taskId%22%3A%22uf9b6b58e-5d9a-4ba0-8743-e3e1d8200d5%22%2C%22taskType%22%3A%22upload%22%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22uc3be219a%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22file%22%7D)
<a name="dQrPr"></a>
# 说明
如果这里有些命令不清楚的就用help 或者 /? 来获取命令的帮助
<a name="kGmTA"></a>
# Python or CMD
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668496330700-afff5ad0-6df2-4f8f-a32c-726db3df45e8.png#averageHue=%23222222&clientId=ua2bf7b75-6c38-4&from=paste&height=490&id=uc3feca9a&originHeight=441&originWidth=722&originalType=binary&ratio=1&rotation=0&showTitle=false&size=130187&status=done&style=none&taskId=uc1a9250b-127d-4bda-8bb2-4ea49ad5330&title=&width=802.2222434738542)
<a name="EhSub"></a>
# 常用的cmd命令
<a name="MP4hR"></a>
## 要背诵的
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668496625128-87c2cfdc-9da5-458f-8134-a4e1dd13a3d6.png#averageHue=%23171717&clientId=ua2bf7b75-6c38-4&from=paste&height=1091&id=u3bdff79c&originHeight=982&originWidth=1435&originalType=binary&ratio=1&rotation=0&showTitle=false&size=244830&status=done&style=none&taskId=ub9ad18df-263a-4da5-b0ce-ba65b6bcea3&title=&width=1594.4444866827987)<br />echo %variable% 是回显这个变量的值
<a name="vAZjw"></a>
## 特殊符号
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668497685179-48577e14-5d64-4061-9938-240d58dd5635.png#averageHue=%23181818&clientId=ua2bf7b75-6c38-4&from=paste&height=1212&id=u27b4ff35&originHeight=1091&originWidth=1606&originalType=binary&ratio=1&rotation=0&showTitle=false&size=370891&status=done&style=none&taskId=u89d571b8-d744-4cd7-9128-fd09920930f&title=&width=1784.44449171608)
<a name="qpcJJ"></a>
### 管道符号  |
这里意思是将通过tasklist得到的任务列表再进行findstr操作，因此管道符号的就是针对一个命令的输出结果进行操作时能用到的。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668570785309-643f29e7-e84f-4920-a320-7673c369e951.png#averageHue=%23131313&clientId=u4d39f4d7-ddba-4&from=paste&height=97&id=udbfcf8ce&originHeight=87&originWidth=793&originalType=binary&ratio=1&rotation=0&showTitle=false&size=28842&status=done&style=none&taskId=u48f9aee5-cd0c-4c06-bfac-887c6ee3c08&title=&width=881.111134452585)
<a name="joWUH"></a>
## >重定向覆盖与>>重定向追加
覆盖与追加区别就是将文本信息一个是覆盖原来的信息，一个是在原来信息的基础上添加新的信息。<br />将命令输出的信息输出到一个文件上。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668503949930-58e9e259-14ca-49c5-93db-b2b1445ad314.png#averageHue=%231a1a1a&clientId=ua2bf7b75-6c38-4&from=paste&height=32&id=u9a968091&originHeight=29&originWidth=446&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1052&status=done&style=none&taskId=u7e79d22e-2479-4dc0-b01c-c9bba692cc0&title=&width=495.55556868329495)<br />D:\ZhangRuiChen\pythonProject>dir /s /b *.py >D:\py.txt
<a name="Eqx64"></a>
## 文件目录
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668500756541-343eabd6-d9bc-40b1-b3e3-796bbf41b0c5.png#averageHue=%23171717&clientId=ua2bf7b75-6c38-4&from=paste&height=887&id=u54dcd2d0&originHeight=798&originWidth=1598&originalType=binary&ratio=1&rotation=0&showTitle=false&size=236794&status=done&style=none&taskId=u7c648c65-670c-4994-a7cb-e22e785c971&title=&width=1775.555602591716)
<a name="dp1KR"></a>
### cd的使用介绍：
当需要切换盘符时需要加 /d 命令<br />更改当前目录为D盘是第一行行，从D盘进入WallPaper是第二行<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668501427188-ce095ff3-a140-40a3-a141-5b4620e361cf.png#averageHue=%23141414&clientId=ua2bf7b75-6c38-4&from=paste&height=143&id=u5d5fa4bb&originHeight=129&originWidth=306&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2360&status=done&style=none&taskId=u6393e0b2-9a25-4a3b-8140-7c623973dff&title=&width=340)<br />.是当前目录， ..是上一级目录<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668501666103-ec79d1f5-164f-410e-b1ec-3fdf071cb5bd.png#averageHue=%23141414&clientId=ua2bf7b75-6c38-4&from=paste&height=101&id=u714696d3&originHeight=91&originWidth=161&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1140&status=done&style=none&taskId=u617738c1-11e9-4fba-bbbc-f97904b5ce9&title=&width=178.8888936278262)
<a name="RwMdd"></a>
### dir的使用介绍
直接dir 是显示当前目录下的所有目录与文件<br />dir + 目录路径 是显示目录路径下的所有目录与文件<br />dir /s + 目录路径 是显示目录路径以及目录路径的子目录下的所有目录与文件<br />dir *.mel  显示当前路径下的以mel结尾的文件（不能够配合指定目录路径，必须先前往目录路径再使用关键字匹配，但是可以配合 /s 匹配子目录的）<br />dir /b 只显示文件名
<a name="dn5yA"></a>
## 文件操作
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668506172041-afca6967-771d-455d-8c1e-103c99a8c074.png#averageHue=%231a1a1a&clientId=ua2bf7b75-6c38-4&from=paste&height=543&id=u50fc07dc&originHeight=489&originWidth=994&originalType=binary&ratio=1&rotation=0&showTitle=false&size=173700&status=done&style=none&taskId=u9963378b-d4ad-455e-a9ec-26c411fbe1c&title=&width=1104.4444737022313)
<a name="cWOaC"></a>
## 文件拷贝
三种文件拷贝的区别：如果文件比较大比较碎的建议使用Robocopy（功能最复杂，最快，支持多线程）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668506191536-a4e8f0f1-726c-4550-9fab-980f64d38469.png#averageHue=%231c1c1c&clientId=ua2bf7b75-6c38-4&from=paste&height=623&id=uc762dc91&originHeight=561&originWidth=817&originalType=binary&ratio=1&rotation=0&showTitle=false&size=165097&status=done&style=none&taskId=ue5b86c14-14c3-43fd-b66a-ccc13cb4f42&title=&width=907.7778018256771)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668506206249-a5187f92-fc02-49cb-88c9-62c6fdd0802e.png#averageHue=%231c1c1c&clientId=ua2bf7b75-6c38-4&from=paste&height=602&id=u0ce4a1b7&originHeight=542&originWidth=764&originalType=binary&ratio=1&rotation=0&showTitle=false&size=158159&status=done&style=none&taskId=u1779bcce-f052-42ba-a7dd-b599d76dc2c&title=&width=848.8889113767653)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668506217113-1db72379-782e-4449-aa8a-d7643088c551.png#averageHue=%231b1b1b&clientId=ua2bf7b75-6c38-4&from=paste&height=473&id=u25d95ef9&originHeight=426&originWidth=853&originalType=binary&ratio=1&rotation=0&showTitle=false&size=149937&status=done&style=none&taskId=uecafe28b-3a1b-40ec-ac51-bbce73fe683&title=&width=947.7778028853153)
<a name="i9nUw"></a>
## 文件查找
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668565921370-accfd197-5762-4936-9f54-6388dca9640e.png#averageHue=%231a1a1a&clientId=u4d39f4d7-ddba-4&from=paste&height=708&id=u5fc9c08b&originHeight=637&originWidth=1005&originalType=binary&ratio=1&rotation=0&showTitle=false&size=255609&status=done&style=none&taskId=uaf0fde54-9824-45f2-a6d9-3931030771f&title=&width=1116.6666962482318)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668565953638-1c21a468-eda5-4edd-bb06-42dddaf8861f.png#averageHue=%231a1a1a&clientId=u4d39f4d7-ddba-4&from=paste&height=508&id=u1bb8b57b&originHeight=457&originWidth=1020&originalType=binary&ratio=1&rotation=0&showTitle=false&size=152534&status=done&style=none&taskId=u05a8fccc-06de-43bc-a686-7378da06446&title=&width=1133.3333633564146)
<a name="E7a0N"></a>
## 文件校验
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668566875308-ec59414f-7ce7-4df4-a633-f0b08f93b5b7.png#averageHue=%23191919&clientId=u4d39f4d7-ddba-4&from=paste&height=279&id=u35c235ec&originHeight=251&originWidth=517&originalType=binary&ratio=1&rotation=0&showTitle=false&size=46657&status=done&style=none&taskId=ub3b949a0-2a02-4d68-ad49-54310865a97&title=&width=574.4444596620258)
<a name="iKQu2"></a>
## 文本查找
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668567693774-d23dbb2d-be53-4dd9-8d49-983d32de1a2e.png#averageHue=%23191919&clientId=u4d39f4d7-ddba-4&from=paste&height=480&id=u2bcef2c7&originHeight=432&originWidth=667&originalType=binary&ratio=1&rotation=0&showTitle=false&size=91224&status=done&style=none&taskId=u46cc4d34-ef49-4cd2-b3e9-3ea9ab57607&title=&width=741.1111307438514)
<a name="peOuj"></a>
## 时间
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668567986805-b22dfba9-02ac-4277-9a27-a97e6c3f02ba.png#averageHue=%231e1e1e&clientId=u4d39f4d7-ddba-4&from=paste&height=262&id=u963c34d5&originHeight=236&originWidth=408&originalType=binary&ratio=1&rotation=0&showTitle=false&size=45836&status=done&style=none&taskId=ubcb13fc1-417e-4d0a-bc0e-fe4727a7b8a&title=&width=453.3333453425658)<br />timeout 的 延时意思是倒计时，类似于python的sleep
<a name="eSw7T"></a>
## 目录映射
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668568266315-d32f7a5b-5d26-48e9-bd3e-300ba208e4bb.png#averageHue=%231d1d1d&clientId=u4d39f4d7-ddba-4&from=paste&height=457&id=uaac80e38&originHeight=411&originWidth=398&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86434&status=done&style=none&taskId=u3a7c0b1c-023b-4abf-9629-b9b261b5adb&title=&width=442.22223393711073)<br />目录映射可以理解为他们两者是相同的，只是文件路径不同，不管针对哪一个进行了处理也会同时的对另一个自动进行处理。
<a name="YR2IS"></a>
## 进程管理
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668570415739-f56d75e5-6e20-4024-9a8c-de522c5ab25b.png#averageHue=%231e1e1e&clientId=u4d39f4d7-ddba-4&from=paste&height=398&id=u04b912bb&originHeight=358&originWidth=725&originalType=binary&ratio=1&rotation=0&showTitle=false&size=107590&status=done&style=none&taskId=ud4117774-0ae8-4700-adba-db2164f9e7c&title=&width=805.5555768954906)<br />sc针对的是服务，例如arnold redshift 
<a name="PK5JP"></a>
## 网络相关
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668575064779-9b9ce2f0-0afd-4bb3-9370-5702d101764f.png#averageHue=%231e1e1e&clientId=u4d39f4d7-ddba-4&from=paste&height=456&id=ue8b7b08c&originHeight=410&originWidth=855&originalType=binary&ratio=1&rotation=0&showTitle=false&size=121971&status=done&style=none&taskId=u48781caa-631c-420f-a5f7-1b51972762f&title=&width=950.0000251664062)<br />ping ： 可以用来测试进入网站![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668571484686-3008c270-7dbe-490a-a118-fb470dfd6609.png#averageHue=%23202020&clientId=u4d39f4d7-ddba-4&from=paste&height=226&id=ub27f42c1&originHeight=203&originWidth=536&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9250&status=done&style=none&taskId=u06657149-95bb-47df-8704-e8d0bec30cf&title=&width=595.5555713323904)<br />ipconfig ： ipconfig /all 可以用来查看网络相关的所有配置<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668575393564-24b8bcc0-dd1f-40f4-ad50-5b816683d212.png#averageHue=%232e2e2e&clientId=u4d39f4d7-ddba-4&from=paste&height=72&id=ua66c6335&originHeight=65&originWidth=859&originalType=binary&ratio=1&rotation=0&showTitle=false&size=35442&status=done&style=none&taskId=u0187cc67-ae45-4ad0-b63b-54913af556e&title=&width=954.4444697285883)这个意思是网络连接另一台电脑（叫服务器吧），服务器的 ipv4为192.168.225.128  密码为nuke  账户名为winroot_ltsc。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668575645597-fdedca08-6a3a-48a4-b852-f8c18c3acdc1.png#averageHue=%23313131&clientId=u4d39f4d7-ddba-4&from=paste&height=60&id=u16d378be&originHeight=54&originWidth=659&originalType=binary&ratio=1&rotation=0&showTitle=false&size=26655&status=done&style=none&taskId=u2a168119-41ec-4f8b-a98b-b8d93c4d408&title=&width=732.2222416194874) 通过这个命令在当前电脑下创建一个B盘，连接ip为192.168.225.128 名字叫share的B盘符![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668575771508-f2aaa038-b0ec-4945-a23e-d35ec8de0aad.png#averageHue=%235b5b5a&clientId=u4d39f4d7-ddba-4&from=paste&height=106&id=u52acd4fc&originHeight=95&originWidth=345&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25126&status=done&style=none&taskId=u3dc83f7c-587f-413a-a2c6-16cddb49881&title=&width=383.33334348819903)，这样可以通过这个盘符来访问服务器上所共享的文件夹。<br />net share ：查询当前电脑所共享的所有文件夹<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668575892615-6499941c-4a57-4b8e-b715-f32609947310.png#averageHue=%232f2f2f&clientId=u4d39f4d7-ddba-4&from=paste&height=62&id=u08248bc3&originHeight=56&originWidth=279&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12439&status=done&style=none&taskId=uc68f8574-69fa-40cf-998e-a516fa6d7e1&title=&width=310.0000082121957) 意思是删除本地电脑使用的所有创建的网络共享的盘符，*可以改为指定的盘符，例如 B:
<a name="wNqhW"></a>
## 关机
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668576164212-656e4353-db1c-4737-998c-cce8b2dac262.png#averageHue=%23191919&clientId=u4d39f4d7-ddba-4&from=paste&height=511&id=u324baf21&originHeight=460&originWidth=1076&originalType=binary&ratio=1&rotation=0&showTitle=false&size=144981&status=done&style=none&taskId=u23426397-9cd1-4339-83da-81691481337&title=&width=1195.5555872269626)<br />/r 是重启  /s 是关机  /t是时间（以秒为单位） /a 是取消计划中的关机<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668576554479-6d9b4e2e-e3a3-4fcd-8e60-d3c1381e3a14.png#averageHue=%23272727&clientId=u4d39f4d7-ddba-4&from=paste&height=58&id=u2d59188d&originHeight=52&originWidth=1070&originalType=binary&ratio=1&rotation=0&showTitle=false&size=38528&status=done&style=none&taskId=u264ab18b-e4f9-41e1-9922-bf0cd36fa49&title=&width=1188.8889203836898) /c的意思是注释  这句的意思就是60秒后强制将ip为192.168.225.128的电脑关机，并显示注释为shutdown![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668576715815-4c4ef5a5-e28f-4418-b770-08e06bbb528c.png#averageHue=%230e69aa&clientId=u4d39f4d7-ddba-4&from=paste&height=160&id=uf5dc45b0&originHeight=144&originWidth=597&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27584&status=done&style=none&taskId=uc3599caf-1b2a-4d23-8240-0942211e7d9&title=&width=663.3333509056661)
<a name="kskgn"></a>
## 系统维护
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668576881549-ba2f1388-f26a-4215-9fa4-783a92471265.png#averageHue=%231b1b1b&clientId=u4d39f4d7-ddba-4&from=paste&height=680&id=u8118936b&originHeight=612&originWidth=1070&originalType=binary&ratio=1&rotation=0&showTitle=false&size=278538&status=done&style=none&taskId=uabf70961-6b36-4a93-8857-d9bdd136098&title=&width=1188.8889203836898)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668577559360-f1c691a2-5c92-4aac-bfae-bb97bf3f0118.png#averageHue=%231d1d1d&clientId=u4d39f4d7-ddba-4&from=paste&height=229&id=u805fdb4b&originHeight=206&originWidth=1864&originalType=binary&ratio=1&rotation=0&showTitle=false&size=152853&status=done&style=none&taskId=u740b34f2-513a-4b2c-8baf-ded71624acb&title=&width=2071.1111659768203)<br />wmic cpu get name  获取当前电脑cpu的名字<br />wmic memorychip 获取当前电脑内存的所有信息<br />wmic memorychip list /format 获取当前电脑内存的所有信息并且格式化显示这些信息<br />wmic memorychip get speed 获取内存的频率（speed可以更换任意一项可以查询的信息）
<a name="AFxUz"></a>
## 变量设置
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668577734694-575aad3a-708a-4fa1-b6f8-dd1baea9a50c.png#averageHue=%23171717&clientId=u4d39f4d7-ddba-4&from=paste&height=416&id=udab5572e&originHeight=374&originWidth=595&originalType=binary&ratio=1&rotation=0&showTitle=false&size=56345&status=done&style=none&taskId=u3aa75c04-a6b7-497f-8e72-3c12e09e01c&title=&width=661.1111286245751)<br />/a的作用：set /a a=1-2+5-6  最终a为-2       set a=1-2+5-6 最终a为1-2+5-6 <br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668578665609-43bd983f-a3a6-47c6-bf35-fd64e086c234.png#averageHue=%23444444&clientId=u4d39f4d7-ddba-4&from=paste&height=57&id=u06ef5606&originHeight=51&originWidth=473&originalType=binary&ratio=1&rotation=0&showTitle=false&size=16858&status=done&style=none&taskId=u4ac2c978-ff7a-449d-a9ce-f6d5e0a7f66&title=&width=525.5555694780236)  意思是将avr变量的str1替换成str2
<a name="qqILh"></a>
## 字符截取
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668579282409-ba5c1a51-1f3b-4b34-9b7d-92fa05f546fd.png#averageHue=%231a1a1a&clientId=u4d39f4d7-ddba-4&from=paste&height=566&id=u30850402&originHeight=509&originWidth=721&originalType=binary&ratio=1&rotation=0&showTitle=false&size=170890&status=done&style=none&taskId=uc14dc1bb-9249-46ce-802f-eca7aaf9c59&title=&width=801.1111323333087)
<a name="U17zZ"></a>
## batch（.bat批处理文件）的参数
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668579401768-cb7a54a4-82bd-4749-a7d9-26592f1d9996.png#averageHue=%231e1e1e&clientId=u4d39f4d7-ddba-4&from=paste&height=218&id=eier7&originHeight=196&originWidth=528&originalType=binary&ratio=1&rotation=0&showTitle=false&size=54253&status=done&style=none&taskId=u4a70ea43-89b5-4707-b294-3827752f15a&title=&width=586.6666822080263)<br />写一个.bat文件，.bat文件是批处理文件，里面是一行行的cmd命令。 可以通过set %~1-9来接受 启动bat文件时传递的参数。<br />调用.bat文件：将.bat文件拖入到cmd窗口上，然后 可以输入需要的参数，然后回车调用
<a name="JNEaX"></a>
### 字符扩充
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668592149372-7b70b739-ec59-4364-90c8-6308843c78b1.png#averageHue=%231e1e1e&clientId=u4d39f4d7-ddba-4&from=paste&height=650&id=u64524934&originHeight=585&originWidth=2176&originalType=binary&ratio=1&rotation=0&showTitle=false&size=468681&status=done&style=none&taskId=uca3bd98e-e6c8-419a-9129-77f09cb52fb&title=&width=2417.7778418270177)<br />字符扩充意思就是  例如<br />set n1=%1 意思就是输入的第一个参数赋予变量n1<br />set n1=%~1 意思是输入的第一个参数删除引号(")后再赋予变量n1<br />针对这些输入的参数也能够进行扩充，来更改输入的参数。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668592158645-e74c816b-e9d3-432b-a268-369a8f9d9678.png#averageHue=%231e1e1e&clientId=u4d39f4d7-ddba-4&from=paste&height=291&id=ua609b3a3&originHeight=262&originWidth=190&originalType=binary&ratio=1&rotation=0&showTitle=false&size=6970&status=done&style=none&taskId=u929d214c-3b3e-43a2-bbfe-af9e6e9d76e&title=&width=211.11111670364582)
<a name="OWjhZ"></a>
## 流程控制
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668652771934-1916702c-3162-4108-9235-ff5606f940e1.png#averageHue=%231a1817&clientId=uad50874a-6552-4&from=paste&height=244&id=ua45569be&originHeight=220&originWidth=464&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14208&status=done&style=none&taskId=u5fbf6804-ab5a-47ef-89ee-82cb1e0230b&title=&width=515.555569213114)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668651841033-8d9d05bd-7bf1-40e3-90a0-1a52d39790bc.png#averageHue=%23171717&clientId=uad50874a-6552-4&from=paste&height=914&id=u0bcde779&originHeight=823&originWidth=1211&originalType=binary&ratio=1&rotation=0&showTitle=false&size=213497&status=done&style=none&taskId=ub73dc7d1-1126-4158-82d6-db9b9bb9942&title=&width=1345.5555912006057)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668651697370-cbd785cc-203a-4f82-a57c-411be633342b.png#averageHue=%23161616&clientId=uad50874a-6552-4&from=paste&height=978&id=u354979ab&originHeight=880&originWidth=1598&originalType=binary&ratio=1&rotation=0&showTitle=false&size=252711&status=done&style=none&taskId=u0a628938-f86d-4495-8738-a49e8bb3735&title=&width=1775.555602591716)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668652007862-465f82d6-64a5-4a09-ae1e-b58b72cf885a.png#averageHue=%231b1b1b&clientId=uad50874a-6552-4&from=paste&height=956&id=u3c57fee5&originHeight=860&originWidth=1267&originalType=binary&ratio=1&rotation=0&showTitle=false&size=352465&status=done&style=none&taskId=ua21fad9e-36f3-4a55-9dfe-4840110b059&title=&width=1407.777815071154)

<a name="NN85W"></a>
# 同一个目录下的贴图转成tx或rsbintex
```python
@echo off 
title texture to tile
set /p texture_path=  要转换的贴图目录：
echo 要转换的贴图目录为%texture_path%
cd /d %texture_path%
set /p renderer=     选择渲染器类型Arnold输入ar，redshift输入rs:
echo 渲染器为%renderer%
if %renderer%==ar goto arnold
if %renderer%==rs goto redshift
:arnold
for %%f in (*) do (
echo %%f的后缀为%%~xf
if /i "%%~xf"==".rstexbin" (echo %%f 
	) else (
		if /i "%%~xf"==".tx" ( echo %%f 
			) else (echo 这个贴图要转换 && "C:\solidangle\mtoadeploy\2018\bin\maketx.exe" -v -u  %%f)
	)
)
goto end

:redshift
for %%f in (*) do (
echo %%f的后缀为%%~xf
REM if "%%~xf"==".rstexbin" (echo %%f 
	REM ) else (
		REM if "%%~xf"==".tx" ( echo %%f 
			REM ) else (echo 这个贴图要转换 && C:\ProgramData\Redshift\bin\redshiftTextureProcessor.exe "%%f")
	REM )
REM )
if /i not "%%~xf"==".rstexbin" (
	if /i not "%%~xf"==".tx" (
		echo 这个贴图要转换 && C:\ProgramData\Redshift\bin\redshiftTextureProcessor.exe "%%f"
	) else (echo 这个贴图不转换 %%f)
)else (echo 这个贴图不转换 %%f)
)

goto end

:end
echo 转换完了。
pause




```
<a name="h4yaF"></a>
# 根据不同项目启动不同maya
```python
@echo off 
choice /C 1234 /T 15 /D 3 /M "1、那托  2、大圣你走开   3、青蛇前源  4、流浪月球"

if errorlevel 4 goto llyq
if errorlevel 3 goto qsqy
if errorlevel 2 goto dsnzk
if errorlevel 1 goto natuo

:llyq
echo 流浪月球
echo maya 2017 
set maya_v=2017
echo arnold 2.1.0.2
copy /v/y "D:\plugins\maya\arnold\maya2017_mtoa2.1.0.2\mtoa.mod" "C:\Program Files\Common Files\Autodesk Shared\Modules\Maya\2017\mtoa.mod"
goto open
:qsqy
echo 青蛇前源
echo maya 2017
set maya_v=2017
echo arnold 3.2.1
xcopy /q /y /v  "D:\plugins\maya\arnold\maya2017_mtoa3.2.1\mtoa.mod"  "C:\Program Files\Common Files\Autodesk Shared\Modules\Maya\2017\"
goto open
:dsnzk
echo 大圣你走开
echo maya 2018 
set maya_v=2018
echo arnold 2.1.0.2
robocopy  "D:\plugins\maya\arnold\maya2018_mtoa2.1.0.2" "C:\Program Files\Common Files\Autodesk Shared\Modules\Maya\2018" "mtoa.mod" /S /NDL /NFL   
goto open
:natuo
echo 那托
echo maya 2018
set maya_v=2018
echo arnold 3.2.1.1
"D:\Program Files\FastCopy385_x64\FastCopy.exe" /cmd=move /speed=full /force_close /no_confirm_stop /force_start "D:\plugins\maya\arnold\maya2018_mtoa3.2.1.1\mtoa.mod" /to="C:\Program Files\Common Files\Autodesk Shared\Modules\Maya\2018"
goto open

:open
echo %maya_v%
set root_maya="C:\Program Files\Autodesk\Maya%maya_v%\bin\maya.exe"
echo %root_maya% 
start "" %root_maya%
pause

```

