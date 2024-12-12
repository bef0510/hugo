+++
date = '2024-12-10T11:43:49+08:00'
draft = true
title = 'Vue 常用套件'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

### **vue-official**
```
VS Code Extensions 安裝
會卡，不使用
```

## **eslint**
[eslint規則網站](https://eslint.vuejs.org/rules/ "eslint規則 網站")
```
VS Code Extensions 安裝
```
![](/images/006_vueCommonlyUsedPackages/01.png)

### 修改 **eslint.config.js**
```
...
{
  rules: {

  }
},
...
```
![](/images/006_vueCommonlyUsedPackages/02.png)

### 未定義 **component**
```
"vue/no-undef-components": "error"
```
#### 錯誤
![](/images/006_vueCommonlyUsedPackages/03.png)
#### 正常
![](/images/006_vueCommonlyUsedPackages/04.png)

### 定義要比較值加型別 (TS)
```
"eqeqeq": "warn"
```
#### 錯誤
![](/images/006_vueCommonlyUsedPackages/05.png)
#### 正常
![](/images/006_vueCommonlyUsedPackages/06.png)

### 定義要比較值加型別 (Html)
```
"vue/eqeqeq": "warn"
```
#### 錯誤
![](/images/006_vueCommonlyUsedPackages/07.png)
#### 正常
![](/images/006_vueCommonlyUsedPackages/08.png)

### **template** 未使用 **defineProps**
```
"vue/no-unused-properties" : "error"
```
#### 錯誤
![](/images/006_vueCommonlyUsedPackages/09.png)
#### 正常
![](/images/006_vueCommonlyUsedPackages/10.png)

### 未使用 **defineEmits**
```
"vue/no-unused-emit-declarations" : "error"
```
#### 錯誤
![](/images/006_vueCommonlyUsedPackages/11.png)
#### 正常
![](/images/006_vueCommonlyUsedPackages/12.png)

## 快速建立 **vue3** 模板 **vs code** 設定
![](/images/006_vueCommonlyUsedPackages/13.png)
![](/images/006_vueCommonlyUsedPackages/14.png)
![](/images/006_vueCommonlyUsedPackages/15.png)
```
<!-- vue.json -->
{
  "vue3": {
    "prefix": "vue3",
    "body": [
      "<template>",
      "  {{ test }}",
      "</template>",
      "",
      "<script setup lang=\"ts\">",
      "  import { ref } from \"vue\"",
      "",
      "  const test = ref('test')",
      "</script>",
      "",
      "<style scoped>",
      "",
      "</style>",
      ""
    ],
    "description": "快速建立 vue3 模板"
  }
}
```

### 使用方式
![](/images/006_vueCommonlyUsedPackages/16.png)
![](/images/006_vueCommonlyUsedPackages/17.png)

## 參考
[Vue 3 教學 - 使用 ESLint 提高 Debug 效率 (Vue3, ESLint)](https://youtu.be/iwMzzAzYgjE?list=PLGAh4USR7RcvNq_8hyrEKojKLx4r-z5f7 "")