---
title: "{{ replace .File.ContentBaseName "-" " " | humanize | title }}"
description: 
slug: "{{ .Name }}"
date: {{ .Date | time.Format "2006-01-02"}}
categories:
    - CSharp
tags:
    - C#
---
