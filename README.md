## Eclipse Che 文档

通过Jekyll 把Che 文档从`.adoc` (AsciiDoc) 文件格式转换为HTML页面。文档被发布在 [https://www.eclipse.org/che/docs](https://www.eclipse.org/che/docs/)。 更新在一个发布周期内同步。

## 构建和预览

在仓库的根路径下有一个名字是`run.sh`的脚本，它启动Docker镜像，挂载源文件，并启动Jekyll。当在本地运行时，通过地址 `localhost:4000`可以访问文档。Jekyll监视着文件的改变并重新生成相关资料，因此你能马上预览到所做的修改。

### 在线构建
[![Contribute](https://che.openshift.io/factory/resources/factory-contribute.svg)](https://che.openshift.io/f?id=factorycgpdptc6cjetbhr5)

### 原生地方式构建

在不用docker构建时， [安装必需的Jekyll依赖](https://jekyllrb.com/docs/installation/):

```
# yum install maven ruby ruby-devel @development-tools
```

然后，不再是运行`run.sh`,而改为直接地运行Maven:

```
$ mvn clean install -Pnative
```

## 增加新页面

为增加一个新的页面，在`src/main/pages/che-<MAJOR-VERSION>/${subdir} `（视你的内容对应的版本，替代 `<MAJOR-VERSION>` 为`6`或`7`）下创建一个`.adoc` 文件。

如果尚没有一个子目录对应于新的页面，就创建一个。查看已有的页面的页头以让生成的HTML页面有预期的名字，标题，和关键字。比如：


```yaml
---
title: "Installing single-user Che on Docker"
keywords: docker, installation
tags: [installation, docker]
sidebar: che_6_docs
permalink: docker-single-user.html
folder: setup
---
```

### 命名

尽量为页面使用短的名字和标题。在页面名称(在页头中的`permalink` )中使用短的横线(`-`)。

### 关键字

检索脚本使用页面标题，概要，和关键字检索相关的结果。确保你的关键字和你新增的页面相关。

### 标签(Tags)

为增加一个新的标签，查阅在 `src/main/pages/che-<MAJOR-VERSION>/tags`中的可用的标签。标签也应该被注册到`src/main/_data/tags.yml`中 ---即标签需要同时在`tags.yml`和一个单独的tag页中创建。

## 格式化和AsciiDoc语法

关于AsciiDoc的语法和通用帮助，请参考 [AsciiDoc Writer's Guide](https://asciidoctor.org/docs/asciidoc-writers-guide/) .

### 链接(Links)

通过如下的语法，实现到内部页面的连接：

```
这是一个链接:file_name.html[到内部页面的链接]
```

不要在文件名字中使用`.adoc`。并且，新增的文件也应该至少在一个sidebar-definition文件中引用，sidebar-definition文件位于`src/main/_data/sidebars/`目录中。


到内部页面的锚（anchors）的链接:

```
link:file_name.html#tag[到内部页面的锚（anchors）的链接]
```

到外部页面的链接：

```
这是一个链接:https://github.com[到外部站点的链接]
```

### 图片文件

图片文件位于`src/main/che/docs/images/`目录中。要发布图片文件，使用下面的语法：

```
image::directory/img.png[alt text]
```

不要把图片添加到目录`image/` 的根的下面 - 或者选择一个已有的子目录或者创建一个，如果没有适合新增加图片的。

图片自动地设置大小。你可以提供一个全尺寸图片的url，和标题与替换文本：

```
.点击查看更大的图片
[link=che/docs/images/devel/js_flow.png
image::devel/js_flow.png[Alt text]
```

不要上传太多的图片除非它是绝对需要的。`.gif`动画图片是好的选择，特别是当解释如何使用复杂的UI特性时。


### 特殊字符

为避免特殊字符被解释为格式化的标记，可以使用通过(pass-through)宏。例如，为避免下划线，星号，或反引号，使用：

```
pass:[VARIABLE_NAME__WITH__UNDERSCORES]
```

## 如何获得支持

* **GitHub issue:** 在这个仓库中[打开问题](https://github.com/eclipse/che-docs/issues/new) 
* **公共讨论:** 加入公共的 [eclipse-che](https://mattermost.eclipse.org/eclipse/channels/eclipse-che) Mattermost 通道与社区和贡献者交流

## 如何做贡献

我们喜欢拉取请求(pull request)和感谢能让文档对用户更有帮助的贡献。参见[贡献指南](https://github.com/eclipse/che#contributing)。
