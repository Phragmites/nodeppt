title: 二手发布前端业务讲解
speaker: 李文文
url:https://github.com/leeww/nodeppt/blob/master/postShare/post.md

[slide]
# 二手发布前端业务讲解
## 李文文

[slide data-transition="move"]
## 主要内容
- 发布现状 {:&.moveIn}
- 代码位置及孙悟空注意事项
- 组件化目录结构
- 基本打包命令 
- 需求开发过程
- 上线

[slide data-transition="horizontal"]
## 发布现状
---- 
- 主要包括三端发布**（PC/M/APP）** + **VIP**发布
- 其中PC、M是组件化的，目前开发分支的代码已迁移到转转的git上
- APP和VIP未组件化且没有开发分支，一般做需求都是直接修改线上分支代码
- 目前主要做的就是发布的扫尾工作，把一些异步请求添加上salepost的标识且同步到git上

[slide data-transition="vertical3d"] 
 ## 代码位置(PC和M)
 ---  
端| 旧的svn | 新的git
:-------|:------:|-------:
PC |svn://10.9.192.100/post/pc-refactor | git@gitlab.58corp.com:wangguanjia/ZZPublish.git 
M | svn://10.9.192.100/post/m_refactor_new | git@gitlab.58corp.com:wangguanjia/ZZPublish.git
备注 | PC的在pc_post目录下，M的在m_post目录下，svn账号权限找**@闫龙波yanlongbo**申请|

[slide data-transition="horizontal3d"]
## 代码位置(APP和VIP)
---- 
- 所有前端上线分支的代码：`svn://10.9.192.100/prod`
- APP:`\prod\app58_static\pic2.58.com\m58\app58\m_static\js(css)`
- VIP代码特别混乱，一般修改的代码存放在`\prod\pc\static.58.com\js\5_1\91\34-es.js`里面

[slide data-transition="zoomin"]
## 孙悟空注意事项
- PC和M组件里面有两个孙悟空策略相关的组件：一是支付相关的payPost组件，一是联系人认证相关的limitPost组件；
- 目前孙悟空相关的东西已经交接给信质了，如果这两个组件做了改动，他们会同步给各个业务线，因为咱们代码已经迁移了，需要先更新一下以前svn的代码，然后手动同步到咱们的git上;
- `/pc-refactor/src/component/limitPost(payPost)`
- `/m_refactor_new/src/component/limitPost(payPost)`

[slide data-transition="vertical3d"]
## 以PC发布为例，组件化目录结构
![以PC发布为例，组件化目录结构](https://github.com/leeww/nodeppt/blob/master/postShare/img/directory_structure.png)

[slide data-transition="horizontal3d"]
## 常用打包命令 
```
//css打包命令和js打包命令
>cd 到pc-refactor目录下
gulp ershou_moto ershou_bike css  //css打包命令，多个分类之间用空格分割
gulp ershou_moto ershou_bike cate //js打包命令

//解析formDefine中的规则配置给后台RD
>cd到tools目录下
>node generateCheckRule.js ershou_moto ershou_bike
```

[slide data-transition="newspaper"]
## 需求开发过程(PC/M/VIP)
- PC:PC主要是在开发分支上进行修改，目前二手所有分类都是组件化的，所有的需求基本都是在以前的基础上修改，一般主要动的就是`/src/data`、`/src/component`、`/src/categary`这三个目录，具体看需求；
- M:M端票务的相关分类操作跟PC类似，剩余二手分类公用一个js文件，开发分支上没有，也是直接修改线上的文件`prod\m\static.58.com\m58\postnew\ershou\js\ershou.js`
- VIP基本都在`34-es.js`里面修改;（vip的需求较其余三端的不太多）

[slide data-transition="circle"]
## 需求开发过程(APP)
- 一般是直接在线上分支上直接修改，联系人相关的在`limitpost_appcommon.js`文件里面，别的基本都在`mclient.publish-ershou-cf.js`文件里面，具体修改看需求；
- APP的开发有时会和native有交互，app.js帮助文档http://apptest.58.com/static/doc/58app/index.html#!/api/app58
- mclient.framework5.js帮助文档:http://wiki.58corp.com/index.php?title=Web%26native%E9%80%9A%E4%BF%A1%E5%8D%8F%E8%AE%AE

[slide data-transition="cover-diamond"]
## 上线(PC/M/VIP)
- PC&M: 打包后文件存放在dist目录下，直接复制到线上分支，使用fcm上线即可:http://fcm.58corp.com/
- VIP在线上分支上修改之后也是使用fcm上线
- 后续listing这边可能要重新搭一个上线系统

[slide data-transition="cover-circle"]
## 上线(APP)
- APP上线使用无线提供的rms系统，需要找**@张天翔zhangtianxiang**申请帐号：http://rms.58corp.com/
- 即使在rms上上线，也要记得提交到svn
- 具体操作见：http://note.youdao.com/noteshare?id=7b29ad12d6a92347f312b1f8013f1ef8&sub=EDD0A44FF53F48CEADEBD13B283B98CA

[slide data-transition="circle"]
## Thank you
## Q&A
