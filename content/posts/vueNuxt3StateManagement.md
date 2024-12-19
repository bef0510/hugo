+++
date = '2024-12-19T09:23:11+08:00'
draft = true
title = 'Vue Nuxt3 狀態管理'
tags = ['Html', 'Vue', 'TypeScript', 'Nuxt3']
categories = ['Html', 'Vue']
+++

### **Hydration** 問題
```
<template>
  <div class="bg-white py-24">
    <div class="flex flex-col items-center">
        <span class="text-9xl font-semibold text-sky-400">{{ count }}</span>
    </div>
  </div>
</template>

<script setup lang="ts">
  // 因為通用渲染關係，server 先給一次值，client 再給一次，會出現 warn
  const count = ref(Math.round(Math.random() * 1000));
</script>
```
![](/images/026_vueNuxt3StateManagement/01.png)

### 使用 **useState** 避免 **Hydration** 問題
```
<template>
  <div class="bg-white py-24">
    <div class="flex flex-col items-center">
      <span class="text-9xl font-semibold text-sky-400">{{ count }}</span>
    </div>
  </div>
</template>

<script setup lang="ts">
  // 給一個 'count' id，client 端執行時看到有 id 就不會再執行一次
  const count = useState('count', () => Math.round(Math.random() * 1000));
</script>
```

### **useState** 離開畫面回來後。值還是存在，重新整理頁面後，執才會初始化
```
<!-- increment.vue -->
<template>
  <div class="bg-white py-24">
    <div class="flex flex-col items-center">
      <span class="text-9xl font-semibold text-sky-600">{{ counter }}</span>
      <div class="mt-8 flex flex-row">
        <button class="font-base mx-2 rounded-full bg-sky-500 px-4 py-2 text-xl text-blue-500"
          @click="counter++">增加</button>
        <button class="font-base mx-2 rounded-full bg-sky-500 px-4 py-2 text-xl text-blue-500"
          @click="counter--">減少</button>
      </div>
      <p class="mt-4 text-slate-500">第一次進頁面，初始值為 0</p>
      <div class="mt-8">
        <NuxtLink to="/">回首頁</NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
  const counter = useState('counter', () => 0);
</script>

-------------------------------------
<!-- index.vue -->

<template>
  <div class="bg-white py-24">
    <div class="flex flex-col items-center">
      <h1 class="text-6xl font-semibold text-gray-800">這是首頁</h1>
      <div class="my-4 flex flex-col space-y-4">
        <NuxtLink to="/count">前往 count</NuxtLink>
        <NuxtLink to="/count/useState">前往 useState</NuxtLink>
        <NuxtLink to="/counter/increment">increment</NuxtLink>
      </div>
    </div>
  </div>
</template>
```

### 使用 **useState** 跨元件共享
```
<!-- surprise.vue -->

<template>
  <div class="bg-white py-24">
    <div class="flex flex-col items-center">
      <span class="text-9xl font-semibold text-sky-600">{{ counter }}</span>
      <div class="mt-8 flex flex-row">
        <button class="font-base mx-2 rounded-full bg-sky-500 px-4 py-2 text-xl text-blue-500"
          @click="counter++">增加</button>
        <button class="font-base mx-2 rounded-full bg-sky-500 px-4 py-2 text-xl text-blue-500"
          @click="counter--">減少</button>
      </div>
      <p class="mt-4 text-slate-500">第一次進頁面，初始值為 0</p>
      <div class="mt-8">
        <NuxtLink to="/">回首頁</NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
  const counter = useState('counter', () => Math.round(Math.random() * 1000));
</script>

-------------------------------------
<!-- index.vue -->

<template>
  <div class="bg-white py-24">
    <div class="flex flex-col items-center">
      <h1 class="text-6xl font-semibold text-gray-800">這是首頁</h1>
      <div class="my-4 flex flex-col space-y-4">
        <NuxtLink to="/count">前往 count</NuxtLink>
        <NuxtLink to="/count/useState">前往 useState</NuxtLink>
        <NuxtLink to="/counter/increment">increment</NuxtLink>
        <NuxtLink to="/counter/surprise">surprise</NuxtLink>
      </div>
    </div>
  </div>
</template>
```

