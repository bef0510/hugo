+++
date = '2024-12-18T14:33:04+08:00'
draft = true
title = 'Vue Nuxt3 Layout'
tags = ['Html', 'Vue', 'TypeScript', 'Nuxt3']
categories = ['Html', 'Vue']
+++

### 新增 **layout → default.vue**
```
<template>
  預設版型
</template>

<!-- 呼叫方式 -->
<template>
  <NuxtLayout />
</template>
```
![](/images/021_vueNuxt3Layout/01.png)

### 基本配置
```
<!-- default.vue -->

<template>
  <div class="bg-sky-100 py-6">
    <p class="px-6 py-2 text-2xl text-sky-600">
      這個是藍色的背景是預設的布局，預計給全部的頁面使用
    </p>

    <!-- 可放導覽列 -->
    <slot name="header"></slot>

    <!-- 可放主要內容 -->
    <slot></slot>

    <!-- 網頁頁腳資訊 -->
    <slot name="footer"></slot>
  </div>
</template>

-------------------------------------
<!-- app.vue -->

<template>
  <div>
    <p class="my-2 px-2 text-2xl text-gray-700">最外層 app.vue</p>
  </div>
  <NuxtLayout>

    <!-- 可放導覽列 -->
    <template #header>
      <p class="px-12 text-green-500">
        這段文字顯示 header slot 的內容
      </p>
    </template>

    <!-- 可放主要內容 -->
    <template #default>
      <p class="px-12 px-6 text-xl text-rose-500">
        被 NuxtLayout 包裹的元件會放置到 Layout 預設的 slot 中
      </p>
    </template>

    <!-- 網頁頁腳資訊 -->
    <template #footer>
      <p class="px-12 text-sky-500">
        這段文字顯示 footer slot 的內容
      </p>
    </template>
  </NuxtLayout>
</template>
```

### 搭配路由
```
<!-- app.vue -->

<template>
  <div>
    <p class="my-2 px-2 text-2xl text-gray-700">最外層 app.vue</p>
  </div>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>

-------------------------------------
<!-- pages → index.vue -->

<template>
  <div class="m-6 bg-slate-50 py-24">
    <div class="flex flex-col items-center">
        <h1 class="text-6xl font-semibold text sky-400">Title</h1>
        <p class="mt-4 text-9xl font-bold text-gray-600">Content</p>
    </div>
  </div>
  <div class="flex flex-col items-center">
    <div class="my-4 flex space-x-4">
        <NuxtLink to="/about" class="px-4 py-2 bg-gray-300 text-gray-800 rounded-lg">前往 About</NuxtLink>
        <NuxtLink to="/contact" class="px-4 py-2 bg-gray-300 text-gray-800 rounded-lg">前往 contact</NuxtLink>
    </div>
  </div>
</template>

-------------------------------------
<!-- pages → about.vue -->

<template>
  <div class="m-6 mb-4 bg-slate-50 py-24">
    <div class="flex flex-col items-center">
        <h1 class="text-6xl font-semibold text-yellow-400">This is Darren</h1>
        <p class="my-8 text-3xl text-gray-600">Here is /about</p>
    </div>
  </div>
</template>

-------------------------------------
<!-- pages → contact.vue -->

<template>
  <div class="m-6 mb-4 bg-slate-50 py-24">
    <div class="flex flex-col items-center">
      <h1 class="text-6xl font-semibold text-yellow-400">This is Contact</h1>
      <p class="my-8 text-3xl text-gray-600">Here is /Contact</p>
    </div>
  </div>
</template>
```

### 自訂 **layout**
```
<!-- layouts → about.vue -->

<template>
  <div class="bg-rose-100 py-6">
    <p class="px-6 py-2 text-2xl text-rose-600">
        這個紅色背景表示使用 custom-layout 布局
    </p>
    <slot />
  </div>
</template>

-------------------------------------
<!-- pages → contact.vue -->

// 使用自訂義 layout
<script setup lang="ts">
  definePageMeta({
    layout: 'custom-layout'
  })
</script>

-------------------------------------
<!-- pages → contact.vue -->

// 不使用任何 layout
<script setup lang="ts">
  definePageMeta({
    layout: 'custom-layout'
  })
</script>
```

## 參考
[Nuxt3](https://nuxt.com.cn/docs/getting-started/installation "")