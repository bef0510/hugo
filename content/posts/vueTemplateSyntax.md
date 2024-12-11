+++
date = '2024-12-10T17:18:06+08:00'
draft = true
title = 'Vue 模版語法'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

### 綁定 **Basic**
```
<div>{{ msg }}</div>
```

### 綁定 **Html** (有 **XSS** 漏洞，慎用)
```
<div v-html="msg"></div>
```

### 綁定 **Attribute**
```
<div v-bind:id="paramId"></div>

<!-- 簡寫 -->
<div :id="paramId"></div>

<!-- :id="id" -->
<div :id></div>
```

### 綁定 **bool Attribute**
```
<button :disabled="isDisabled"></button>
```

### **Html** 引用函式
```
<script setup lang="ts">
const checked: boolean = false;

function checkIsDisabled(checked: boolean) {
  return checked = !checked;
}
</script>

<template>
  <button :disabled="checkIsDisabled(checked)">Click</button>
</template>

```

### 綁定 **if**
```
<p v-if="isShow">Now you see me</p>
```

### 綁定 **href**
```
<a v-bind:href="url">說明</a>

<!-- 簡寫 -->
<a :href="url">說明</a>
```

### 綁定 **click function**
```
<a v-on:click="onClick()"> ... </a>

<!-- 無參數可不用 ( ) -->
<a v-on:click="onClick"> ... </a>

<!-- 簡寫 -->
<a @click="onClick"> ... </a>
```

### 綁定動態屬性
```
<script setup lang="ts">

const attribute: string = 'test';
const attributeName: string = 'id';

</script>

<template>
  <input type="type" v-bind:[attributeName]="attribute" />

  <!-- 簡寫 -->
  <input type="type" :[attributeName]="attribute" />
</template>
```
![](/images/007_vueTemplateSyntax/01.png)

### 綁定動態函式
```
<script setup lang="ts">

const eventName: string = 'focus';
function onDoSomething() {
  console.log('do something');
}

</script>

<template>
  <input type="type" v-on:[eventName]="onDoSomething" />

  <!-- 簡寫 -->
  <input type="type" @[eventName]="onDoSomething" />
</template>
```
![](/images/007_vueTemplateSyntax/02.png)

## 響應式狀態 (Composition API) 建議使用

### **ref()** 淺層監聽，單一值
```
import { ref } from 'vue'

const count = ref(0)
console.log(count) // { value: 0 }
console.log(count.value) // 0

count.value++
console.log(count.value) // 1
```

### **template** 中，不需使用 **.value**
```
<button @click="count++">
  {{ count }}
</button>
```

### **reactive()** 深層監聽，物件
```
import { reactive } from 'vue'

const state = reactive({ count: 0 })

<button @click="state.count++">
  {{ state.count }}
</button>
```

## 參考
[Vue.js](https://cn.vuejs.org/guide/essentials/template-syntax.html "")