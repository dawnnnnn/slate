---
title: API Reference

language_tabs:
  - shell
  - php
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - basis
  - questions
  - blogs
  - articles
  - shares
  - notes
  - activities
  - favorites
  - tags
  - user
  - settings
  - assist


search: true
---

# Introduction 简介

## API 文档简介

SegmentFault API 采用 REST 风格设计。所有接口请求地址都是可预期的以及面向资源的。使用规范的 HTTP 响应代码来表示请求结果的正确或错误信息。使用 HTTP 内置的特性，如 HTTP Authentication 和 HTTP 请求方法让接口易于理解。所有的 API 请求都会以规范友好的 JSON 对象格式返回（包括错误信息）。

# Authentication

期望在识别用户登录状态时，将用户的 `token` 以 Header 的方式放入请求中

`Authorization: token`




