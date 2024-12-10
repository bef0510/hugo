+++
date = '2024-12-06T10:23:50+08:00'
draft = true
title = '使用 Netlify 架設 Hugo 專案'
tags = ['Hugo', 'Taxonomy']
categories = ['Hugo']
+++

## 修改專案

#### 1. 修改 **hugo.toml**
```
baseURL = 'https://darrenwang.netlify.app/'
languageCode = 'en-us'
title = "Darren's notes"
theme = 'paper'
buildDrafts = true
```
![](/images/002_hugoWithNetlify/01.png)

#### 2. 新增 **netlify.toml**
```
[build.environment]
HUGO_VERSION = "0.139.3"
TZ = "America/Los_Angeles"

[build]
publish = "public"
command = "hugo --gc --minify"
```
![](/images/002_hugoWithNetlify/02.png)

## **Git Hub**
[GitHub網站](https://github.com/ "GitHub")

#### 1. 新增一個 **Repository**
![](/images/002_hugoWithNetlify/03.png)
![](/images/002_hugoWithNetlify/04.png)

#### 2. **Upload files**
![](/images/002_hugoWithNetlify/05.png)

## **Netlify**
[Netlify網站](https://github.com/ "Netlify")

#### 1. 使用 **Git Hub** 帳號登入
![](/images/002_hugoWithNetlify/06.png)

#### 2. 新增一個站台專案來源
![](/images/002_hugoWithNetlify/07.png)

#### 3. 選取專案來源
![](/images/002_hugoWithNetlify/08.png)
![](/images/002_hugoWithNetlify/09.png)

#### 4. 發佈專案
![](/images/002_hugoWithNetlify/10.png)
![](/images/002_hugoWithNetlify/11.png)
![](/images/002_hugoWithNetlify/12.png)

#### 5. 查看網址
[Darren's notes](https://darrenwang.netlify.app "Darren's notes")
![](/images/002_hugoWithNetlify/13.png)

## 參考
[Host on Netlify](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/ "")