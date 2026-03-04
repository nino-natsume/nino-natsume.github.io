---
date: '2026-02-28T11:00:00+09:00'
title: 'Hugoウェブサイト構築プロセス'
weight: 1
categories:
  - 次元星域
tags:
  - 次元星域
  - Hugo
  - チュートリアル
---
{{< heatMapCard levelStandard="200,700,1000" >}}
# はじめに
このチュートリアル専用のブログを作成したくなかったので、この記事で全てを詳しく説明し、できる限りスムーズに設定できるようにしたいと思います。

この記事では、Hugo フレームワークと hugo-theme-reimu テーマを使用します。作成、設定、デプロイまで、1 つの記事でわかりやすく説明しています。他のテーマについては、それぞれの公式ドキュメントを参照してください。

## **記事の理解と設定手順:**
この記事の理解を深めるために、以下のチュートリアルのどの部分がどのフォルダーに対応しているかを理解するため、以下の説明を読むことを強くお勧めします。

| フォルダーまたはファイル | 意味 |
| :----: | :----: |
| /blog | 初期フォルダー |
| /blog/blog | ブログディレクトリ。カスタマイズする場合は、/blog/0721 のように適宜変更してください。
| /blog/blog/xxx | ブログディレクトリ内の対応するパスにあるファイルまたはフォルダー |
| /theme/hugo-theme-reimu/xxx | テーマフォルダ内の該当パスにあるファイルまたはフォルダ |

## 事前の注意事項:
1. 私はテーマの作者ではありません。これは個人的な導入手順の説明です。

2. この記事はすべてテキストベースです。ご質問がある場合は、下記にコメントを残すか、info@natsume.xin までご連絡ください。

(以下はチュートリアルの本文です)

