+++
date = '2024-12-19T11:42:26+08:00'
draft = true
title = 'Vue Nuxt3 useCookie'
tags = ['Html', 'Vue', 'TypeScript', 'Nuxt3']
categories = ['Html', 'Vue']
+++

### **cookie** 使用
```
<template>
  <div class="flex flex-col items-center justify-center px-4 py-6">
    <div class="flex w-full max-w md flex-col justify-center">
      <div class="flex flex-col items-center">
        <h2 class="my-4 text-center text-3xl font-bold tracking-tight text-gray-700">Cookie</h2>
      </div>
      <div class="mx-auto flex w-full max-w xs flex-row justify-around gap-2">
        <div class="flex flex-col items-center gap-2">
          <button type="button" class="w-fit rounded-sm bg-emerald-500 px-4 py-2 text-sm text-white hover:bg-emerald-600"
           @click="setNameCookie">設置 name</button>
        </div>
        <div class="flex">
          <label class="text-lg font-semibold text-emerald-500">name:</label>
          <span class="ml-2 flex text-lg text-slate-700">{{ name }}</span>
        </div>
      </div>
      <div class="flex flex-col items-center gap-2">
        <button type="button" class="w-fit rounded-sm bg-emerald-500 px-4 py-2 text-sm text-white hover:bg-emerald-600"
           @click="setCounterCookie">設置 counter</button>
      </div>
      <div class="flex">
          <label class="text-lg font-semibold text-emerald-500">counter:</label>
          <span class="ml-2 flex text-lg text-slate-700">{{ counter }}</span>
        </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const name = useCookie('name');
const counter = useCookie('counter', { maxAge: 10 }); // 10 秒後過期

const setNameCookie = () => {
  name.value = 'Darren'
}

const setCounterCookie = () => {
  counter.value = Math.round(Math.random() * 1000)
}
</script>
```

## 參考
[Nuxt3](https://nuxt.com/docs/api/composables/use-cookie "")