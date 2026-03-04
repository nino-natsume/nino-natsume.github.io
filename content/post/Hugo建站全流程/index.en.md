---
date: '2026-02-28T11:00:00+09:00'
title: 'Hugo Website Building Process'
categories:
  - 次元星域
tags:
  - Jigen_Seiki
  - hugo
  - tutorial
---
{{< heatMapCard levelStandard="200,700,1000" >}}
# Introduction

Since I didn't want to create a separate blog for this tutorial, I'll use this article to explain everything in detail, ensuring you can successfully set it up as much as possible.

This article uses the Hugo framework and the hugo-theme-reimu theme. From creation and configuration to deployment, it's explained clearly in one article. For other themes, please refer to their official documentation.

## **Article Understanding and Configuration Instructions:**

To help you understand this article, I strongly recommend reading this explanation to understand which folder corresponds to which part of the tutorial below:

| Folder or File | Meaning |
| :----: | :----: |
| /blog | Initial folder |
| /blog/blog | Blog directory. If you customize it, please modify it accordingly, such as /blog/0721 |
| /blog/blog/xxx | Files or folders at the corresponding path in the blog directory |
| /theme/hugo-theme-reimu/xxx | Files or folders at the corresponding path within the theme folder |

## Preliminary Notes:

1. I am not the theme author; this is merely a personal deployment process explanation.

2. This article will be entirely text-based. If you have any questions, please leave a comment below or contact info@natsume.xin.

(Below is the tutorial text)

# Hugo Personal Blog Full Setup Tutorial

## 1. Environment Setup

### 1.1 Git Download

