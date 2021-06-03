# Typora+PicGo+Gitee笔记方案

**前言：**需要学习的知识太多，从一开始就在寻找一款能让我完全满意的编辑器，然而一直都没有令我满意的。在前两天Typora新版本更新后，总算是拥有了一套我认为很完美的笔记方案：使用Typora编写markdown笔记，使用Gitee作为图床，并使用Typora新版本整合的PicGo软件实现图片自动上传。

## 一、工具

**Markdown**是一门易于上手能帮助作者专心写作的文档编辑语言，它的好处太多了，建议想自己动手做笔记写博客的朋友都可以学一学，10分钟上手，从此不用在为排版烦恼。

[Typora](https://www.typora.io/)是一款优雅的markdown编辑器，所见即所得的编辑方式让我爱不释手，也推荐给大家。

[Gitee](https://gitee.com/)是国内版的Github，功能跟Github基本一样，主要是在国内访问非常快，作为图床和笔记文件存放仓库非常合适。

[PicGo](https://github.com/Molunerfinn/PicGo/releases)实现自动上传图片并返回markdown格式的图片url，这是自动上传的，也就是在Typora中插入图片就自动帮你上传替换图片的url，对于我们用户是透明的，十分舒服。

## 二、安装步骤

需要注册Gitee账户跟Github一样，就不具体描述了，并创建存放笔记的仓库，比如notebook。

### 1）安装和配置Typora

1. 到官网https://www.typora.io/下载安装即可。
2. 配置图片自动上传：
   1. 偏好设置->图像->插入图片时：选择上传图片。
   2. 偏好设置->图像->上传服务：选择PicGo.app。
3. 使用git将在Gitee上创建的存放笔记的仓库git clone到本地，使用Typora打开目录，之后就可以新增自己的*.md笔记文件，最后使用git add、commit、push上传到Gitee上保存。

### 2）在Gitee上创建图床仓库

1. 在Gitee上创建存放图片的仓库，比如images4mk。
2. 在该项目下创建一个文件夹叫imgs。
3. 在网页上点击头像->设置->私人令牌->生成新令牌（将生成的令牌保存下来）。

### 3）安装PicGo

1. 到github地址https://github.com/Molunerfinn/PicGo/releases下载PicGo软件并安装。

2. 打开PicGo主界面，在插件设置中搜索gitee，安装gitee。安装完之后完成对应配置：

   首先复制Gitee上的图床仓库url，例如：[kest/Blog_images (gitee.com)](https://gitee.com/kest/blog_images)

   1. url：[https://gitee.com](https://gitee.com/)
   2. ower：填gitee的用户名（对应图床仓库url中的kest）
   3. repo：图床仓库名（对应图床仓库url中的Blog_image）
   4. path：img
   5. token：填入在2中生成的新令牌字符串。

3. 将默认图床设置为Gitee图床。

## 三、测试

在Typora中新建md文件，并插入图片，看图片url是否会自动变成gitee的url。