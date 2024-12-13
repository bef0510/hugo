+++
date = '2024-12-13T12:49:15+08:00'
draft = true
title = 'Json Server'
tags = ['Json-Server']
categories = ['Json-Server']
+++

### 1. 安裝 **Json Server**
```
npm i json-server
```

### 2. 新增 **json** 檔案
![](/images/013_userJsonServer/01.png)

### 3. 修改 **package.json**
```
"server": "json-server --watch src/prods.json --port 3005"
```
![](/images/013_userJsonServer/02.png)

### 4. **run server**
```
npm run server
```
![](/images/013_userJsonServer/03.png)

## 參考
[json-server](https://www.npmjs.com/package/json-server "")