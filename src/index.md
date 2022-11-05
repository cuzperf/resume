---
# Language (Optional)
lang: en
# Site Keywords & Description
keywords: Resume,Hexo,Resume Theme
description: This is a cool resume theme for hexo.
# Resume Title
resume_title: resume_title
# Job Applicant Name
name: your name
avatar: img/avatar.jpeg
# Contact
contact:
  # URL
  - icon: fas fa-globe-europe
    text: https://resume.js.org
    url: https://resume.js.org
  # Email
  - icon: fas fa-envelope
    text: your email
    url:
  # Phone Number
  - icon: fas fa-phone-alt
    text: 1xxxxxxxxxx
    url: tel:10086
# PDF Download Link
download:
  title: github link
  icon: fab fa-github
  url: https://github.com/cuzperf/resume
---

{% raw %}
<center>
<a href='en/'>cuzperf's Resume</a> | <a href='zh-cn/'>陈智鹏的简历</a>
</center>
{% endraw %}

## 原作者简历模版

<https://resume.js.org/zh-cn>

## Hexo 个人简历使用教程

- fork <https://github.com/xaoxuu/resume-docs>（也可以 fork 本 [repo](https://github.com/cuzperf/resume)）
- `git submodule update --init` 安装主题（可能不需要）
- `npm i` 看看效果（如果有报错可能需要 `npm install hexo-deployer-git`）
- 修改个人信息: `_config.yml` 和 `src` 下的内容，以及 `themes/resume/_config.yml` 中的 copyright
- 修改主题（可选）
- 正常的 `hexo c`, `hexo g`, `hexo s` 预览

## 修改主题

- fork <https://github.com/xaoxuu/hexo-theme-resume>，然后自行魔改
- [移出原有的 git submodule](https://blog.csdn.net/pcjustin/article/details/79350987)
- `git submodule add https://username@github.com/username/hexo-theme-resume.git themes/resume` 添加自己的
