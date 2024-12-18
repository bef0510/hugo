+++
date = '2024-12-18T15:59:13+08:00'
draft = true
title = 'Vue Nuxt3 Plugin'
tags = ['Html', 'Vue', 'TypeScript', 'Nuxt3']
categories = ['Html', 'Vue']
+++

### 1. 安裝 **vue-scrollto**
```
npm install -D vue-scrollto
```

### 2. 重新啟動 **server**
```
npm run dev
```

### 基本使用方式 **scrollto**
```
<!-- plugins → scrollto.js -->

import VueScrollTo from 'vue-scrollto'

export default defineNuxtPlugin((nuxtApp) => {
  console.log(12, nuxtApp)
  nuxtApp.vueApp.use(VueScrollTo)
})

<!-- 呼叫方式 -->

<template>
  <div class="flex flex-col items-center overflow-y-visible px-6 py-4">
    <a v-scroll-to="'#element'" href="#" class="my-4 font-medium text-gray-600">
      捲動頁面至 #element
    </a>
    
    <div id="element" class="mt-24">
      <h1 class="p-2 text-6xl font-semibold text-sky-400">
        捲動至此
      </h1>
    </div>

    <div class="h-screen w-full"></div>
  </div>
</template>
```

### **helper** 使用方式 **scrollto**
```
<!-- scrollto.js -->
import VueScrollTo from 'vue-scrollto'

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.use(VueScrollTo)

  return {
    provide: {
      scrollTo: VueScrollTo.scrollTo
    }
  }
})

<!-- 呼叫方式 -->
```

### 自定 **directive (focus)**
```
<!-- plugins → directive.js -->

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.directive('focus', {
    mounted(el) {
      el.focus()
    }
  })
})

<!-- 呼叫方式 -->

<template>
  <button 
    v-focus
    class="my-4 w-fit rounded-full bg-blue-500 px-8 py-3 font-medium text-white hover:bg-blue-400"
    @click="scrollToElement">
      捲動頁面至 #element
  </button>

</template>
```

## 參考
[Nuxt3](https://nuxt.com.cn/docs/getting-started/installation "")