+++
date = '2024-12-13T13:26:06+08:00'
draft = true
title = 'Vue Spinner'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

### 1. 安裝 **Vue Spinner**
```
npm i vue-spinner
```

### 2. **PulseLoader**
```
<template>
  <div v-if="state.loading">
    <PulseLoader :color="color" :size="size" />
  </div>
  <div v-else>
    <h1>Hello world</h1>
  </div>
</template>

<script setup lang="ts">
  import { onMounted, ref, reactive } from 'vue'
  import PulseLoader from 'vue-spinner/src/PulseLoader.vue'

  const state = reactive({
    loading: true
  })

  const color = ref('red')  // default color is green
  const size = ref('15px') // defalue size is 15px

  onMounted(() => {
    setTimeout(() => {
      state.loading = false
    }, 3000)
  })
</script>
```
![](/images/014_vueSpinner/01.png)

### 3. 其他範例
```
<template>

  <FadeLoader />
  
</template>

<script setup lang="ts">
  
  import FadeLoader from 'vue-spinner/src/FadeLoader.vue'

</script>
```
![](/images/014_vueSpinner/02.png)

## 參考
[Vue Spinner](https://madewith.cn/728 "")