+++
date = '2024-12-10T10:11:39+08:00'
draft = true
title = 'Vue 起手式'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

## **Vue** 建立專案

### 1. **using CDN**
```
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

### 2. **using npm**
```
npm create vue@latest projectName
```
![](/images/005_vueOpeningGesture/01.png)

### 3. **install**
```
cd projectPath
npm i
```
![](/images/005_vueOpeningGesture/02.png)

### 4. 修改 **vite.config.ts → Port 3000**
```
...
server: {
  port: 3000,
},
...
```
![](/images/005_vueOpeningGesture/03.png)

## DOM 掛載
```
<div id="app"></div>

<script>
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
</script>
```

## 基本架構
```
<template>
  <!-- 只能有一個 root dom -->
  <div class="vue-component-example">
    <!-- ... -->
  </div>
</template>

<script>
  export default {
    // Vue instance 的各種屬性和設定
  }
</script>

<style scope>
  .vue-component-example {
    /* ... */
  }
</style>
```

### **Option API** 選項式
```
<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>

<script>
export default {
  // 宣告響應式資料的初始值
  data() {
    return {
      count: 0
    }
  },

  // methods 宣告在元件中要使用的方法
  methods: {
    increment() {
      this.count++
    }
  },

  // mounted 回傳對資料的加工或計算結果
  mounted() {
    incrementd() {
      console.log(`The initial count is ${this.count}.`)
    }
  }
}
</script>
```

### **Composition  API** 組合式，組合模板
```
<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>

<script setup>
import { ref } from 'vue'

export default {
  setup() {
    const count = ref(0)

    function increment() {
      // 在 JavaScript 中需要 .value
      count.value++
    }

    // 要暴露 increment 函式
    return {
      count,
      increment
    }
  }
}
</script>
```

### **Composition  API** 組合式，單文件組合 **(SFC)**
```
<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>

<script setup>
import { computed, reactive, ref } from "vue";

// 宣告響應式資料的初始值
const count = ref(0);

// methods 宣告在元件中要使用的方法
function increment() {
  count.value++;
}

// mounted 回傳對資料的加工或計算結果
const incrementd = computed(() => 	console.log(`The initial count is ${count.value}.`));
</script>
```

### 擴充 **main.ts → error**
```
import './assets/main.css'

import { createApp } from 'vue'
import App from './App.vue'

const app = createApp(App)
app.mount('#app')

app.config.errorHandler = (err) => {
  console.log('errorHandler', err)
}
```
![](/images/005_vueOpeningGesture/04.png)

## 參考
[Vue.js](https://cn.vuejs.org/guide/introduction.html "")