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

## 參考
[Nuxt3](https://nuxt.com.cn/docs/getting-started/installation "")