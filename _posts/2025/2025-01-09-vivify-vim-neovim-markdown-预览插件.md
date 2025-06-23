---
title: "Vivify.vim: Neovim Markdown 预览插件"
date: 2025-01-09
categories: 
  - "josiah的terminal本当上手"
tags: 
  - "markdown"
  - "markdown-preview"
  - "nvim"
  - "vivify"
---

最近在看MIT的The Missing Semester，然后有了想把自己markdown工作流从typora转换到nvim的想法，于是在网上找nvim的markdown插件，看到大家用的比较多的貌似是 [Markdown-Preview.nvim](https://github.com/iamcco/markdown-preview.nvim)，于是自己也上手试了试，但是后来在写笔记的时候发现这东西会莫名其妙的从类似/page/1重定向/1这样的地址，会导致流传输出现问题，非常的不优雅。故用了12个小时的时间来找问题（对不起我真的很菜）最后从index.jsx中发现它写了一段重定向，但是因为对这个语言不是很熟悉所以不想对项目的源文件做太多的修改。在看issue的过程中发现这基本上是个被作者完全放弃的开源项目，于是也不是很想在无人维护的项目上耗费太多自己的时间精力。最后的解决方法是换用了题目中提到的Vivify.vim，这个项目是vivify的一个扩展，用于连接vivify和nvim，作者维护比较用心，并且实际体验也不错，故写文章纪念自己浪费的12个小时。

链接在这里[https://github.com/jannis-baum/Vivify](https://github.com/jannis-baum/Vivify)
