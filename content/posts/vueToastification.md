+++
date = '2024-12-13T15:09:52+08:00'
draft = true
title = 'Vue Toastification'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

### 1. 安裝 **Vue Toastification**
```
npm i vue3-toastify
```

### 2. 修改 **main.js**
```
import './assets/main.css'

import Vue3Toastify, { type ToastContainerOptions } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';

import { createApp } from 'vue'
import App from './App.vue'

const app = createApp(App)

app.use(Vue3Toastify, {
  autoClose: 3000,
} as ToastContainerOptions);

app.mount('#app')

app.config.errorHandler = (err) => {
  console.log('errorHandler', err)
}
```
![](/images/015_vueToastification/01.png)

### 3. 使用方式
```
<template>
  1
</template>

<script setup lang="ts">
  import { onMounted } from 'vue';
  import { toast } from 'vue3-toastify';

  onMounted(() => {
    setTimeout(() => {
      toast.info('info TOP_RIGHT',{
        position: toast.POSITION.TOP_RIGHT,
      });

      toast.error('error!!');
      toast.success('success!!');
      toast.success('success colored TOP_LEFT!!', {
        theme: 'colored',
        position: toast.POSITION.TOP_LEFT,
      });
      toast.warn('warn TOP_LEFT!!', {
        position: toast.POSITION.TOP_LEFT,
      });
      toast.warn('warn dark TOP_LEFT!!', {
        theme: 'dark',
        position: toast.POSITION.TOP_LEFT,
      });
    
    }, 3000)
  })
</script>
```
![](/images/015_vueToastification/02.png)

## 參考
[vue3-toastify](https://www.npmjs.com/package/vue3-toastify "")