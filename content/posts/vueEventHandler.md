+++
date = '2024-12-11T16:24:17+08:00'
draft = true
title = 'Vue 事件處理'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

### 事件 **click** 基礎
```
function greet(event: any) {
  // event 是 DOM 原生事件
  console.log(event);
  console.log(event.target.tagName);
}

<button v-on:click="greet">Greet</button>

<!-- 簡寫 -->
<button @click="greet">Greet</button>
```

### 事件 **click** 參數
```
function greet(message: string) {
  console.log(message);
}

<button @click="greet('hello')">Greet</button>

<!-- 傳入 event -->
function warn(message: any, event: any) {
  // 原生事件
  console.log(event);
}

<button @click="warn('hello', $event)">Submit</button>

<!-- 傳入 event arrow -->
<button @click="(event) => warn('hello', event)">Submit</button>
```

### 事件 修飾語 -1
```
<!-- 點擊事將停止傳遞 -->
<button @click.stop="doThis"></button>

<!-- 提交事件後不再重新load頁面 -->
<form @submit.prevent="onSubmit"></form>

<!-- 可以再加修飾語 -->
<a @click.stop.prevent="doThat"></a>

<!-- 也可以只有修饰符 -->
<form @submit.prevent></form>

<!-- 本身才會載發，子元素不會 -->
<div @click.self="doThat">...</div>
```

### 事件 修飾語 -2
```
<!-- 有子元素時，會先觸發這個 -->
<div @click.capture="doThis">...</div>

<!-- 只會被觸發一次 -->
<a @click.once="doThis"></a>


function onScroll(event: any) {
  // event 是 DOM 原生事件
  console.log(event)
}

<!-- 觸發 scroll 事件 -->
<div @scroll.passive="onScroll" style="height: 100px;overflow:auto;">
  ..........<br/>..........<br/>..........<br/>..........<br/>..........<br/>..........<br/>
</div>
```

### 事件 修飾語 按鍵
```
<!-- 按 enter 時 -->
<input @keyup.enter="submit" />

<!-- 按 page-down 時 -->
<input @keyup.page-down="onPageDown" />

<!-- 常用 -->
.enter
.tab
.delete ("Delete" 和 "Backspace")
.esc
.space
.up
.down
.left
.right

<!-- 系統按鍵 -->
.ctrl
.alt
.shift
.meta

<!-- Alt + Enter -->
<input @keyup.alt.enter="clear" />
```

## 參考
[Vue.js](https://cn.vuejs.org/guide/essentials/event-handling.html "")