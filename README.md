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

检索脚本使用页面标题，概要，和关键字检索相关的结果。确保你的关键字和你新增的页面页面相关。

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

Do not add images into the root of the `images/` directory - either choose an existing sub-directory or create one if none of them fits the new image.

Images are sized automatically. You can provide a URL to a full-size image, as well as a caption and alt text:

```
.Click to view a larger image
[link=che/docs/images/devel/js_flow.png
image::devel/js_flow.png[Alt text]
```

Do not post too many images unless it is absolutely necessary. Animated `.gif` images are preferred, especially when explaining how to use complex UI features.

### Special characters

To prevent special characters from being interpreted as formatting mark-up, use pass-through macros. For example, to escape underscores, asterisks, or backticks, use:

```
pass:[VARIABLE_NAME__WITH__UNDERSCORES]
```

## How to get support

* **GitHub issue:** [open an issue](https://github.com/eclipse/che-docs/issues/new) in this repository
* **Public Chat:** Join the public [eclipse-che](https://mattermost.eclipse.org/eclipse/channels/eclipse-che) Mattermost channel to talk to the community and contributors

## How to contribute

We love pull requests and appreciate contributions that make docs more helpful for users. See the [Contribution guide](https://github.com/eclipse/che#contributing).
