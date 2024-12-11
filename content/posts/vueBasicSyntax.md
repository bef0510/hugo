+++
date = '2024-12-11T11:09:35+08:00'
draft = true
title = 'Vue 基礎語法'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

### 綁定 **Html class** 基本
```
<div v-bind:class="{ active: isActive }"></div>

<!-- 簡寫 -->
<div :class="{ active: isActive }"></div>
```

### 綁定 **Html class** 搭配 **template**
```
const isActive = ref(true)
const hasError = ref(false)

<div class="static" :class="{ active: isActive, 'text-danger': hasError }"></div>

<!-- 渲染後 -->
<div class="static active"></div>
```

### 綁定 **Html class** 搭配 **object**
```
const classObject = reactive({
  active: true,
  'text-danger': false
})

<div :class="classObject"></div>

<!-- 渲染後 -->
<div class="active"></div>
```

### 綁定 **Html class** 搭配 **object** + 計算
```
const isActive = ref(true)
const error = ref(null)

const classObject = computed(() => ({
  active: isActive.value && !error.value,
  'text-danger': error.value && error.value.type === 'fatal'
}))

<div :class="classObject"></div>

<!-- 渲染後 -->
<div class="active"></div>
```

### 綁定 **Html class** 陣列
```
const activeClass = ref('active')
const errorClass = ref('text-danger')

<div :class="[activeClass, errorClass]"></div>

<!-- 渲染後 -->
<div class="active text-danger"></div>
```

### 綁定 **Html class** 三元運算式
```
const activeClass = ref('active')
const errorClass = ref('text-danger')

<div :class="[isActive ? activeClass : '', errorClass]"></div>

<!-- 渲染後 -->
<div class="active text-danger"></div>
```

### 綁定 **Html class** 陣列 + 三元運算式
```
const activeClass = ref('active')
const errorClass = ref('text-danger')

<div :class="[{ [activeClass]: isActive }, errorClass]"></div>

<!-- 渲染後 -->
<div class="active text-danger"></div>
```

### 綁定 **Html style** 基本
```
const activeColor = ref('red')
const fontSize = ref(30)

<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

<!-- 簡寫 -->
<div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

<!-- kebab-cased 型態 -->
<div :style="{ 'font-size': fontSize + 'px' }"></div>
```

### 綁定 **Html style** 搭配 **object**
```
const styleObject = reactive({
  color: 'red',
  fontSize: '30px'
})

<div :style="styleObject"></div>
```

### 綁定 **Html style** 陣列
```
const styleObject1 = reactive({
  color: 'red'
})

const styleObject2 = reactive({
  fontSize: '30px'
})

<div :style="[styleObject1, styleObject2]"></div>
```

### 條件渲染 **v-if**
```
<h1 v-if="awesome">Vue is awesome!</h1>

<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

### 條件渲染 **v-else**
```
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```

### 條件渲染 **v-else-if**
```
<div v-if="type === 'A'">A</div>
<div v-else-if="type === 'B'">B</div>
<div v-else-if="type === 'C'">C</div>
<div v-else>Not A/B/C</div>
```

### 條件渲染 **v-show**
```
<h1 v-show="ok">Hello!</h1>
```

### 列表渲染 **v-for** 基礎
```
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])

<ul>
  <li v-for="item in items">{{ item.message }}</li>
</ul>

<!-- with index -->
<ul>
  <li v-for="(item, index) in items">{{ index }} - {{ item.message }}</li>
</ul>

<!-- 也可用 of -->
<div v-for="item of items">{{ item.message }}</div>

<!-- with template -->
<ul>
  <template v-for="item in items"><li>{{ item.message }}</li></template>
</ul>
```

### 列表渲染 **v-for** 搭配 **object**
```
const myObject = reactive({
  title: 'How to do lists in Vue',
  author: 'Jane Doe',
  publishedAt: '2016-04-10'
})

<ul>
  <li v-for="value in myObject">{{ value }}</li>
</ul>

<!-- 第二個參數是 key -->
<ul>
  <li v-for="(value, key) in myObject">{{ key }}: {{ value }}</li>
</ul>

<!-- 第三個參數是 index -->
<ul>
  <li v-for="(value, key, index) in myObject">{{ key }}: {{ value }} - {{ index }}</li>
</ul>
```

### 列表渲染 **v-for** 直接給值
```
<!-- 初始值是 1 -->
<span v-for="n in 10">{{ n }}</span>
```

### 列表渲染 **v-for** 搭配 **key**
```
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>

<template v-for="todo in todos" :key="todo.name">
  <li>{{ todo.name }}</li>
</template>
```

### 列表渲染 **v-for** 搭配 **component**
```
<MyComponent v-for="item in items" :key="item.id" />

<!-- 需要自己傳 prop 進去 -->
<MyComponent
  v-for="(item, index) in items"
  :item="item"
  :index="index"
  :key="item.id"
/>
```

## 參考
[Vue.js](https://cn.vuejs.org/guide/essentials/class-and-style.html "")