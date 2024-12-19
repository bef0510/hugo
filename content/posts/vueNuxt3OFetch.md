+++
date = '2024-12-19T08:45:41+08:00'
draft = true
title = 'Vue Nuxt3 OFetch'
tags = ['Html', 'Vue', 'TypeScript', 'Nuxt3']
categories = ['Html', 'Vue']
+++

### 使用 **$fetch** 會發送兩次
```
<template>
  <div class="my-24 flex flex-col items-center">
    <span class="text-xl text-gray-400">[$fetch]</span>
    <span class="my-2 text-2xl text-gray-600">回傳資料:</span>
    <p class="my-4 text-xl font-semibold text-blue-500">{{ data }}</p>
  </div>
</template>

<script setup lang="ts">
  // 預設為通用渲染，server 端請求一次；client 端請求一次 (Hydration)
  const data = await $fetch('https://60bd9841ace4d50017aab3ec.mockapi.io/api/post_card')
</script>
```

### 使用 **useAsyncData** 解決 **$fetch** 發送兩次問題
```
<template>
  <div class="my-24 flex flex-col items-center">
    <span class="text-xl text-gray-400">[$useAsyncData]</span>
    <span class="my-2 text-2xl text-gray-600">回傳資料:</span>
    <p class="my-4 text-xl font-semibold text-blue-500">{{ data }}</p>
  </div>
</template>

<script setup lang="ts">
  const data = await useAsyncData('about', () => $fetch('https://60bd9841ace4d50017aab3ec.mockapi.io/api/post_card'))
</script>
```

### 使用 **useFetch = useAsyncData + $fetch**
```
<template>
  <div class="my-24 flex flex-col items-center">
    <span class="text-xl text-gray-400">[$useFetch]</span>
    <span class="my-2 text-2xl text-gray-600">回傳資料:</span>
    <p class="my-4 text-xl font-semibold text-blue-500">{{ data }}</p>
  </div>
</template>

<script setup lang="ts">
  const data = await useFetch('https://60bd9841ace4d50017aab3ec.mockapi.io/api/post_card')
</script>
```

### **useFetch** 各回傳參數 使用範例
```
<template>
  <div class="my-24 flex flex-col items-center">
    <span class="text-xl text-gray-400">[$useFetch]</span>
    <span class="mt-4 text-xl text-sky-500">請求狀態: {{ status }}</span>
    <span v-if="error" class="mt-4 text-xl text-rose-500">發生錯誤: {{ error }}</span>
    <span class="my-2 text-2xl text-gray-600">回傳資料:</span>
    <p v-if="pending" class="my-4 text-xl font-semibold text-blue-500">請求處理中...</p>
    <p v-else class="my-4 text-xl font-semibold text-blue-500">{{ data }}</p>

    <button class="mt-6 rounded-md bg-blue-500 px-6 py-3 text-white hover:bg-blue-600 focus:outline-none"
      @click="refresh">重新獲取
    </button>
  </div>
</template>
  
<script setup lang="ts">
  console.log('fetch data')
  const{ data, pending, refresh, error, status } = await useFetch('https://60bd9841ace4d50017aab3ec.mockapi.io/api/post_card')
  console.log('data =>', data)
  console.log('pending =>', pending)
  console.log('refresh =>', refresh)
  console.log('error =>', error)
  console.log('status =>', status)
</script>
```

## 參考
[Nuxt3](https://nuxt.com/docs/api/utils/dollarfetch "")