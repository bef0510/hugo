+++
date = '2024-12-18T14:25:00+08:00'
draft = true
title = 'Vue Nuxt3 Route'
tags = ['Html', 'Vue', 'TypeScript', 'Nuxt3']
categories = ['Html', 'Vue']
+++

### 動態路由 單一參數
```
<!-- 在 vue3 -->
path: "/about/:id",
name: "about",
component: AboutView,

<!-- 在 Nuxt -->
使用檔案名稱 [id].vue
<template>
  這裡是 users 動態路由頁面
  <p>id: {{ id }}</p>
</template>

<script setup lang="ts">
  const route = useRoute()
  const { id } = route.params;
</script>
```
![](/images/020_vueNuxt3Route/01.png)

### 動態路由 多參數
```
<!-- 在 Nuxt -->
使用檔案名稱 [...slug].vue
<template>
  {{ slug }}
</template>

<script setup lang="ts">
  const route = useRoute()
  const { slug } = route.params;
</script>
```
![](/images/020_vueNuxt3Route/02.png)
![](/images/020_vueNuxt3Route/03.png)

### **404 not found**
```
<!-- pages 根目錄 [...slug].vue -->
<template>
  404 not found
</template>

<script setup lang="ts">
  setResponseStatus(404)
</script>
```
![](/images/020_vueNuxt3Route/04.png)

## 複雜路由
![](/images/020_vueNuxt3Route/05.png)

### 新增 **category → index.vue**
```
<template>
  <h1>Category 頁面</h1>
  <div>
    <NuxtLink to="/category/8">前往指定的類別</NuxtLink><br />
    <NuxtLink to="/category/8/posts/1">前往指定的類別的文章</NuxtLink><br />
    <NuxtLink to="/category/top-3">前往 Top 3</NuxtLink><br />
    <NuxtLink to="/category/top-10">前往 Top 10</NuxtLink>
  </div>
</template>

<script setup lang="ts">
  import { ref } from "vue"

  const test = ref('test')
</script>
```

### 新增 **category → [categoryId] → index.vue**
```
<template>
  <h1>Category Id: {{ categoryId }}</h1>
</template>

<script setup lang="ts">
  const route = useRoute()
  const { categoryId } = route.params;
</script>
```

### 新增 **category → [categoryId] → posts → [postId].vue**
```
<template>
  <h1>Category Id: {{ categoryId }}</h1>
  <div>Post Id: {{ postId }}</div>
</template>

<script setup lang="ts">
  const route = useRoute()
  const { categoryId, postId } = route.params;
</script>
```

### 新增 **category → top-[number].vue**
```
<template>
  <h1>這是 category/top-[number]</h1>
  <div>top number: {{ number }}</div>
</template>

<script setup lang="ts">
  const route = useRoute()
  const { number } = route.params;
</script>
```

## **route middleware**
### 匿名路由 **middleware**
```
<!-- pages → index.vue-->

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

<script setup lang="ts">
 definePageMeta({
  middleware: defineNuxtRouteMiddleware(() => {
    console.log('[匿名 middleware] 進入頁面')
  })
 })
</script>
```

### 具名路由 **middleware**
```
<!-- middleware → random-redirect.js -->

export default defineNuxtRouteMiddleware(() => {
  if (Math.random() > 0.5) {
    console.log('middleware Redirecting to /hero')
    return navigateTo('/hero')
  }

  console.log('middleware not-thing happened')
})

<!-- 呼叫方式 about.vue -->

<template>
  <div class="m-6 mb-4 bg-slate-50 py-24">
    <div class="flex flex-col items-center">
        <h1 class="text-6xl font-semibold text-yellow-400">This is Darren</h1>
        <p class="my-8 text-3xl text-gray-600">Here is /about</p>
    </div>
  </div>
</template>

<script setup lang="ts">
  definePageMeta({
    middleware: ['random-redirect'] // 可用多個，以陣列方式
  })
</script>
```

### 全域路由 **middleware**
```
<!-- middleware → always-run.global.js -->

export default defineNuxtRouteMiddleware((to, from) => {
  console.log(`middleware to: ${to.path}, from: ${from.path}`)
})
```

## 參考
[Nuxt3](https://nuxt.com.cn/docs/getting-started/installation "")