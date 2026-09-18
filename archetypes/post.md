---
title: {{ replace .File.ContentBaseName "-" " " | title | jsonify }}
date: {{ .Date }}
slug: {{ .File.ContentBaseName | jsonify }}
draft: true
description: ""
categories: []
tags: []
image: ""
---

在这里写正文。标题可使用中文；发布后保持 slug 不变。