### 使用 **composibles** 元件共享
```
<!-- composables → useLocale.js -->

export default function () {
  return useState('locale', () => 'zh-TW')
}

-------------------------------------
<!-- locale.vue -->

<template>
  <div class="bg-white py-24">
    <div class="flex flex-col items-center">
        <p class="mt-4 text-xl text-slate-500">Locale</p>
        <span class="text-6xl font-semibold text-emerald-400">{{ locale }}</span>
    </div>
  </div>
</template>

<script setup lang="ts">
  const locale = useLocale()
</script>

-------------------------------------
<!-- index.vue -->

<template>
  <div class="bg-white py-24">
    <div class="flex flex-col items-center">
      <h1 class="text-6xl font-semibold text-gray-800">這是首頁</h1>
      <div class="my-4 flex flex-col space-y-4">
        <NuxtLink to="/count">前往 count</NuxtLink>
        <NuxtLink to="/count/useState">前往 useState</NuxtLink>
        <NuxtLink to="/counter/increment">increment</NuxtLink>
        <NuxtLink to="/counter/surprise">surprise</NuxtLink>
        <NuxtLink to="/locale">locale</NuxtLink>
      </div>
    </div>
  </div>
</template>
```

## 使用 **pinia**
```
npm install -D pinia --force
npm install -D @pinia/nuxt
```

### 1. 修改 **nuxt.config.ts**
```
export default defineNuxtConfig({
  modules: [
    ...
    '@pinia/nuxt'
  ],
  compatibilityDate: '2024-11-01',
  devtools: { enabled: true }
})
```

### 2. 使用方式
```
<!-- stores → counter.js -->

import { defineStore } from 'pinia'

export const useCounterStore = defineStore('counter', () => {
  const count = ref(0);

  const doubleCount = computed(() => {
    return count.value * 2
  });

  const increment = () => {
    count.value++;
  };

  const decrement = () => {
    count.value--;
  };

  return {
    count,
    increment,
    decrement,
    doubleCount
  };
});

-------------------------------------
<!-- counter.vue -->

<template>
  <div class="bg-white py-24">
    <div class="flex flex-col items-center">
      <span class="text-9xl font-semibold text-sky-600">{{ counterStore.count }}</span>
      <div class="mt-8 flex flex-row">
        <button class="font-base mx-2 rounded-full bg-sky-500 px-4 py-2 text-xl text-blue-500"
          @click="counterStore.increment">增加</button>
        <button class="font-base mx-2 rounded-full bg-sky-500 px-4 py-2 text-xl text-blue-500"
          @click="counterStore.decrement">減少</button>
      </div>
      <p class="mt-4 text-slate-500">第一次進頁面，初始值為 0</p>
      <div class="mt-8">
        <NuxtLink to="/">回首頁</NuxtLink>
      </div>
    </div>
  </div>
</template>
  
<script setup lang="ts">
  import { useCounterStore } from '~/stores/counter';
  const counterStore = useCounterStore();
</script>

-------------------------------------
<!-- show.vue -->

<template>
  <div class="bg-white py-24">
    <div class="flex flex-col items-center">
      <span class="text-9xl font-semibold text-sky-600">{{ counterStore.count }}</span>
      <div class="mt-8">
        <NuxtLink to="/">回首頁</NuxtLink>
      </div>
    </div>
  </div>
</template>
  
<script setup lang="ts">
  import { useCounterStore } from '~/stores/counter';
  const counterStore = useCounterStore();
</script>
```

### 將 **stores** 資料夾加入 **auto import**
```
<!-- nuxt.config.ts -->

export default defineNuxtConfig({
  ...
  devtools: { enabled: true },
  imports: {
    dirs: ['stores'] // 陣列方式將資料夾加入 auto import
  }
})

-------------------------------------
<!-- counter.vue -->

<script setup lang="ts">
  const counterStore = useCounterStore();
</script>

-------------------------------------
<!-- show.vue -->
  
<script setup lang="ts">
  const counterStore = useCounterStore();
</script>
```

### **pinia** 持久化套件，用於 **local storeage**
```
npm install -D @pinia-plugin-persistedstate/nuxt
```

### 修改 **nuxt.config.ts** 重整後，值仍然存在，且存在 **local storeage**
#### 建議搭配 **client only**
```
export default defineNuxtConfig({
  modules: [
    ...
    '@pinia/nuxt',
    '@pinia-plugin-persistedstate/nuxt'
  ],
  compatibilityDate: '2024-11-01',
  devtools: { enabled: true },
  imports: {
    dirs: ['stores']
  }
})

<!-- stores → counter.js -->
import { defineStore } from 'pinia'

export const useCounterStore = defineStore('counter', () => {

    ...

    return {
      count,
      increment,
      decrement,
      doubleCount
    }
  }, {
    persist: {
      key: 'counter',
      storage: persistedState.localStorage
    }
});
```
![](/images/026_vueNuxt3StateManagement/02.png)

## 參考
[Nuxt3](https://nuxt.com/docs/getting-started/state-management "")