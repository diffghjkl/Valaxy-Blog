---
layout: <%=layout%>
title: <%=title%>
date: <%=date%>
categories: 
tags: 
 - 
icon:  // 标题前的图标
cover:  // 文章封面&头图
author: // 作者
top:  // 置顶，数字越大越靠前
nav:  // true 显示前一篇、后一篇导航
toc:  // false 隐藏目录
aside:  // false 隐藏右侧文章导航栏（即右侧目录所在卡片）
comment:  // false 关闭评论
codeHeightLimit:  // 300 代码块高度限制（300px）
draft:  // true 为草稿，将仅在开发时被展示
copyright:  // true 显示文章底部版权信息
sponsor: // true 开启赞助
hide: 
 // 临时隐藏文章（该文章仍然会被渲染）
 // true / all 当设置为 true 或 all 时，该文章仍然会被渲染，你可以直接访问链接进行查看。但不会被显示在展示的文章卡片与归档中
 // index 设置为 index 时，将只在首页隐藏，归档中仍然展示（譬如放一些没有必要放在首页的笔记，并在归档中方便自己查看）
password: 
 // 加密文章的密码
 // 被加密的内容应在解密后动态渲染。此时无法（也不应）参与到构建流程中生成静态产物（否则会被直接看到）。 因此对于加密内容中的图片路径，总是应该使用绝对路径而非相对路径。
excerpt: // 自定义摘要（优先级高于 <!-- more -->）
excerpt_type: 
 // 预览列表摘要的渲染类型（与 <!-- more --> 配合使用）
 // md 展示原始 Markdown
 // html 以 HTML 形式展示
 // text 以纯文本形式展示（去除 HTML 标签）
---
