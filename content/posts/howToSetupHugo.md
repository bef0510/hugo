+++
date = '2024-12-05T17:14:34+08:00'
draft = true
title = '如何建置 Hugo'
tags = ['Hugo', 'Taxonomy']
categories = ['Hugo']
+++

## 下載 **Hugo**
[Hugo網站](https://gohugo.io/ "Hugo 網站")
[直接下載](https://github.com/gohugoio/hugo/releases/tag/v0.139.3 "直接下載")

#### 1. 進入 **Hugo** 網站
![](/images/001_howToSetupHugo/01.png)

#### 2. **Installation → Windows**
![](/images/001_howToSetupHugo/02.png)

#### 3. 往下拉到 **Prebuilt binaries**
![](/images/001_howToSetupHugo/03.png)

#### 4. 點選版本下載
![](/images/001_howToSetupHugo/04.png)

#### 5. 解壓縮
![](/images/001_howToSetupHugo/05.png)

## 修改環境變數

#### 1. 將檔案放進 **Program Files\Hugo\bin**
![](/images/001_howToSetupHugo/06.png)

#### 2. 進階系統設定
![](/images/001_howToSetupHugo/07.png)

#### 3. 修改系統變數 **Path**
![](/images/001_howToSetupHugo/08.png)

#### 4. 增加 **Program Files\Hugo\bin**
![](/images/001_howToSetupHugo/09.png)

## 建立 **Hugo** 專案

#### 1. 建立專案
```
hugo new site MyNotes
```
![](/images/001_howToSetupHugo/10.png)

#### 2. 下載 **Theme**
[Hugo Themes](https://themes.gohugo.io/ "Hugo Themes")
![](/images/001_howToSetupHugo/11.png)

#### 3. 點擊 **Download**
![](/images/001_howToSetupHugo/12.png)

#### 4. Install **Theme**
![](/images/001_howToSetupHugo/13.png)

#### 5. **Git clone**
```
cd Mynotes
git clone https://github.com/nanxiaobei/hugo-paper themes/paper
```
![](/images/001_howToSetupHugo/14.png)

#### 6. 修改 **hugo.toml**
```
baseURL = 'https://example.org/'
languageCode = 'en-us'
title = "Darren's notes"
theme = 'paper'
```
![](/images/001_howToSetupHugo/15.png)

#### 7. 新增一個文章
```
hugo new posts/test.md
```
![](/images/001_howToSetupHugo/16.png)

#### 8. **Run** 專案
```
hugo server --buildDrafts
```

## 參考
[Hugo Blog Tutorial: Setting up Hugo and installing a theme](https://youtu.be/cev4gGE41e8 "")