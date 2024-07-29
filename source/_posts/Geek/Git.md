---
title: Git
tags: Git
categories: Geek
abbrlink: 69c3279c
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

<a name="VwMGb"></a>
# 安装
去官网下载，然后无脑下一步
<a name="PJY3l"></a>
# 注册账号
进入 Git Bash<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669040621480-d85eb128-78ab-4c88-b36c-806b2ac97685.png#averageHue=%23242423&clientId=u10eb3d9e-7294-4&from=paste&height=164&id=ue0e8ebb4&originHeight=164&originWidth=274&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7854&status=done&style=none&taskId=u5b39029c-ffb9-4796-8698-b2c197f6b0d&title=&width=274)<br />输入用户名 邮箱来注册，框住的内容为自定义<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669040650975-6616584c-2a11-47c3-a81e-41f7310291e5.png#averageHue=%23030302&clientId=u10eb3d9e-7294-4&from=paste&height=367&id=u7e3c761b&originHeight=367&originWidth=719&originalType=binary&ratio=1&rotation=0&showTitle=false&size=129387&status=done&style=none&taskId=ue36240d8-9535-4c6d-8809-dc4d80d3539&title=&width=719)
<a name="lED8v"></a>
# 获取git版本库
<a name="Zpcaq"></a>
## 将本地的文件夹变成git版本库
在想要变成git版本库的文件夹下右键使用git bash![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669041397312-587a89eb-d6ca-4d32-844d-ea041090b575.png#averageHue=%23e9e9e9&clientId=u10eb3d9e-7294-4&from=paste&height=402&id=u4b3f9cb6&originHeight=402&originWidth=458&originalType=binary&ratio=1&rotation=0&showTitle=false&size=23186&status=done&style=none&taskId=ub039647d-eeb6-4a63-93f8-76ce6bb49df&title=&width=458)<br />输入命令  git init<br />带有.git的就代表这个文件夹已经是git版本库了<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669041441689-733f517d-1308-4a94-baaf-96509ea4656f.png#averageHue=%23fcfbf9&clientId=u10eb3d9e-7294-4&from=paste&height=228&id=u3b89c54e&originHeight=228&originWidth=523&originalType=binary&ratio=1&rotation=0&showTitle=false&size=17856&status=done&style=none&taskId=ub551a34a-d94e-4554-86c4-cf5ad5cf163&title=&width=523)
<a name="c0OsB"></a>
## 将其他人的git库克隆到本地
使用git clone命令<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669041841250-14dce49d-f465-4ed9-b64b-1922aa8c9a97.png#averageHue=%23161815&clientId=u10eb3d9e-7294-4&from=paste&height=50&id=ue65dcb27&originHeight=50&originWidth=1152&originalType=binary&ratio=1&rotation=0&showTitle=false&size=59161&status=done&style=none&taskId=u881382c4-4162-4476-85ee-29f7d2f9d75&title=&width=1152)<br />右边的地址可以通过github中找到<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669041868693-698b9c68-78e6-4274-bc8f-4474e8a33dc9.png#averageHue=%23ddbd7b&clientId=u10eb3d9e-7294-4&from=paste&height=399&id=u566bc653&originHeight=399&originWidth=442&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27469&status=done&style=none&taskId=u4f00f38e-b805-4e1c-8baa-54e404ac044&title=&width=442)<br />因此可以将自己的代码上传到github，这样之后在任何地方都可以通过这个地址将git库安装过来
<a name="vsjLV"></a>
# git仓库的三种状态以及对应工作区
<a name="QPcJv"></a>
## 三种状态
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669042292284-e01fba27-6085-43d0-8605-d975cd495f37.png#averageHue=%233d3d3d&clientId=u10eb3d9e-7294-4&from=paste&height=279&id=u919397af&originHeight=279&originWidth=551&originalType=binary&ratio=1&rotation=0&showTitle=false&size=157445&status=done&style=none&taskId=u072f1028-0599-4d9f-bcf7-f0551492fc6&title=&width=551)
<a name="CkWKT"></a>
## 对应工作区
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669042272485-adace1b3-77fd-4c64-ac95-f11fb0e0f8f9.png#averageHue=%23393939&clientId=u10eb3d9e-7294-4&from=paste&height=485&id=ua4691269&originHeight=485&originWidth=1361&originalType=binary&ratio=1&rotation=0&showTitle=false&size=695792&status=done&style=none&taskId=u7ebfb571-be9b-4ec6-8074-be801f86b19&title=&width=1361)
<a name="JgEFb"></a>
# 查看版本库的状态（使用git时第一个要用的命令）
git status 用于查看当前版本库的状态<br />git status -short  或者是 git status -s 是以简单信息的形式查看版本库状态<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669042876861-4b2e071d-5fe3-4da5-ac5d-e0a6c05073df.png#averageHue=%230b0705&clientId=u10eb3d9e-7294-4&from=paste&height=119&id=uf1f9713b&originHeight=119&originWidth=160&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4404&status=done&style=none&taskId=ua825efc3-27ca-4386-9bbb-6e135084316&title=&width=160)<br />使用git status -s 出现的信息中各符号代表的含义：<br />空格也有含义，含义是表示当前文件在暂存区的状态<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669042950720-5b048eae-d58c-4f48-b79c-75b9b59c9879.png#averageHue=%23464640&clientId=u10eb3d9e-7294-4&from=paste&height=196&id=udf58f32e&originHeight=196&originWidth=216&originalType=binary&ratio=1&rotation=0&showTitle=false&size=40012&status=done&style=none&taskId=u34380527-6c0e-4872-8663-50ceaf2b4e0&title=&width=216)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669042862405-1ae074ea-aba7-4641-9942-4cd4aead9e5c.png#averageHue=%23b9b9b9&clientId=u10eb3d9e-7294-4&from=paste&height=735&id=ue16ca3a4&originHeight=735&originWidth=1568&originalType=binary&ratio=1&rotation=0&showTitle=false&size=395006&status=done&style=none&taskId=u35cdee9b-6bf7-4f85-80cf-184d27485c7&title=&width=1568)
<a name="PiP9u"></a>
# 文件的追踪和更新

git add 文件名或者文件夹名（如果文件名或者目录名里带有空格，就需要将名字用双引号包含住）<br />添加当前目录： git add .  (点来代表当前目录，添加当前目录不会添加空文件夹，如果想要添加空文件夹需要在文件夹下随便创建一个空的文件)<br />git add除了可以用它来开始追踪新的文件或者把已经追踪的文件放到暂存区，还能用于合并时把有冲突的文件，标记为已解决状态等。
<a name="dCNen"></a>
## 提交更新
git commit -m "这里填写更新信息"

使用git commit的话会自动跳出填写日志信息的编辑器，默认是vim编辑器。如果使用git commit -m 就不会弹出编辑器![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669044499302-80ef4cfd-b27d-46c5-a904-97604d9c91c1.png#averageHue=%23302b2a&clientId=u10eb3d9e-7294-4&from=paste&height=471&id=ua8e01e07&originHeight=471&originWidth=1369&originalType=binary&ratio=1&rotation=0&showTitle=false&size=172925&status=done&style=none&taskId=u4c0654ba-5f18-4338-a2d6-734b1d2e334&title=&width=1369)
<a name="VBTc8"></a>
# 历史版本追踪与文件忽略
<a name="N7dZH"></a>
## git log
git log 会按照提交的时间列出所有的更新，最新的更新会排在最上面，按回车键进行翻页，按q键可以退出查看<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669046034315-c4e587d9-7bcb-43e6-8419-10823b86c375.png#averageHue=%236c643b&clientId=u10eb3d9e-7294-4&from=paste&height=531&id=u48d4d0d1&originHeight=531&originWidth=859&originalType=binary&ratio=1&rotation=0&showTitle=false&size=335691&status=done&style=none&taskId=uaabc464e-271a-4dd1-8773-59d36a9f36e&title=&width=859)<br />git log -p 加上-p会使输出信息附带每次commit发生的变化<br />git log -p -数字 会显示最近三次的提交的详细信息<br />git log --stat 会显示被修改文件的哪些行被移除了或是添加了<br />git log --since=2.weeks 会显示两周内所有的更新
<a name="F0ouc"></a>
## git diff
git diff 显示当前工作目录中当前文件和暂存区域快照之间的差异  也就是修改之后还没有暂存起来的内容<br />git diff --staged  查看已经暂存的将要添加到下一次提交里的内容<br />git diff SHA-1校验码  SHA-1校验码  可以对比前后文件的差异， SHA-1校验码可以通过 git log 获取 文件校验码很长，一般只需要SHA-1校验码中的4个字母即可找到对应的文件
<a name="hhtfs"></a>
## 头指针-HEAD指针
HEAD指针也叫头指针，HEAD指针默认指向当前版本库的最后一个版本，我们可以使用HEAD指针来对比当前版本与某一历史版本之间的差别<br />因此 可以通过HEAD指针来代替 最新SHA-1校验码。<br />git diff HEAD SHA-1校验码 即可对比当前版本库与SHA-1校验码对应的版本库之间的差异<br />HEAD^代表当前版本的上一版本<br />HEAD^^代表当前版本的上上版本<br />因此也可以使用 git diff HEAD HEAD^ 来显示当前版本与上一版本的区别
<a name="kHD3u"></a>
## 还原历史版本
<a name="blFBq"></a>
### git checkout
git checkout 可以将HEAD指针移动到任意版本处（意思就是还原整个仓库）（比较复杂，需要深入学习）<br />还原某一个文件：<br />git checkout HEAD^ test_file.txt   将test_file.txt 文件还原至上一版本<br />git checkout -- 文件名 清空当前未被追踪的改动（撤销还未提交的针对文件的改动）
<a name="jimCH"></a>
### git  revert
这个命令和git checkout 的区别是这个命令会新建一个版本，因此不会导致修改历史的消失。<br />git revert 命令只能用于工作区和暂存区都为空的时候才可以被使用（工作区是否为空可以通过git status来查看）<br />git revert HEAD
<a name="Ie0dG"></a>
### git reset
这个命令可以直接将部分文件或者整个仓库还原到某个历史状态下，与此同时，暂存区的内容也会被清理掉。变为未被追踪的状态。<br />因为这个命令很容易导致代码丢失，所以不推荐使用这个命令。<br />如果希望回退版本建议使用 git revert
<a name="YoOFP"></a>
## 忽略文件
如果希望git仓库不追踪某些文件<br />那么可以在仓库中创建一个.gitignore文件来忽略某些文件<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669049477776-b3937239-d487-4d6c-82a6-f237fd2c346c.png#averageHue=%232e2c2b&clientId=u10eb3d9e-7294-4&from=paste&height=468&id=uc5d22b94&originHeight=468&originWidth=1019&originalType=binary&ratio=1&rotation=0&showTitle=false&size=152355&status=done&style=none&taskId=uac0508cb-9dd9-4693-9eb5-a3b5f9f7767&title=&width=1019)
<a name="frU53"></a>
### 举例
在仓库中右键新建一个文本，然后改名叫.gitignore. (如果是windows系统那么需要前后都有点)。然后打开这个文件输入*.txt 意思就是忽略所有以.txt结尾的文件
<a name="Xq2XB"></a>
### .gitignore模板
[https://github.com/github/gitignore](https://github.com/github/gitignore)
<a name="YPr6V"></a>
# Git分支操作
使用分支可以把工作从开发主线上分离，以免影响开发主线，对于社会化协作的项目来说，分支提供了很好的代码隔离的功能，核心开发者们可以借助对比分支的方式对新加入的代码进行审核，并在其中挑选出有用的分支，合并到主分支当中以确保项目的健康稳定。
<a name="VfJbq"></a>
## 查看分支
git branch  会显示当前库中的分支，当前使用的分支会以*开头标注<br />git branch -a  查看远程分支(显示所有分支)
<a name="Wz0jd"></a>
## 创建、切换、修改、删除分支
创建：<br />使用 git init 命令会自动创建一个 master 分支 <br />git branch 分支名 创建一个新的分支<br />切换<br />git checkout 分支名可以切换分支(新建分支并不会直接切换到新建的那个分支，需要用到这个命令来切换)  <br />切换分支时必须谨慎地关注工作目录中文件的变化，切换分支的同时会将工作目录更改为不同分支对应的目录<br />修改<br />git branch -m 分支名 新分支名   修改分支的名字<br />删除<br />git branch  -d 分支名  删除某一个分支<br />git branch -D 分支名  强制删除一个还没有合并的分支
<a name="sD2UH"></a>
## 合并分支
首先 git checkout 到想要并入的分支然后再使用merge命令合并<br />命令： git merge <想要使其合并到当前分支的那个分支名>  
<a name="zhoMR"></a>
## 合并冲突
假如一个主分支分出来的两个分支对同一文件进行了编辑，那么合并这两个分支时就会产生合并冲突。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669103436797-8f350751-23dc-4dc3-8476-ad418c152eee.png#averageHue=%233c3c3c&clientId=ud3c6b9f0-5404-4&from=paste&height=448&id=u7034298f&originHeight=403&originWidth=974&originalType=binary&ratio=1&rotation=0&showTitle=false&size=329736&status=done&style=none&taskId=ueef31e00-da71-45c9-a3f2-2ba4307c0a1&title=&width=1082.2222508913212)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669103718823-24e88be4-6372-4477-9434-a47e735e5f39.png#averageHue=%23f0f0e9&clientId=ud3c6b9f0-5404-4&from=paste&height=227&id=u5ba6dfa7&originHeight=204&originWidth=602&originalType=binary&ratio=1&rotation=0&showTitle=false&size=91357&status=done&style=none&taskId=ua6731bae-0932-402d-81bb-052a2938c2e&title=&width=668.8889066083937)<br />处理完有冲突的文件后，使用git add 重新添加这个文件进行提交即可解决冲突
<a name="rJwqJ"></a>
# 协作开发中的分支架构

<a name="HgevY"></a>
## 协作项目中的分支规则
根据分支存在的生命周期长短不同，大致上将分支分为长期分支，和短期分支两种<br />长期分支是指一直存在的分支，短期分支指的是用完即销毁的分支<br />短期分支可以将问题集中化，一个分支只解决一个问题，非常适合用作单一特性的开发，或明确的bug修复等这样的短期工作<br />长期分支更加适合解决整个项目运行过程中一直需要应对的问题，比如存放当前可运行的最终代码，或者临时存放需要测试的代码等
<a name="EZcOq"></a>
## 适合协作的分支架构
master 分支是版本库初始化时自动被创建出来的分支，项目中所有的分支都来源于这个分支。<br />master分支来管理发布后的最终代码，在除了初始化阶段外的任何时候，master分支上的代码都应当是稳定和可用的。<br />dev分支是用来维护整个开发的进程的，所有的特征分支（短期分支，针对某一项进行开发）都需要从这个分支开始，并最终合并回这个分支。<br />当任务创建出来之后，特征分支就可以随时被创建出来，开发者们在特征分支上不断的提交更新，直到完成开发工作，最终将特性分支合并到dev分支上并删掉原有的特性分支，当dev分支上的代码已经达到了可用的阶段时即可进入发布，发布的目的是将开发完成的代码打包成一个可以直接使用的软件。<br />发布阶段可以从dev分支创建一个短期的release分支或是将dev分支合并到一个长期的release分支上进行测试和编译，测试中的修改可以继续在这个分支上进行，但是当发布完成后一定要将所有的修改合并回dev分支，并将最终的代码合并到master分支上。<br />当发现master分支上的代码，存在紧急的bug的时候，则需要临时创建一个hotfix分支来快速的修复，hotfix分支和特征分支一样，也应当是短期的分支，当bug修复之后，即需要尽快的将其合并到master和dev上以保持代码的可靠性。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669111005370-b3bc1eae-cb77-4d9e-93a6-d0b1e95788e1.png#averageHue=%23b0afae&clientId=u833f77fa-b51c-4&from=paste&height=857&id=u8c75defb&originHeight=771&originWidth=1480&originalType=binary&ratio=1&rotation=0&showTitle=false&size=285161&status=done&style=none&taskId=uaf727463-7844-4fd8-9484-5fdc2d357e4&title=&width=1644.4444880073465)
<a name="IxvAr"></a>
## 远程分支操作

如果想要为本地自己 init 的git库添加远程库则可以使用这个命令：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669111802352-9c5513fc-daea-4527-b108-2ab22a2c85aa.png#averageHue=%23e0e0e0&clientId=u833f77fa-b51c-4&from=paste&height=141&id=wWycq&originHeight=127&originWidth=681&originalType=binary&ratio=1&rotation=0&showTitle=false&size=29794&status=done&style=none&taskId=u000266d7-1c59-4c10-8ac9-5be16200bf3&title=&width=756.6666867114885)

git  remote -v  查看当前版本库的远程库![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669107337652-fcb15e05-d5f0-4fca-9786-8b5ce348d521.png#averageHue=%230b0705&clientId=u833f77fa-b51c-4&from=paste&height=61&id=u880605ef&originHeight=55&originWidth=532&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3281&status=done&style=none&taskId=u8a6268ce-38d6-49b4-9a26-2c02e8eeb9b&title=&width=591.1111267702083)  fetch是下载，push是上传<br />git remote add  <git库名字> <git库路径>  可以额外添加远程分支<br />在远程库被添加之后，本地仓库中则会同时出现本地的分支和远程的分支，那些存在于远程库中的分支并不会将本地的分支覆盖或与之自动的合并，而是会以远程分支的形式存在<br />远程分支以远程库的名称作为名称空间并以斜杠作为连接符与原本的分支名连接![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669112698223-efe49e5b-4b2b-4fa7-9dc5-2daf96b01a08.png#averageHue=%234c3325&clientId=u833f77fa-b51c-4&from=paste&height=336&id=u16bd6dfa&originHeight=302&originWidth=917&originalType=binary&ratio=1&rotation=0&showTitle=false&size=169845&status=done&style=none&taskId=udb7a5350-78c1-418c-988a-4c1b142d5bd&title=&width=1018.8889158802275)<br />远程分支其实也存在于本地的版本库当中。与本地分支不同，远程分支并不能直接被修改，它的功能是用于与远程库中相同的分支进行信息同步，远程分支中的信息一般和远程库中保持一致，当远程库有新的更新时可以使用git fetch命令更新本地仓库的远程分支。<br />**从远程库拉取新代码：**<br />例如当远程库origin发生了更多的操作而导致与本地库不同时则可以使用，git fetch origin命令从远程库origin中同步更新所有的远程分支信息。更新完远程分支信息之后则可以使用git merge 命令将其合并到对应的本地分支上。<br />也可以通过 git pull <远程库名> <分支名> 来一步到位同步远程库的远程分支到当前的分支，这里举例就是将origin远程库的new_test分支合并到当前的new_test分支![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669112832693-cbfc834e-4491-4d0d-8e22-7497d85db3a7.png#averageHue=%2347432a&clientId=u833f77fa-b51c-4&from=paste&height=158&id=u01768d09&originHeight=142&originWidth=999&originalType=binary&ratio=1&rotation=0&showTitle=false&size=110225&status=done&style=none&taskId=u6b8849d3-78ff-473b-9471-38a887ea550&title=&width=1110.000029404959)<br />git branch -vv 来查看本地分支与远程分支之间的关联 关系<br />如果本地分支与远程分支之间已经建立了关系，则更新时就可以直接省略远程库名和分支名，直接写为 git pull<br />将远程分支同步到本地：git checkout origin/remote_branch  这样本地就会自动创建一个 remote_branch分支并与origin/remote_branch关联<br /> 当修改了本地分支后，如果希望将其推送到远程库中时，则可以通过 git push  origin 分支名 将当前活动的本地分支推送到远程库上的同名分支上去，如果远程的同名分支不存在则会被新建出来。

<a name="czXKA"></a>
# Git常用命令以及注意事项
将本地的代码上传到github的流程：[https://cloud.tencent.com/developer/article/1648509](https://cloud.tencent.com/developer/article/1648509)<br />git clone 把远程库克隆到本地进行开发<br />git branch 创建一个要添加修改的分支（一个公司的，一个家里的）<br />git push origin + 你现在的分支名   向远程库推送自己的更新   (vscode有插件可以用vscode来推送)<br />git pull --rebase origin master  更新远程主分支的内容到本地
<a name="is5A4"></a>
## vscode 结合 git的使用说明：
[https://blog.l0v0.com/posts/94ffdbdf.html](https://blog.l0v0.com/posts/94ffdbdf.html)<br />[https://blog.l0v0.com/posts/a91a4c58.html](https://blog.l0v0.com/posts/a91a4c58.html)
<a name="prTdb"></a>
## 使用SSH来传输
[https://blog.csdn.net/qq_38163309/article/details/105335097](https://blog.csdn.net/qq_38163309/article/details/105335097)<br />[https://www.bilibili.com/video/BV1EE41157ro/?spm_id_from=333.1007.top_right_bar_window_history.content.click](https://www.bilibili.com/video/BV1EE41157ro/?spm_id_from=333.1007.top_right_bar_window_history.content.click)
<a name="lDoBO"></a>
## Git常用命令汇总
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669141756421-248ed107-f546-4217-8b43-b07992da53f7.png#averageHue=%23d5cac1&clientId=u8964c6e1-bf9f-4&from=paste&height=552&id=ua4edb5a1&originHeight=552&originWidth=872&originalType=binary&ratio=1&rotation=0&showTitle=false&size=158354&status=done&style=none&taskId=u513d86e8-3365-44f3-8782-1c3a42caab5&title=&width=872)
<a name="WyD7T"></a>
## 注意事项
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669141951237-6197a90e-22b0-41f4-890a-22b819adca3f.png#averageHue=%23ededec&clientId=u8964c6e1-bf9f-4&from=paste&height=652&id=u398dc4fe&originHeight=652&originWidth=1526&originalType=binary&ratio=1&rotation=0&showTitle=false&size=275541&status=done&style=none&taskId=ua3431058-5efb-4678-85dc-33fcc6f2a46&title=&width=1526)

# 上传本地文件（夹）到GitHub
>https://zhuanlan.zhihu.com/p/136355306
