---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "2021 05 07academic主题应用"
subtitle: "academic introduction"
summary: "免费的开源Wowchemy Website Builder使您可以在10分钟内使用Hugo静态站点生成器轻松创建一个精美简单的网站"
authors: [admin]
tags: ["网络","博客"]
categories: [博客]
date: 2021-05-07T14:21:53+08:00
lastmod: 2021-05-07T14:21:53+08:00
featured: true
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: true
  reading_time: true  # Show estimated reading time?
  share: true  # Show social sharing links?
  profile: admin  # Show author profile?
  commentable: true  # Allow visitors to comment? Supported by the Page, Post, and Docs content types.
  editable: false  # Allow visitors to edit the page? Supported by the Page, Post, and Docs content types.
# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

##  目录

  ### 1. [编辑您的网站](#编辑您的网站)

  1.1. [选择适合您的颜色主题](#选择适合您的颜色主题)

  1.2. [选择适合您的布局](#选择适合您的布局)

  1.3. [自订](#自订)

  1.4. [自我介绍](#自我介绍)

  1.5. [菜单](#菜单)

### 编辑您的网站  

#### 选择适合您的颜色主题
查看颜色主题，并尽享选择自己喜欢的风格的乐趣。

确定颜色主题后，请***config/_default/params.yaml***在文本编辑器（例如在线GitHub编辑器）中编辑文件，然后将theme选项设置为所选主题的名称。
<div class="alert alert-note">
  <div>
  文件***config/***夹中的站点配置文件可以使用TOML或YAML格式设置，例如页面首页。

在将参数添加到配置文件时，请考虑将参数添加到文件的哪一部分，否则它们可能无效。
  </div>
</div>
您的主题带有用于设置标题和文本样式的字体集，但是您可以通过使用以下font选项指定可用字体集之一来覆盖它：

最小（现代）
经典（原始的学术v1样式）
玫瑰（传统衬线）
机器人先生（未来派）
可以使用该选项将字体大小从XS（超小）调整为XL（超大）font_size。

如果您对颜色或字体还不是100％满意，请不要担心，因为这些颜色可以在以后完全自定义。
[返回目录](#目录)
### 选择适合您的布局
无论您是为简历，学术研究，博客，课程，实验室，商业，摄影，作品集或餐厅创建网站，Wowchemy都能为您提供一个布局！

您想发布什么样的内容？Wowchemy支持：

页数：所有常规内容
窗口小部件页面：可以包含许多窗口小部件的页面，例如主页
帖子：博客文章或新闻
出版物：从BibTeX导入您的研究出版物
在线课程：在线共享知识
项目：发布您的投资组合或项目
注意：跨笔记本，版块和页面的内容进行协作
软件文档：记录您的软件项目
演讲/事件：发布您正在演讲的任何演讲
幻灯片：使用Markdown非常有效地编写幻灯片，在您的演讲中展示它们，并在线共享
确定了要发布的内容类型后，请查看可用的首页小部件，然后考虑与您最相关的小部件。

然后，打开您的content/home/文件夹并将active参数设置为true或false每个窗口小部件，取决于您是否希望显示它。您也可以删除不需要的小部件，而不必将其设置active为false。您还可以添加更多的窗口小部件实例，例如显示带有特定标签的博客帖子或出版物，或者添加具有您自己的自定义内容和设计的更多空白窗口小部件。

接下来，让我们根据您的喜好放置小部件。要上下移动窗口小部件，请增加或减小weight激活的每个窗口小部件中参数的值。控件将按照这些权重的升序进行排序，并且权重不必是连续的数字。

<div class="alert alert-note">
  <div>
    如果您的content/home/文件夹为空，请从示例站点填充它
  </div>
</div>

[返回目录](#目录)

### 自订
选择主题和布局后，使其成为自己的主题。

核心参数
网站的核心参数可以在config/_default/params.yaml文件中进行编辑。

在“联系信息”部分下编辑您的个人/公司详细信息：

在此输入的任何详细信息将显示在“联系人”小部件中（如果使用）
对于组织而言，某些联系方式（例如电话）可用于丰富搜索结果（例如在Google上）
要隐藏联系人字段，只需清除值""或在行上加上井号（#）即可将其注释掉
的接触形式可以配置分别在正面物质联系小部件本身
如果您是组织或项目，

编辑您的内容site_type以反映您的业务性质
在下面添加您的组织或项目名称 org_name
将徽标图像另存为，logo.png然后将图像上传到assets/media/文件夹，如果站点的根目录尚不存在assets和media文件夹，则创建和文件夹
在“网站功能”部分下为您的网站启用丰富的内容。如果编写技术内容，请考虑启用以下选项，否则将这些选项设置为：false

代码语法高亮与highlight = true
LaTeX数学与math = true
美人鱼图与diagram = true
该保密包，也可以从激活网站功能部分。启用隐私包后，将向访问者显示Cookie同意消息（链接到您的隐私权政策），并在Google Analytics（分析）中匿名显示访问者IP（如果启用）。

要添加隐私政策，请privacy.md在您的content文件夹中创建一个文件，并draft从最前面删除所有选项以进行发布。

同样，要添加“法律条款”，请创建一个terms.md文件。这些文档的链接将自动显示在您的网站页脚中。
[返回目录](#目录)

### 自我介绍

默认情况下，将使用用户名admin和位于的相应用户配置文件创建一个超级用户content/authors/admin/_index.md。让我们在文本编辑器中打开此文件，然后编辑此文件以使其成为您的个人资料：

将您的显示名称（通常是全名）添加到title字段中
将您的角色/职位或标语添加到role字段
在该bio字段中写一个简短的句子来形容自己-该内容可以在页面内容之后显示在作者列表中
编辑organizations您所属的，或将其设置[]为隐藏
在中列出您的兴趣或爱好interests，或将其设置[]为隐藏
使用education–>courses块列出您的主要资格
可以根据需要创建或删除这些块
要隐藏资格，请删除这些块或通过在其前面加上井号（#）来注释掉这些行
添加您的社交或学术网络链接
这些被定义为的实例，social可以根据需要创建或删除
现在，让我们在最重要的事情之后（即最后---一行之后）添加一个传记或一些有关您的有趣事实。您可以利用Markdown和简码进行格式化。

要显示头像，avatar请在的个人资料文件夹中放置一个名为的方形裁剪人像照片，以content/authors/admin/覆盖示例图像。或者，如果您已有Gravatar / Wordpress虚拟形象，则可以通过将其设置gravatar为并true在中config/_default/params.yaml输入相关的email地址来使用它content/authors/admin/_index.md。请注意，您可以删除示例avatar图像以禁用头像功能。

设置好帐户后，根据演示文章，您可以在内容开头的authors字段中引用您的用户名。

您的显示名称，您的用户配置文件中输入，将自动出现在网页的元数据。您也可以在authors页面字段中输入其他名称，如果需要，还可以选择为它们创建用户个人资料。如果不存在作者的用户个人资料，则其姓名将与您在前件中输入的姓名完全一样。

<div class="alert alert-note">
  <div>
    通过重命名文件夹，可以从admin更改超级用户的用户名admin。用户名必须是小写字母，并且所有空格都用连字符（-）代替。
  </div>
</div>

<div class="alert alert-note">
  <div>
    如果更改用户名，则可能希望从author“关于”窗口小部件（content/home/about.md）的authors字段以及引用该用户的任何页面的开头的字段中更新对该用户名的任何引用。
  </div>
</div>

[返回目录](#目录)

#### 菜单

可以在config/_default/menu.toml文件中编辑导航菜单：

这些[[main]]条目定义了网站顶部的导航链接。根据您在上面选择的布局，可以根据需要添加或删除它们。

要链接到主页的某一部分，请使用形式#<section-filename>where<section-filename>文件名（不带.md扩展名）。例如，#posts引用具有filename的部分posts.md。您可以在中重命名分区文件content/home/，只需记住-在文件名中使用破折号（）而不是空格。

<div class="alert alert-note">
  <div>
    要创建下拉子菜单，请添加identifier = "a-unique-reference"到父项和parent = "a-unique-reference"子项，并替换a-unique-reference为您选择的唯一引用。
  </div>
</div>

在此处阅读更多有关底层Hugo菜单系统的信息。

添加您的内容
请参阅我们的内容管理指南，以创建自己的内容，例如博客文章，出版物，在线课程，讲座和项目等。

删除所有未使用的示例页面
通过删除示例模板中剩余的所有未使用的页面来整理您的网站。

[返回目录](#目录)