1. Go to [Git Official Website](https://git-scm.com/) and download the installer.

2. Keep clicking Next; the default installation is fine. If you don't understand the meaning and function of the options, try not to modify them!

### 1.2 Hugo Download

1. Go to the official Hugo Github page (https://github.com/gohugoio/hugo/tags), select the first latest version, download and extract.

2. The source code above is the latest version for Windows; the one with `withdeploy` is best.

### 1.3 Download Theme

1. Go to the official Hugo Theme Reimu page (https://github.com/D-Sketon/hugo-theme-reimu/tags), again select the first latest version.

2. After downloading the source code, extract it, delete the version number after the filename, keeping only `hugo-theme-reimu`. Edit the theme folder and set it aside.

## 2. Deploying the Blog

### 2.1 Creating a Blog

1. Go to `/blog`, type `cmd` in the folder's address bar to open the command line.

2. Type `hugo new site blog` to create the main Hugo blog file.

3. Continue by typing `cd blog`, and then navigate to the parent folder... After copying hugo.exe into your blog, the file path of the /blog folder should be:
```blog/
blog/
|- blog/
|  |-archetypes/
|  |-assets/
|  |-content/
|  |-data/
|  |-i18n/
|  |-layouts/
|  |-static/
|  |-themes/
|  |-hugo.toml
|- hugo.exe
|- LICENSE
|- README.md
```

4. Enter `hugo server -D` to start the blog. After seeing `http://localhost:1313`, Ctrl + click the address to access it. At this point, the browser will display the text "Page Not Found", indicating that the blog service has started successfully.

5. Press Ctrl + C to exit; otherwise, the browser will pop up a warning after any subsequent operation or save.

### 2.2 Initial Configuration

To ensure the theme runs smoothly, it is recommended to perform all the following steps:

1. Create a `config` folder in `/blog/blog`, and create a `_default` folder inside the `config` folder. The current path should be: `/blog/blog/config/_default/`

2. Copy or drag the theme folder (prepared in step 1.3) into `/blog/blog/theme`. The current path should be: `/blog/blog/theme/hugo-theme-reimu/`

3. Copy `theme/hugo-theme-reimu/config/_default/params.yml` into `/blog/blog/config/_default`

4. 5. Copy all files from `theme/hugo-theme-reimu/data` to `/blog/blog/data`.

6. Copy all files from `theme/hugo-theme-reimu/_example` to `/blog/blog/content`. Create this folder if it doesn't exist.

7. Copy all files from `theme/hugo-theme-reimu/assets` to `/blog/blog/assets`.

8. Copy all files from `theme/hugo-theme-reimu/layouts` to `/blog/blog/layouts`.

9. Copy all files from `theme/hugo-theme-reimu/static` to `/blog/blog/static`.

10. Copy the following code to `/blog/blog/hugo.toml`.

                                                                                                Click below 👇 to expand
```hugo.toml
baseURL = 'https://example.com/xxx'
theme = 'hugo-theme-reimu'
defaultContentLanguage = 'zh-CN'
enableEmoji = 'true'
[languages]
[languages.zh-CN]
languageCode = 'zh-CN'
languageName = '简体中文'
weight = 1
hasCJKLanguage = 'true'
title = 'xxxxxxxx'
author = 'xxxxxxxx'

[languages.en]
languageCode = 'en'
languageName = 'English'
weight = 2
hasCJKLanguage = 'true'
title = 'xxxxxxxx'
author = 'xxxxxxxx'

[languages.ja]
languageCode = 'ja'
languageName = '日本語'
weight = 3
hasCJKLanguage = 'true'
title = 'xxx'                                      # 自己编辑
author = 'xxx'                                     # 自己编辑

[markup.highlight]
guessSyntax = 'true'
noClasses = 'false'

[markup.goldmark.extensions.passthrough]
enable = 'true'
delimiters.block = [["\\[", "\\]"], ["$$", "$$"]]
delimiters.inline = [["\\(", "\\)"], ["$", "$"]]

[outputs]
home = ["Algolia", "HTML", "RSS"]

[outputFormats.Algolia]
baseName = "algolia"
isPlainText = 'true'
mediaType = "application/json"
notAlternative = 'true'

[markup]
  [markup.tableOfContents]
    endLevel = 4
    ordered = 'true'
    startLevel = 1
```

10. In the address bar of /blog/blog, type cmd to open the command prompt. Type `hugo server -D` to start the blog. After the address appears, press Ctrl + click to enter. At this point, the browser should successfully display the theme example interface. The blog setup is now complete.

## 3. Theme Settings (Optional Reading)

### 3.1 Multi-language i18n Configuration

1. Open /blog/blog/config/_default/params.yml, customize the name and url configurations, and save after modification.

2. Open the corresponding language .yml file in the /blog/blog/i18n folder. Open several and modify the corresponding parts accordingly.

[Assuming I have set three languages ​​in the above hugo.toml: Simplified Chinese, English, and Japanese, I will now configure i18n for these three languages.]

The following is sample code:

```params.yml
# menu part
menu:
  - name: home
    url: ""
  - name: archives
    url: "archives"
  - name: about
    url: "about"
  - name: link
    url: "link"
```
```en.yml
# menu only
home: Home
about: About
link: Link
archives: Archives
```
```zh-CN.yml
# menu only
home: 首页
about: 关于
link: 更多
archives: 归档
```
```ja.yml
# menu only
home: ホーム
about: プロフィール
link: リンク
archives: アーカイブ
```

After modifying the code above, you can try running it and see that the multilingual functionality works correctly.
### 3.2 Core Settings

This section will explain the core configuration file for this theme, params.yml, analyzing the code segment by segment to help you complete the configuration smoothly.

After navigating to /blog/blog/config/_default/params.yml, please follow the instructions below to customize the settings.

The code is quite long; please read it carefully before proceeding. The comments in both Chinese and English are very detailed; be sure to read them for accurate configuration!

                                                                                                Click below 👇 to expand
```params.yml
menu:                                  # 此部分设置菜单文字及图标，前面已有教程说明如何配置此板块
  - name: home
    url: ""
    icon: 'xxx'                       # 可前往 https://github.com/D-Sketon/hexo-theme-reimu/issues/30 选择想要的图标，注意应选iconfont列而非fontawesome列
  - name: archives
    url: "sort"
    icon: 'xxx'
  - name: about
    url: "about"
    icon: 'xxx'
  - name: link
    url: "link"
    icon: 'xxx'

mainSections: ["post"]                 # 此栏为时间的显示格式，可不改
yearFormat: "2006"
monthFormat: "2006-01"
dateFormat: "2006-01-02"
timeFormat: "2006-01-02 15:04:05"

author: xxx                            #设置作者，此栏显示在主页头像下方
email: xxx@example.com                 #设置邮箱，此栏不显示
description: "xxxxxxxxxxxxxxxxxxx"     #设置描述，此栏显示在主页作者下方
# subtitle: "少女祈祷中..."              #设置副标题，若下方启用则此处保持注释状态
subtitle:
  typing:
    enable: true                       #启动打字动画，此栏显示在标题下方
    strings:                           #若启用需删除 - 前的#，下方为该动画的配置
      # - 句子1
      # - 句子2
      # - 句子3
      # - 句子4
    typeSpeed: 100              # 打字速度（毫秒/字符） 
    backSpeed: 50               # 删除速度（毫秒/字符）
    backDelay: 2000             # 打完一句话后，等待时间
    startDelay: 300             # 页面加载后，等待时间
    loop: true                  # 是否循环播放
    shuffle: true               # 是否随机输出句子
    showCursor: true            # 是否显示闪烁的字符
    cursorChar: "|"             # 字符
    smartBackspace: true        # 智能退格，只删除不同的部分
  text: "xxxxxxxxxxxxx"         # 当 typing.enable = false 时使用

banner: "https://example.com"   # 或 banner: "/image/banner.png"，若为图片API 使用默认语句，本地图片则使用本栏语句

banner_srcset:                  #设置本地背景图，该设置可让背景图在以下图片中随机显示
  enable: false
  srcset:
    - src: "images/banner-600w.webp"
      media: "(max-width: 479px)"
    - src: "images/banner-800w.webp"
      media: "(max-width: 799px)"
    - src: "images/banner.webp"
      media: "(min-width: 800px)"

avatar: "avatar.png"             #设置头像，此栏显示在主页头像处

# Control the display of the post cover
# If not set, the banner image will be displayed by default
# Its priority is lower than the cover in the Front-matter
cover: # https://example.com / false / rgb(255,117,117)

# Control the display of the post toc
# Its priority is lower than the toc in the Front-matter
toc: true

# Open Graph
open_graph:
  enable: true
  options:
    #twitter_card: <twitter:card>
    #twitter_id: <twitter:creator>
    #twitter_site: <twitter:site>
    #twitter_image: <twitter:image>
    #google_plus: <g+:profile_link>
    #fb_admins: <fb:admin_id>
    #fb_app_id: <fb:app_id>

# Content
excerpt_link: Read More

# Footer copyright
# Inject code snippet right in the footer copyright
# Make sure your code snippet is safeHTML
copyright:
# Need help choosing? Please see...
# https://creativecommons.org/choose/
# https://choosealicense.com/
# copyright: |-
#   <div style="flex-direction:column;align-items: center;"><a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a>
#   All website licensed under <a href="https://creativecommons.org/licenses/by/4.0/" target="_blank">CC BY 4.0</a></div>

footer:                            #设置页尾，此栏显示在主页最下方
  since: 2025 # 2020-current year
  powered: true
  count: true
  busuanzi: false
  icon:
    url: "../images/taichi.png"     # 若不设置则为默认图片
    rotate: true
    mask: true # whether to use the images as a mask

sidebar:                            #设置侧边栏，此栏显示在主页侧边栏处
  position: left
  menu: true  # 侧边栏菜单
  article:
    show_common: true               # 侧边栏最新文章栏处

social:                            #设置社交方式，若启用需删除#
  # email: xxx:xxx@example.com
  # github: https://github.com/xx
  # google: https://plus.google.com/yourname
  # twitter: https://twitter.com/yourname
  # facebook: https://www.facebook.com/yourname
  # instagram: https://www.instagram.com/yourname
  # linkedin: https://www.linkedin.com/in/yourname
  # pinterest: https://www.pinterest.com/yourname
  # youtube: https://www.youtube.com/channel/yourname
  # vimeo: https://vimeo.com/yourname
  # flickr: https://www.flickr.com/photos/yourname
  # dribbble: https://dribbble.com/yourname
  # behance: https://www.behance.net/yourname
  # bilibili: https://space.bilibili.com/xx
  # weibo: https://weibo.com/yourname
  # zhihu: https://www.zhihu.com/people/yourname
  # reddit: https://www.reddit.com/user/yourname
  # tumblr: https://yourname.tumblr.com
  # medium: https://medium.com/@yourname
  # deviantart: https://yourname.deviantart.com
  # stackoverflow: https://stackoverflow.com/users/yourname
  # keybase: https://keybase.io/yourname
  # telegram: https://t.me/xx
  # discord: https://discordapp.com/users/yourname
  # steam: https://steamcommunity.com/id/yourname

widgets:                            #设置，此栏显示在侧边栏描述下方，此栏尽量不要改
  - category
  - tag
  - tagcloud
  - recent_posts

# Widget behavior                   #设置，设置上方栏目行为
category_limits: 10
tag_limits: 10
recent_posts_limits: 5
tagcloud_limits: 20

# Archive behavior
only_show_capsule_in_index: false # If you have hugo amounts of tags and categories, you can set this to true to only show the capsule in the index page for better performance
uppercase_capsule: true # If you want to keep taxonomic capsule unchanged, please set this to false

show_update_time: false # If you want to show the update time, please set this to true

# Summary content
summary:
  enable: false
  style: 'subtitle' # 'subtitle' or 'blockquote'

# RSS output
rss:
  limit: 10             # The number of recent articles to be output, write -1 to output all
  showFullContent: false # output full content or description
  showCopyright: false   # If true, add copyright to the end of article.

# Sort order configuration
# Available values: default, date, date-reverse, weight, weight-reverse
# default: hugo's default sort order for page collections, see https://gohugo.io/quick-reference/page-collections/#sort
# date: sorted by date in ascending order (oldest first)
# date-reverse: sorted by date in descending order (newest first)
# weight: sorted by weight in ascending order
# weight-reverse: sorted by weight in descending order
sort_order:
  taxonomy:
    category: date-reverse # controlled by categories_weight
    tag: date-reverse # controlled by tags_weight
  archive: date-reverse # controlled by weight
  home: default # controlled by weight

paginate:                            #设置每页文章数，将xx替换为数值即可，注意保留后方空格，否则报错
  archive: xx # Number of posts per page in archive and taxonomy pages
  post: xx # Number of posts per page in home and other list pages

########################################
# CSS
########################################

layout:
  max_width: 1350px # the max width of the main content area

triangle_badge:                          # 设置页面右上角三角标
  enable: false
  icon: github # same as the icon in the social config
  link: https://github.com/D-Sketon/hugo-theme-reimu

anchor_icon: # default use '#' icon, you can use a hexadecimal representation of fontawesome or icon_font, like 'f0c1', you can also use false to hide anchor icon

reimu_cursor:                            #设置鼠标图标，若自定义请自行准备图片，建议像素32 X 32
  enable: true
  cursor:
    default: ../images/cursor/default.png  # this path is relative to the css/main.css, so it needs to go up one level to reach the images folder
    pointer: ../images/cursor/pointer.png
    text: ../images/cursor/text.png

icon_font: 4552607_4k4bc36ef96            #设置菜单图标，此栏勿改

# Font loading strategy
# Custom Font -> Google Fonts -> Local FallBack Font

# Custom Font
custom_font:                            #设置字体，若自定义请自行准备字体css文件
  enable: false
  article:
    # - css: https://fontsapi.zeoseven.com/292/main/result.css # font css
    #   name: LXGW WenKai # font name
  code:

# https://fonts.google.com/
# Google Fonts, higher priority than local_font
font:                                   #设置字体，选用google字体，若自定义请自行准备字体文件
  enable: true
  article:
    - Mulish
    - Noto Serif SC
  code:
    # - Ubuntu Mono
    # - Source Code Pro
    # - JetBrains Mono

# Local FallBack Font
local_font:                            #设置字体，选用本地字体文件，若自定义请自行准备字体文件
  article:
    - "-apple-system"
    - PingFang SC
    - Microsoft YaHei
    - sans-serif
  code:
    - Menlo
    - Monaco
    - Consolas
    - monospace

dark_mode:                            #设置明暗主题，下方enable自选
  # true means that the dark mode is enabled by default
  # false means that the dark mode is disabled by default
  # auto means that the dark mode is automatically switched according to the system settings
  enable: auto # true | false | auto

########################################
# Analytics
########################################

baidu_analytics: false                 #设置分析
google_analytics: false
clarity: false

########################################
# Markdown Display
########################################

# mermaid url https://github.com/mermaid-js/mermaid
mermaid:
  zoom: true # whether to enable zoom for mermaid diagrams

code_block:                            #设置代码块启用，用于写文章
  # whether to expand the code block by default
  # true means expand all code blocks by default
  # false means collapse all code blocks by default
  # number means collapse the code block by default when the number of lines exceeds the specified value
  expand: true

# Clipboard configuration
clipboard:                            #设置粘贴板显示效果
  success: 
    en: Copy successfully (*^▽^*)
    zh-CN: 复制成功 (*^▽^*)
    zh-TW: 複製成功 (*^▽^*)
    ja: コピー成功 (*^▽^*)
  fail: 
    en: Copy failed (ﾟ⊿ﾟ)ﾂ
    zh-CN: 复制失败 (ﾟ⊿ﾟ)ﾂ
    zh-TW: 複製失敗 (ﾟ⊿ﾟ)ﾂ
    ja: コピー失敗 (ﾟ⊿ﾟ)ﾂ
  copyright:
    enable: false
    count: 50 # The number of characters when the copyright is displayed
    license_type: by-nc-sa # https://creativecommons.org/licenses

math:                                 #设置启用数学公式
  katex:
    enable: true
  mathjax:
    enable: false
    options: # see https://docs.mathjax.org/en/latest/web/configuration.html
    # we need to put the configuration in an array, because hugo will automatically convert the key to lowercase
      [
        {
          tex:
            {
              tags: "ams",
              useLabelIds: true,
              inlineMath: [["$", "$"], ['\\(', '\\)']],
              displayMath: [["$$", "$$"], ['\\[', '\\]']],
              processEscapes: true,
              processEnvironments: true,
              autoload: { color: [], colorv2: ["color"] },
              packages: { "[+]": ["noerrors"] },
            },
          options:
            {
              skipHtmlTags:
                ["script", "noscript", "style", "textarea", "pre", "code"],
              ignoreHtmlClass: "tex2jax_ignore",
              processHtmlClass: "tex2jax_process",
            },
          loader: { load: ["input/asciimath", "[tex]/noerrors"] },
        },
      ]

########################################
# 下方为评论系统的配置，请仔细阅读代码后配置
########################################

comment:                      # comment system title
  title:
    en: Leave a comment
    zh-CN: 说些什么吧！
    zh-TW: 說些什麼吧！
    ja: コメントを残す
  default: waline             # default comment system, when you enable multiple comment systems

# valine comment system. https://valine.js.org
valine:
  enable: false # 启用填 true
  appId: # 填写 app id
  appKey: # 填写 app key
  pageSize: 10 # comment list page size
  avatar: mp # gravatar style https://valine.js.org/#/avatar
  # lang: zh-cn # deprecated, use html.lang instead
  placeholder: Just go go # valine comment input placeholder(like: Please leave your footprints )
  guest_info: nick,mail,link #valine comment header info
  recordIP: true # whether to record the IP address of the commenters
  highlight: true # whether to highlight the code blocks
  visitor: false # whether to display the number of visitors
  serverURLs: # leancloud server url

# https://waline.js.org/
waline:
  enable: false
  serverURL:
  # lang: zh-CN # deprecated, use html.lang instead
  locale: {} # https://waline.js.org/guide/features/i18n.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%AF%AD%E8%A8%80
  emoji:
    - https://unpkg.com/@waline/emojis@1.2.0/weibo
    - https://unpkg.com/@waline/emojis@1.2.0/alus
    - https://unpkg.com/@waline/emojis@1.2.0/bilibili
    - https://unpkg.com/@waline/emojis@1.2.0/qq
    - https://unpkg.com/@waline/emojis@1.2.0/tieba
    - https://unpkg.com/@waline/emojis@1.2.0/tw-emoji
  meta:
    - nick
    - mail
    - link
  requiredMeta:
    - nick
    - mail
  wordLimit: 0
  pageSize: 10
  pageview: true

# https://twikoo.js.org
twikoo:
  enable: true
  envId: https://xxx.vercel.app # 腾讯云环境填 envId；Vercel 环境填地址（https://xxx.vercel.app）
  region:

# https://github.com/gitalk/gitalk/blob/master/readme-cn.md
gitalk:
  enable: false
  clientID:
  clientSecret:
  repo:
  owner:
  admin:
  md5: false

# https://giscus.app/zh-CN
giscus:
  enable: false
  repo:
  repoId:
  category:
  categoryId:
  mapping: mapping
  strict: 0
  reactionsEnabled: 1
  emitMetadata: 0
  inputPosition: bottom
  # commentTheme: preferred_color_scheme invalid
  # lang: zh-CN # deprecated, use html.lang instead

# https://disqus.com
disqus:
  enable: false
  shortname: # your disqus shortname
  count: true

# https://utteranc.es
utterances:
  enable: false
  repo: owner/repo # Change this to "Your GitHub Username/The Repository Name" used for storing blog comments
  issue_term: title
  theme: auto # auto means to automatically adapt to dark and light themes, you can also use specific themes like github-light, github-dark, preferred-color-scheme, etc.

########################################
# Search
########################################

algolia_search:
  enable: true
  appID: xxx
  apiKey: xxxxxxxxxxxxxxxxxxxxxxxxx
  indexName: 'xxx'
  hits:
    per_page: 20

preloader:                            #设置预加载界面
  enable: true
  text: 
    zh-CN: 少女祈祷中...
    zh-TW: 少女祈禱中...
    en: Loading...
    ja: 少女祈祷中...
  icon: #  '/images/taichi.png' 或图片API 'https://xxxxx.com'
  rotate: true # 旋转图标

# see https://github.com/D-Sketon/aos.js
animation:                            #设置整体动画效果
  enable: true
  options:
    header:
      title: slide-up
      subTitle: slide-down
    home:
      post: fade-up
      widget: fade-up
      sidebar: fade-up
    article:
      whole: fade-up
      date: zoom-in
      category: zoom-in
      tag: zoom-in
      comment: zoom-in
      reading: zoom-in
      nav: fade-up
    archive:
      whole: fade-up
      tag: zoom-in
      category: zoom-in
      section: fade-up
      nav: fade-up

# see https://github.com/D-Sketon/mouse-firework
firework:                            #设置点击时的烟花效果
  enable: true
  disable_on_mobile: false
  options:
    excludeElements: ["a", "button"]
    particles:
      - shape: circle
        move: ["emit"]
        easing: easeOutExpo
        colors: ["var(--red-1)", "var(--red-2)", "var(--red-3)", "var(--red-4)"]
        number: 20
        duration: [1200, 1800]
        shapeOptions:
          radius: [16, 32]
          alpha: [0.3, 0.5]
      - shape: circle
        move: ["diffuse"]
        easing: easeOutExpo
        colors: ["var(--red-0)"]
        number: 1
        duration: [1200, 1800]
        shapeOptions:
          radius: 20
          alpha: [0.2, 0.5]
          lineWidth: 6

article_copyright:                            #设置版权信息，显示在文章末尾
  enable: true
  content:
    author: true
    link: true
    title: true
    date: true
    updated: false
    license: true
    license_type: by-nc-sa # https://creativecommons.org/licenses

# Back To Top
top:                                          #设置 返回顶部 按钮配置
  enable: true
  position: right # left or right
  icon:
    url: "../images/2.png" # 配置图标
    rotate: true
    mask: true # whether to use the images as a mask

outdate:                                      #设置 文章最后更新于xxx天前，可能不适用 效果
  enable: false
  daysAgo: 180 # The number of days after which the article is considered outdated
  message:
    en: This article was last updated on {time}. Please note that the content may no longer be applicable.
    zh-CN: 本文最后更新于 {time}，请注意文中内容可能已不适用。
    zh-TW: 本文最後更新於 {time}，請注意文中內容可能已不適用。
    ja: この記事は最終更新日：{time}。記載内容が現在有効でない可能性がありますのでご注意ください。

# ICP 备案
icp:
  icpnumber: # ICP备案号
  beian: # 网安备案号
  recordcode: # 网安备案链接中的recordcode参数

# 萌国 ICP 备案
moe_icp:
  icpnumber: # 萌国ICP备案号

# 赞助
sponsor:
  enable: false
  tip: 
    zh-CN: 请作者喝杯咖啡吧
    zh-TW: 請作者喝杯咖啡吧
    en: Buy me a coffee
    ja: コーヒーを買ってください
    pt-BR: Compre-me um café
  icon:
    url: "../images/3.png" # this path is relative to the css/main.css, so it needs to go up one level to reach the images folder
    rotate: true
    mask: true # whether to use the images as a mask
  qr:
    # - name: 支付宝
    #   src: "sponsor/alipay.jpg"
    # - name: 微信
    #   src: "sponsor/wechat.png"

# Share
share:
   - facebook
   - twitter
   - linkedin
   - reddit
   - weibo
   - qq
   - weixin

# 设置目录卡片
home_categories:
  enable: true
  content:
    - categories: '' # string (single-layer category) or array (multi-layer category)
      cover: 'https://xxx.com' # 目录图片，空则随机图片
    - categories:
      cover:

########################################
# Experimental features
########################################

# 代码注入器
injector:
  head_begin: # Inject code snippet right after <head>
  head_end: # Inject code snippet right before </head>
  body_begin: # Inject code snippet right after <body>
  body_end: # Inject code snippet right before </body>
  sidebar_begin: # Inject code snippet right after <aside>
  sidebar_end: # Inject code snippet right before </aside>

# Experimental, may have a lot of bugs, open with caution!
pjax:                                 #设置加速网页显示速度
  enable: true

# Experimental
# https://github.com/GoogleChromeLabs/quicklink
quicklink:                            #设置提前加载链接，利于跳转更快
  enable: true
  # The `requestIdleCallback` timeout, in milliseconds.
  timeout: 3000
  # Whether or not the URLs within the options.el container should be treated as high priority.
  # When true, quicklink will attempt to use the fetch() API if supported (rather than link[rel=prefetch]).
  priority: true
  # Determine if a URL should be prefetched.
  # Only support string
  ignores: []

# Experimental
service_worker:
  enable: false

#下方live2d和live2d_widgets只能开后者，前者无反应
# Experimental
live2d:
  enable: false
  position: right # left or right

# Experimental
live2d_widgets:
  enable: true
  position: right # left or right

# https://github.com/CodeByZach/pace
pace:
  enable: true

# 音乐播放器，现为完全开启状态，禁用则将aplayer或meting任一设置为false即可
player:
  disable_on_mobile: true
  position: before_sidebar # before_sidebar | after_sidebar | after_widget
  # if you enable meting, you must enable aplayer first
  aplayer:
    # 下方配置请前往 Aplayer官方中文文档： https://aplayer.js.org/#/zh-Hans/?id=%E5%8F%82%E6%95%B0 查看
    enable: true
    options:
      audio: []
      fixed: true
      autoplay:
      loop:
      order:
      preload:
      volume:
      mutex:
      listFolded:
      lrcType:
  meting:
    # https://github.com/metowolf/MetingJS
    enable: true
    meting_api: # custom api
    options:
      id: xxxxx
      server: netease
      type: playlist
      auto: true

########################################
# pangu.js
########################################

pangu:
  # more information: https://github.com/vinta/pangu.js 
  enable: false  # enable pangu.js to add space between Chinese and English

########################################
# Theme
########################################

# experimental, may have a lot of bugs, open with caution!
# A dynamic color generation tool based on Google's Material You design guidelines, capable of extracting primary colors from any image and generating complete light and dark color schemes.
material_theme:
  # more information: https://github.com/2061360308/material-theme
  # notice: when you enable this feature, all the covers will be automatically added "crossorigin" attribute to support the dynamic color scheme
  # so make sure your custom covers will not be blocked by the browser's CORS policy
  enable: false # enable material_theme to generate dynamic color schemes based on the banner image

internal_theme:                            #设置主题强调色
  light:
    --red-0: '#ffb7c5'
    --red-1: '#ffb7c2'
    --red-2: '#ff7c7c'
    --red-3: '#ffafaf'
    --red-4: '#ffd0d0'
    --red-5: '#ffecec'
    --red-5-5: '#fff3f3'
    --red-6: '#fff7f7'
    --color-red-6-shadow: 'rgba(255, 78, 78, 0.6)'
    --color-red-3-shadow: 'rgba(255, 78, 78, 0.3)'

    --highlight-nav: "#f5f5f5"
    --highlight-scrollbar: "#d6d6d6"
    --highlight-background: "#fdfdfd"
    --highlight-selection: "#e9e9e988"
    --highlight-foreground: "#24292e"
    --highlight-comment: "#7d7d7d"
    --highlight-red: "#d73a49"
    --highlight-orange: "#e36209"
    --highlight-yellow: "#cb911d"
    --highlight-green: "#22863a"
    --highlight-aqua: "#005cc5"
    --highlight-blue: "#032f62"
    --highlight-purple: "#6f42c1"
    --highlight-deletion: "#b31d28"
    --highlight-deletion-bg: "#ffeef0"
    --highlight-addition: "#22863a"
    --highlight-addition-bg: "#f0fff4"
  dark:
    --red-4: 'rgba(255, 208, 208, 0.5)'
    --red-5: 'rgba(255,228,228,0.15)'
    --red-5-5: 'rgba(255,236,236,0.05)'
    --red-6: 'rgba(255, 243, 243, 0.2)'

    --highlight-nav: "#222830"
    --highlight-scrollbar: "#454d59"
    --highlight-background: "#1e2027"
    --highlight-selection: "#51515155"
    --highlight-foreground: "#c9d1d9"
    --highlight-comment: "#8b949e"
    --highlight-red: "#ff7b72"
    --highlight-orange: "#ffa657"
    --highlight-yellow: "#ffcc66"
    --highlight-green: "#7ee787"
    --highlight-aqua: "#a5d6ff"
    --highlight-blue: "#79c0ff"
    --highlight-purple: "#d2a8ff"
    --highlight-deletion: "#ffa198"
    --highlight-deletion-bg: "#490202"
    --highlight-addition: "#7ee787"
    --highlight-addition-bg: "#04260f"

```
### 3.3 How to Write an Article Page

1. Open a command prompt in the address bar of /blog/blog and type `hugo new content post/blog1/index.md`, or create a new folder named `blog1` within the `/blog/blog/content` folder, and create a new file named `index.md` within the `blog1` folder. Open the file; if you need to use the shortcode feature, please see section 4.3 below.

2. Please copy the following code as needed. **The two code snippets have different uses; choose the one that suits your needs.**
```Article Example 1.md
# Articles only
+++
data = '2026-01-01T09:00:00+09:00'
weight = 1
+++
balabalabalabalabalabalabalabalabalabalabalabala
```

```Article Example 2.md
# Articles, Tags, and Categories
---
data: '2026-01-01T09:00:00+09:00'
weight: 1
tags:
  - tag1
  - tag2
categories:
  - content1
  - content2
---
balabalabalabalabalabalabalabalabalabalabalabala
```

### 3.4 Using Shortcodes
Sometimes, to add more functionality to your webpage, you might need to use richer code. However, the Hugo framework has limitations in certain areas. But for user convenience, a backdoor is provided: shortcodes.

To use the corresponding code, please remove spaces such as between !{, between two lines, or between {{) to ensure the code runs.

The code has been confirmed to work during writing. If it doesn't, simply adjust the spaces in the code.

#### heatMapCard Article Heatmap
This card can only be displayed at the beginning of the **article page**. It cannot be displayed on the homepage or elsewhere!

To view the heatmap display effect, please return to the beginning of the article!

To use this card on the article page, refer to the code below, such as:

```Article Page.md

{ {< heatMapCard levelStandard="?" >} }

{{< heatMapCard levelStandard="?" >}}

```
#### Friends Link Card

If the content contains a friend.md file, refer to the code below, such as:

```Article Page.md

{ {< friendsLink >} }

{{< friendsLink >}}

```
#### TagRoulette

This card can only be displayed on the article page.

To use this card, refer to the code below and customize the tags and icon.

Usage: Clicking the icon will randomly display a tag.

For example:

```Article Page.md

{ {< tagRoulette tags="tag1,tag2,tag3" icon="🎲" >} }

{{< tagRoulette tags="tag1,tag2,tag3" icon="🎲" >}}

```
#### alertBlockquote Block Reference

This card can only be displayed on the article page.

To use this card on the article page, refer to the code below, such as:

```Article page.md

{ {< alertBlockquote type="0721" >}}

Ciallo～(∠・ω< )⌒★

{ {</alertBlockquote>} }

{{< alertBlockquote type="0721" >}}
Ciallo～(∠・ω< )⌒★
{{</alertBlockquote>}}

Alternatively, you can use similar modules: note, tips, important, warning, etc. Other modules are similar, such as:

{ {< alertBlockquote type="note" >} }
Ayachi Nene is coming~

{ {< /alertBlockquote >} }

{{< alertBlockquote type="note" >}}
Ayachi Nene is Coming~
{{< /alertBlockquote >}}

```
#### link Link Card

This card can only be displayed on article pages.

To use this card on an article page, refer to the code below, such as:

```Article Page.md

{ {< link title="0721" link="https://ciallo.cc" cover="auto" escape="true" >} }

{{< link title="0721" link="https://ciallo.cc" cover="auto" escape="true" >}} or

{ {< link title="0721" path="https://ciallo.cc" cover="auto" escape="true" >} }

{{< link title="0721" path="https://ciallo.cc" cover="auto" escape="true" >}}

```
#### gallery Photo Wall

This card can only be displayed on article pages.

To use this card on an article page, refer to the code below, such as:

```Article Page.md
{ {< gallery >} }

! [Figure 1] (https://xxx.com/xxx.webp)

! [Figure 2] (https://xxx.com/xxx.webp)

...
{ {</gallery>} }
{{< gallery >}}
![Figure 1](https://tc.alcy.cc/tc/20260121/2c785c4a015e858d9d470d51ca702a1a.webp)
![Figure 2](https://tc.alcy.cc/tc/20260121/6c4e58cf6f6ce1cc144f834ba98d22fa.webp)
...
{{</gallery>}}

```
#### grid Grid Layout

This card can only be displayed on article pages.

To use this card on an article page, refer to the code below, such as:

```Article Page.md

{ {< grid width=300 col=3 >} }

<!-- cell -->

07211

<!-- cell -->

07212

<!-- cell -->

07213

{ {< /grid >} }

Display Effect:

{{< grid width=300 col=3 >}}
<!-- cell -->
07211
<!-- cell -->
07212
<!-- cell -->
07213
{{< /grid >}}

```
#### Details Collapsed Panel

This card can only be displayed on article pages.

To use this card on an article page, refer to the code below, such as:

```Article Page.md

{ {< details summary="0721" >} }

Ciallo～(∠・ω< )⌒★

{ {< /details >} }
{{< details summary="0721" >}}
Ciallo～(∠・ω< )⌒★
{{< /details >}}
```
## 4. Blog Deployment
### 4.1 Standard Deployment (**Required for first-time use**)

1. Log in to your GitHub account. Create a new repository at https://github.com/example?tab=repositories. Name the repository example.github.io/blog.

2. Open a command prompt in the address bar of the /blog/blog/public folder and enter the following code:

```
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/example/blog.git   # Remember to change
git push -u origin main                                     # If it fails, change -u to -f

```

3. After the progress reaches 100%, refresh the GitHub page. You should now see the running repository. Click Settings, then Pages, select main in the Branch section, and then click Save.

4. Wait a few minutes, then refresh. You should now see the address on this page, such as `Your site is live at https://example.github.io/blog/ indicates successful deployment`.

{{<details summary="Want to use a different domain?" >}}
If you want to use a different domain name, the repository name **must** be `example.github.io`. The following configuration uses Cloudflare and Huawei Cloud as examples; the configuration for other domain service providers may differ.

Domain Configuration Method:

1. Complete the main domain name resolution in Cloudflare. For example, if you have a main domain name resolved in Cloudflare such as example.com, decide which domain name you want to use for your blog before performing the following operations, such as `blog.example.com`. Note that this should be a top-level domain or a second-level domain; otherwise, it will not be able to be bound to Huawei Cloud later.

**Correction**: If you use a free domain name such as .dpdns.org or .cc.wt, it **will not be recognized as a usable domain name in Huawei Cloud**.

2. MPlease ensure that the international interface is displayed when you open the [Huawei Cloud](https://www.huaweicloud.com/intl/en-us/) website.Then register an account, and register with your email address. If you are required to verify your login during the process, select "I understand" and then "Do not enable for now." Skip any requests to bind your mobile phone number! !

3. After entering the console, click "Public Domains" in the "My Resources" section. Add the domain name you just decided on in step 1. After successfully adding it, configure it in Cloudflare and Huawei Cloud respectively according to the template below:

Cloudflare Configuration:

| Type | Name | Nameserver | TTL |
| :---: | :---: | :---: | :---: |
| NS | blog | ns1.huaweicloud-dns.org | Auto |
| NS | blog | ns1.huaweicloud-dns.net | Auto |
| NS | blog | ns1.huaweicloud-dns.com | Auto |
| NS | blog | ns1.huaweicloud-dns.cn | Auto |

Huawei Cloud Configuration: Click "Add Recordset," fill in the following information, and confirm:

| Type | Name | Line | TTL (s) | Value |
| :---: | :---: | :---: | :---: | :---: |
| CNAME | Leave blank | Default for all networks | 300 | Github repository name |

6. In Github's Settings - Pages page, scroll down to find Custom domain, enter the domain name, click Save, and then **make sure to check** "Enforce HTTPS" (if you click Save and Enforce HTTPS is grayed out and unchecked, there's an error; go back and check). Wait for it to take effect.

7. After this configuration is complete, you can access the blog by visiting the domain `blog.example.com`.
{{< /details >}}

### 4.2 Automated Deployment (**Initial deployment completed, subsequent code updates required**)

1. Create a new file `.gitignore` in `/blog/blog`. Open the file, copy the following content, and save it:

```.gitignore
public
resources
.hugo_build.lock
hugo.exe
```

2. Create a `.github` folder inside `/blog/blog`. Inside the `.github` folder, create a `workflows` folder. Inside the `workflows` folder, create a new file `hugo_deploy.yaml`. Copy the following code into the file and save it:

```hugo_deploy.yaml
name: deploy

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
        - name: Checkout
          uses: actions/checkout@v4
          with:
              fetch-depth: 0

        - name: Setup Hugo
          uses: peaceiris/actions-hugo@v3
          with:
              hugo-version: "latest"
              extended: true

        - name: Build Web
          run: hugo -D

        - name: Deploy Web
          uses: peaceiris/actions-gh-pages@v4
          with:
              PERSONAL_TOKEN: ${{ secrets.TOKEN }}
              EXTERNAL_REPOSITORY: [your github name/Your warehouse name]
              PUBLISH_BRANCH: main
              PUBLISH_DIR: ./public
              commit_message: auto deploy

```

3. In the repository interface, click your avatar, click Settings, scroll down to the bottom of the **sidebar**, click Developer settings, click Personal access tokens, click the displayed Token (classic), click Generate new token, click Generate new Token (Classic)

4. Verify User. Optional input: Note. For Expiration, select "no expiration." In Select scopes, check "All repo" and "Workflow." Scroll to the bottom and click "Generate token." **Very important!** Be sure to copy and save the generated key; it will only be displayed once!

5. Return to the created repository page, click Settings, scroll down, find Secrets and variables under Security in the sidebar, and click Actions.

6. Under Repository secrets, click New repository secret, fill in the template below, and click Add secret after completion.

```
Name*
TOKEN

Secret*
ghp_xxxxxxxxxxxxxxxxxxxxxxxx                 # Paste the key generated in step 4 here.
```

7. In the address bar of the /blog/blog folder, type cmd to open the command line, and enter the following code. You may be prompted to verify your GitHub account; just follow the prompts. To ensure successful upload, please keep a proxy running.

```
git add .
git commit -m "update"
git push -u origin main                     # If it fails, change -u to -f
```

8. Return to the Github interface, click Actions. When you see the current two workflows (displayed as workflow on the webpage) running successfully with green checkmarks, click Settings, click Pages, select main in the Branch section, and finally click... Save

9. Wait a few minutes and refresh. You can view the blog when the Pages page displays the address.