# Hugo 個人ブログ 完全セットアップチュートリアル
## 1. 環境設定
### 1.1 Git のダウンロード
1. [Git 公式サイト](https://git-scm.com/) にアクセスし、インストーラーをダウンロードします。

2. 「次へ」をクリックし続けます。デフォルトのインストールで問題ありません。オプションの意味や機能がわからない場合は、変更しないでください。

### 1.2 Hugo のダウンロード
1. Hugo の公式 Github ページ (https://github.com/gohugoio/hugo/tags) にアクセスし、最新バージョンの中から最初のものを選択してダウンロードし、解凍します。

2. 上記のソースコードは Windows 用の最新バージョンです。`withdeploy` が含まれているものが最適です。

### 1.3 テーマのダウンロード
1. Hugo の公式テーマ Reimu ページ (https://github.com/D-Sketon/hugo-theme-reimu/tags) にアクセスし、同じく最新バージョンの中から最初のものを選択します。

2. ソースコードをダウンロードしたら解凍し、ファイル名の後のバージョン番号を削除して `hugo-theme-reimu` だけを残します。テーマフォルダを編集し、別の場所に保存します。
## 2. ブログのデプロイ
### 2.1 ブログの作成
1. `/blog` に移動し、フォルダのアドレスバーに `cmd` と入力してコマンドラインを開きます。

2. `hugo new site blog` と入力して、Hugo ブログのメインファイルを作成します。

3. `cd blog` と入力して、親フォルダに移動します。hugo.exe をブログにコピーします。この時点で、/blog フォルダ内のファイルパスは以下のようになります。
```blog/
blog/
|- blog/
| |-archetypes/
| |-assets/
| |-content/
| |-data/
| |-i18n/
| |-layouts/
| |-static/
| |-themes/
| |-hugo.toml
|- hugo.exe
|- LICENSE
|- README.md

```

4. `hugo server -D` と入力してブログを起動します。`http://localhost:1313` が表示されたら、Ctrl キーを押しながらアドレスをクリックしてアクセスします。この時点でブラウザに「ページが見つかりません」と表示され、ブログサービスが正常に起動したことを示します。

5. Ctrl キーを押しながら C キーを押して終了します。そうしないと、以降の操作や保存後にブラウザにエラーメッセージが表示されます。
### 2.2 初期設定
テーマをスムーズに動作させるには、以下の手順をすべて実行することをお勧めします。

1. `/blog/blog` 内に `config` というフォルダを作成し、さらに `config` 内に `_default` というフォルダを作成します。現在のパスは `/blog/blog/config/_default/` です。

2. 手順 1.3 で作成したテーマフォルダを `/blog/blog/theme` にコピーまたはドラッグします。現在のパスは `/blog/blog/theme/hugo-theme-reimu/` です。

3. `theme/hugo-theme-reimu/config/_default/params.yml` を `/blog/blog/config/_default` にコピーします。

4. `theme/hugo-theme-reimu/data` にあるすべてのファイルを `/blog/blog/data` にコピーします。

5. `theme/hugo-theme-reimu/_example` にあるすべてのファイルを `/blog/blog/content` にコピーします。このフォルダが存在しない場合は作成します。

6. `theme/hugo-theme-reimu/assets` にあるすべてのファイルを `/blog/blog/assets` にコピーします。

7. ... `theme/hugo-theme-reimu/layouts` のすべてのファイルを `/blog/blog/layouts` にコピーします。

8. `theme/hugo-theme-reimu/static` のすべてのファイルを `/blog/blog/static` にコピーします。

9. 以下のコードを `/blog/blog/hugo.toml` にコピーします。

                                                                                   以下をクリック👇して展開します。

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
title = 'xxx'
author = 'xxx'

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

10. /blog/blog のアドレスバーに「cmd」と入力してコマンドラインを起動します。「hugo server -D」と入力してブログを起動します。アドレスが表示されたら、Ctrlキーを押しながらクリックしてログインします。この時点で、ブラウザはテーマのサンプルインターフェースを正常に表示できるはずです。これでブログの設定は完了です。

## 3. テーマ設定（任意参照）
### 3.1 多言語 i18n 設定
1. `/blog/blog/config/_default/params.yml` を開き、`name` と `url` の設定をカスタマイズし、変更後に保存します。

2. `/blog/blog/i18n` フォルダにある、対応する言語の `.yml` ファイルを開きます。いくつか開き、該当する部分を変更します。

[上記の `hugo.toml` で簡体字中国語、英語、日本語の3つの言語を設定したと仮定し、これら3つの言語に対してi18nを設定します。]

以下はサンプルコードです。

```params.yml
# メニューセクション
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
# メニューに関連するコードのみ表示
home: Home
about: About
link: Link
archives: Archives
```
```zh-CN.yml
# メニューに関連するコードのみ表示
home: 主页
about: 关于
link: 更多
archives: 归档
```
```ja.yml
# 表示のみメニュー関連コード
home: ホームページ
about: プログラム
link: リンク
archives: アーカイブ
```

上記のコードを修正したら、実行してみてください。多言語機能が正しく動作するはずです。
### 3.2 コア設定
このセクションでは、このテーマのコア設定ファイルである params.yml について解説します。コードをセグメントごとに分析することで、設定をスムーズに完了できるようにします。

/blog/blog/config/_default/params.yml にアクセスしたら、以下の手順に従って設定をカスタマイズしてください。

コードはかなり長いので、先に進む前によくお読みください。中国語と英語のコメントは非常に詳細です。正確な設定のために必ずお読みください。
                                                                                   以下をクリック👇して展開します。
```params.yml
menu:
  - name: home
    url: ""
    icon: 'xxx'                       #  https://github.com/D-Sketon/hexo-theme-reimu/issues/30
  - name: archives
    url: "sort"
    icon: 'xxx'
  - name: about
    url: "about"
    icon: 'xxx'
  - name: link
    url: "link"
    icon: 'xxx'

mainSections: ["post"]
yearFormat: "2006"
monthFormat: "2006-01"
dateFormat: "2006-01-02"
timeFormat: "2006-01-02 15:04:05"

author: xxx
email: xxx@example.com
description: "xxxxxxxxxxxxxxxxxxx"
# subtitle: "少女祈祷中..."
subtitle:
  typing:
    enable: true
    strings:
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

avatar: "avatar.png"

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
### 3.3 記事ページの作成

1. /blog/blog のアドレスバーでコマンドプロンプトを開き、「hugo new content post/blog1/index.md」と入力するか、`/blog/blog/content` フォルダ内に `blog1` という新しいフォルダを作成し、その中に `index.md` という新しいファイルを作成します。ファイルを開きます。ショートコード機能を使用する必要がある場合は、以下のセクション 4.3 を参照してください。

2. 必要に応じて以下のコードをコピーしてください。**2 つのコードスニペットは用途が異なります。ニーズに合ったものを選択してください。**

```Article Example 1.md
# これは純粋な記事のフォーマットです
+++
data = '2026-01-01T09:00:00+09:00'
weight = 1 # これは記事をピン留めするためのフォーマットです
+++
Content: blah blah blah blah blah blah blah
```

```Article Example 2.md
# これはタグまたはディレクトリ設定を含めるためのフォーマットです
---
data: '2026-01-01T09:00:00+09:00'
weight: 1 # これは記事をピン留めするためのフォーマットです
---
tags:
- タグ 1
- タグ 2
categories:
- ディレクトリ 1
- ディレクトリ 2 # 2つ目のディレクトリ名は以下で設定する必要がありますparams.yml に記述してください。そうしないと表示されません。
---
内容: blah blah blah blah blah blah
```

### 3.4 ショートコードの使用
ウェブページに機能を追加したい場合、より高度なコードの使用が必要になることがあります。Hugo フレームワークにはいくつかの制限がありますが、ユーザーのニーズに応えるため、ショートコードというバックドアが用意されています。

該当するコードを使用する必要がある場合は、行間、2行間、{{ などのスペースを削除して、コードが確実に実行されるようにしてください。

コードは作成時に動作を確認しています。動作しない場合は、コード内のスペースをご自身で調整してください。

#### heatMapCard 記事ヒートマップ

このカードは**記事ページ**にのみ表示できます。記事の冒頭部分は、ホームページやその他の場所には表示できません。

ヒートマップを表示するには、記事の冒頭に戻ってください。

このカードを記事ページで使用するには、以下のコードを参照してください。例：

```Article Page.md
{ {< heatMapCard levelStandard="?" >} }
{{< heatMapCard levelStandard="?" >}}
```

#### 友達リンクカード
コンテンツにfriend.mdファイルが含まれている場合は、以下のコードを参照してください。例：

```Article Page.md
{ {< friendsLink >} }
{{< friendsLink >}}
```
#### タグルーレット
このカードは記事ページにのみ表示されます。

このカードを使用するには、以下のコードを参照し、タグとアイコンをカスタマイズしてください。

使用方法：アイコンをクリックすると、ランダムにタグが表示されます。

例:

```Article Page.md
{ {< tagRoulette tags="tag1,tag2,tag3" icon="🎲" >} }
{{< tagRoulette tags="tag1,tag2,tag3" icon="🎲" >}}

```
#### alertBlockquote ブロック参照
このカードは記事ページにのみ表示されます。

このカードを記事ページで使用するには、以下のコードを参照してください。例:

```Article page.md
{ {< alertBlockquote type="0721" >} }

Ciallo～(∠・ω< )⌒★

{ {</alertBlockquote>} }

{{< alertBlockquote type="0721" >}}
Ciallo～(∠・ω< )⌒★
{{</alertBlockquote>}}

または、note、tips、important、warning などの類似モジュールを使用することもできます。他にも、以下のような類似モジュールがあります。

{ {< alertBlockquote type="note" >} }

Ayachi Nene is Coming～

{ {< /alertBlockquote >} }

{{< alertBlockquote type="note" >}}
Ayachi Nene is Coming～
{{< /alertBlockquote >}}

```
#### link リンクカード

このカードは記事ページにのみ表示されます。

記事ページでこのカードを使用するには、以下のコードを参照してください。例：

```Article Page.md
{ {< link title="0721" link="https://ciallo.cc" cover="auto" escape="true" >} }
{{< link title="0721" link="https://ciallo.cc" cover="auto" escape="true" >}} または

{ {< link title="0721" path="https://ciallo.cc" cover="auto" escape="true" >} }
{{< link title="0721" path="https://ciallo.cc" cover="auto" escape="true" >}}

```
#### gallery フォトウォール

このカードは記事ページにのみ表示されます。

このカードを記事ページで使用するには、以下のコードを参照してください。例:

```Article Page.md
{ {< gallery >} }

! [図 1] (https://xxx.com/xxx.webp)

! [図 2] (https://xxx.com/xxx.webp)

...
{ {</gallery>} }

{{< gallery >}}
![図 1](https://tc.alcy.cc/tc/20260121/2c785c4a015e858d9d470d51ca702a1a.webp)
![図 2](https://tc.alcy.cc/tc/20260121/6c4e58cf6f6ce1cc144f834ba98d22fa.webp)
...
{{</gallery>}}

```
#### グリッド グリッドレイアウト

このカードは記事ページにのみ表示できます。

このカードを記事ページで使用するには、以下のコードを参照してください。例:

```Article Page.md
{ {< grid width=300 col=3 >} }

<!-- cell -->

07211

<!-- cell -->

07212

<!-- cell -->

07213

{ {< /grid >} }

表示効果:

{{< grid width=300 col=3 >}}
<!-- cell -->
07211
<!-- cell -->
07212
<!-- cell -->
07213
{{< /grid >}}
```
#### 詳細折りたたみパネル

このカードは記事ページにのみ表示できます。

このカードを記事ページで使用するには、以下のコードを参照してください。

```Article Page.md
{ {< details summary="0721" >} }

Ciallo～(∠・ω< )⌒★

{ {< /details >} }

{{< details summary="0721" >}}
Ciallo～(∠・ω< )⌒★
{{< /details >}}

```

## 4. ブログへのデプロイ

### 4.1 標準デプロイ (**初回使用時に必須**)

1. GitHub アカウントにログインし、https://github.com/example?tab=repositories に example.github.io/blog という名前の新しいリポジトリを作成します。

2. /blog/blog/public フォルダのアドレスバーでコマンドプロンプトを開き、以下のコードを入力します。

```
git init
git add .
git commit -m "最初のコミット"
git branch -M main
git remote add origin https://github.com/example/blog.git # 必ず変更してください
git push -u origin main # 失敗した場合は -u を -f に変更してください

```

3. 進行状況が 100% に達したら、GitHub ページを更新します。実行中のリポジトリが表示されます。「設定」をクリックし、「ページ」をクリックし、「ブランチ」セクションで main を選択して、「保存」をクリックします。

4. 数分待ってから更新します。このページに「Your site is live at https://example.github.io/blog/」のようなアドレスが表示され、デプロイが成功したことを示します。

{{< details summary="別のドメインを使用しますか？" >}}
別のドメイン名を使用する場合、リポジトリ名は `example.github.io` である必要があります。以下の設定では、Cloudflare と Huawei Cloud を例として使用しています。他のドメインサービスプロバイダーでは設定が異なる場合があります。

ドメイン設定方法：

1. Cloudflare でメインドメイン名の解決を完了します。例えば、Cloudflare で example.com などのメインドメイン名を解決済みの場合は、以下の操作を実行する前に、ブログで使用するドメイン名（`blog.example.com` など）を決定します。

注：ここで使用するドメイン名は、トップレベルドメインまたはセカンドレベルドメインである必要があります。.dpdns.org や .cc.wt などの無料ドメイン名を使用すると、Huawei Cloud では **使用可能なドメイン名として認識されません**。

2. [Huawei Cloud](https://www.huaweicloud.com/intl/ja-jp/) ウェブサイト を開いたときに、国際地域が表示されていることを確認してください。次に、メールアドレスを使用してアカウントを登録します。登録中にログインを求められた場合は、「理解しました」を選択し、「今は有効にしない」をクリックします。携帯電話番号の紐付けに関する要求はスキップしてください。3. コンソールに入ったら、「マイリソース」セクションの「パブリックドメイン」をクリックします。手順1で決定したドメイン名を追加します。追加が完了したら、以下のテンプレートに従って、CloudflareとHuawei Cloudでそれぞれ設定します。

Cloudflareの設定：

| タイプ | 名前 | ネームサーバー | TTL |
| :---: | :---: | :---: | :---: |
| NS | blog | ns1.huaweicloud-dns.org | 自動 |
| NS | blog | ns1.huaweicloud-dns.net | 自動 |
| NS | blog | ns1.huaweicloud-dns.com | 自動 |
| NS | blog | ns1.huaweicloud-dns.cn | 自動 |

Huawei Cloud 設定：「レコードセットを追加」をクリックし、以下の情報を入力して確定します。

| Type | Name | Line | TTL (秒) | Value |
| :---: | :---: | :---: | :---: | :---: |
| CNAME | 空白のままにする | Default | 300 | Github リポジトリ名 |

6. Github の「設定 - ページ」ページで、下にスクロールして「カスタムドメイン」を見つけ、ドメイン名を入力して「保存」をクリックします。最後に「HTTPS を強制する」に**必ずチェックを入れてください**（「保存」をクリックしても「HTTPS を強制する」がグレー表示され、チェックが外れている場合はエラーが発生しています。戻って確認してください）。設定が反映されるまでお待ちください。

7. この設定が完了すると、ドメイン `blog.example.com` にアクセスしてブログにアクセスできます。
{{< /details >}}

### 4.2 自動デプロイ (**初期デプロイは完了、その後のコード更新が必要**)

1. `/blog/blog` に新しいファイル `.gitignore` を作成し、ファイルを開いて以下の内容をコピーして保存します。

```.gitignore
public
resources
.hugo_build.lock
hugo.exe
```

2. `/blog/blog` 内に `.github` フォルダを作成し、そのフォルダ内に `workflows` フォルダを作成します。さらに、そのフォルダ内に新しいファイル `hugo_deploy.yaml` を作成し、以下のコードをコピーして保存します。
```hugo_deploy.yaml
name: deploy

# 代码提交到main分支时触发github action
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
              EXTERNAL_REPOSITORY: [あなたのGitHub名/倉庫名]
              PUBLISH_BRANCH: main
              PUBLISH_DIR: ./public
              commit_message: auto deploy

```

3. リポジトリインターフェースで、アバターをクリックし、「設定」をクリックします。**サイドバー** の一番下までスクロールして、「開発者設定」をクリックします。「個人アクセストークン」をクリックし、表示された「トークン（クラシック）」をクリックします。「新しいトークンの生成」をクリックします。「新しいトークンの生成（クラシック）」をクリックします。

4. ユーザーを確認します。「メモ」は任意で入力します。「有効期限」は「無期限」を選択します。「スコープの選択」は、すべてのリポジトリエントリとワークフローにチェックを入れます。一番下までスクロールして「トークンの生成」をクリックします。**重要** 生成されたキーは必ずコピーして保存してください。表示されるのは一度だけです!!!

5. 作成したリポジトリページに戻り、「設定」をクリックし、下にスクロールして、サイドバーの「セキュリティ」の下にある「シークレットと変数」を見つけて、「アクション」をクリックします。

6. 「リポジトリシークレット」で「新しいリポジトリシークレット」をクリックし、以下のテンプレートを入力して、「シークレットを追加」をクリックします。

```
名前*
トークン


シークレット*
ghp_xxxxxxxxxxxxxxxxxxxxxxxx # 手順4で生成したキーをここに貼り付けます。
```

7. /blog/blog フォルダのアドレスバーに「cmd」と入力してコマンドラインを開き、以下のコードを入力します。GitHubアカウントの確認を求められる場合がありますが、指示に従ってください。アップロードを成功させるには、プロキシを実行したままにしてください。

```
git add .
git commit -m "update"
git push -u origin main # 失敗する場合は、-u を -f に変更してください。
```

8. GitHubインターフェースに戻り、「アクション」をクリックします。現在実行中の2つのワークフロー（ウェブページ上では workflow として表示）が緑色のチェックマーク付きで正常に動作していることを確認できたら、「設定」をクリックし、「ページ」をクリックして、「ブランチ」セクションで「main」を選択し、「保存」をクリックします。

9. 数分待ってからページを更新します。「ページ」ページにアドレスが表示されたら、ブログを閲覧できます。