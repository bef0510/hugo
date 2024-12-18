+++
date = '2024-12-18T15:28:32+08:00'
draft = true
title = 'Vue Nuxt3 Components'
tags = ['Html', 'Vue', 'TypeScript', 'Nuxt3']
categories = ['Html', 'Vue']
+++

### 新增 **components → Welcome.vue**
```
<template>
  <div class="py-24">
    <div class="flex flex-col items-center">
      <h1 class="text-6xl font-semibold text-sky-400">Welcome title</h1>
      <p class="my-8 text-3xl text-gray-600">Welcome content</p>
    </div>
  </div>
</template>

<!-- 呼叫方式 -->
<template>
  <Welcome />
</template>
```
![](/images/022_vueNuxt3Components/01.png)

### **Client only***
```
<!-- components → base → BaseApplyButton.vue -->

<template>
  <button class="mt-6 bg-blue-600 px-8 py-3 text-xl font-medium text-white hover:bg-blue-500">
    Clike me
  </button>
</template>

<!-- 呼叫方式 -->
<template>
  <div class="flex flex-col items-center">
    
    <!-- 只有 client 看的到 -->
    <ClientOnly>
      <BaseApplyButton />

      <template #fallback>
        <p class="my-6 flex justify-center">
          [BaseApplyButton] 元件載入中...
        </p>
      </template>
    </ClientOnly>
  </div>
</template>
```

### 另一種 **client** 端渲染方式
```
<!-- components → JustClient.client.vue -->
<template>
  <div class="mx-16 my-4 rounded-lg bg-green-100 p-4 text-sm text-green-700">
    <span class="font-semibold">[JustClient.client.vue]</span>
    <span class="ml-2">
      這是只有在 <span class="font-bold">Client</span>才會渲染的元件
    </span>
  </div>
</template>

<!-- 呼叫方式 -->

<template>
  <div class="flex flex-col items-center">
    <JustClient />
  </div>
</template>
```

### 動態載入 **components**
```
<!-- 只要在 components 前加上 Lazy -->
<LazyBaseApplyButton />
```

## 參考
[Nuxt3](https://nuxt.com.cn/docs/getting-started/installation "")