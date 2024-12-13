+++
date = '2024-12-12T11:01:50+08:00'
draft = true
title = 'Vue 模板'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

### 使用 **set focus()**
```
import { onMounted, useTemplateRef } from 'vue';
let email: any = useTemplateRef('email');
const name: any  = useTemplateRef('name');

onMounted(() => {
  name.value.focus();
});

<input type="text" ref="email">
<input type="text" ref="name">
```

### 使用 **v-for**
```
import { ref, useTemplateRef, onMounted } from 'vue';

const list = ref([
  'item 1', 'item 2', 'item 3'
]);

const itemRefs = useTemplateRef('items');

onMounted(() => console.log(itemRefs.value));

<ul>
  <li v-for="item in list" ref="items">
    {{ item }}
  </li>
</ul>
```

### 使用 **component**
```
import { useTemplateRef, onMounted } from 'vue';
import HelloWorld from './components/HelloWorld.vue';

const childRef = useTemplateRef('child');

onMounted(() => {
  // childRef.value 将持有 <Child /> 的实例
  console.log(childRef.value);
})

<HelloWorld ref="child"></HelloWorld>
```

## **component**
### **component** 基礎引用
```
<!-- ButtonCounter.vue -->

<template>
  <button @click="onAdd">Count add</button>
  {{ count }}
</template>

<script setup lang="ts">
  import { ref } from 'vue';

  const count = ref(0);
  function onAdd() {
    count.value++;
  }
</script>

-------------------------------------
<!-- App.vue -->

<template>
  <ButtonCounter />
  <ButtonCounter></ButtonCounter>
</template>

<script setup lang="ts">
  import ButtonCounter from './components/ButtonCounter.vue'
</script>
```

### **component** 傳遞 **props (parent → child)**
```
<!-- ButtonCounter.vue -->

<template>
  <h4>{{ title }}</h4>
</template>

<script setup lang="ts">
  const props = defineProps(['title']);
  console.log(props);
  console.log(props.title);
</script>

-------------------------------------
<!-- App.vue -->

<template>
  <ButtonCounter title="My journey with Vue" /> <br />
  <ButtonCounter title="My journey with Vue"></ButtonCounter>
</template>

<script setup lang="ts">
  import ButtonCounter from './components/ButtonCounter.vue';
</script>
```

### **component** 傳遞多 **props**，不能傳 **object**
```
<!-- ButtonCounter.vue -->
<template>
  <h4>{{ title }}</h4>
  <h4>{{ id }}</h4>
</template>

<script setup lang="ts">
  defineProps(['title', 'id']);
</script>

-------------------------------------
<!-- App.vue -->

<template>
  <ButtonCounter v-for="post in posts"
    :id="post.id"
    :title="post.title" />
</template>

<script setup lang="ts">
  import { ref } from 'vue';
  import ButtonCounter from './components/ButtonCounter.vue';

  const posts = ref([
  { id: 1, title: 'My journey with Vue' },
  { id: 2, title: 'Blogging with Vue' },
  { id: 3, title: 'Why Vue is so fun' }
]);
</script>
```

### **component** 傳遞 **v-model** (parent → child)
```
<!-- ButtonCounter.vue -->
<template>
  {{ firstName }} - {{ lastName }}
</template>

<script setup lang="ts">
  import { defineModel } from "vue"
  const firstName = defineModel('firstName')
  const lastName = defineModel('lastName')
</script>

-------------------------------------
<!-- App.vue -->

<template>
  <ButtonCounter
    v-model:firstName="firstName"
    v-model:lastName="lastName"/>
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  import ButtonCounter from './components/ButtonCounter.vue'

  const firstName = ref('darren')
  const lastName = ref('wang')
</script>

```

### **component emit (child → parent)**
```
<!-- ButtonCounter.vue -->
<template>
  <div class="blog-post">
    <h4>{{ msg }}</h4>
    <button @click="updateText">emit event</button>
  </div>
</template>

<script setup lang="ts">
  import { ref, defineProps, defineEmits } from 'vue';
  // parent's props
  const props = defineProps(['message']);
  const emit = defineEmits(["update"]);

  // local props
  const msg = ref(props.message);

  function updateText() {
    msg.value = 'hello';
    emit('update', msg.value); 
  }
</script>

-------------------------------------
<!-- App.vue -->

<template>
  <ButtonCounter :message="message" @update="selfUpdate" />
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  import ButtonCounter from './components/ButtonCounter.vue'

  const message = ref('');

  function selfUpdate(message: string) {
    console.log(123, message)
  }
</script>
```

### **component tag** 插入文字 **slot**
```
<!-- ButtonCounter.vue -->
<template>
  <div class="blog-post">
    <h4>{{ msg }}</h4>

    <slot></slot>
		
    <button @click="updateText">emit event</button>
  </div>
</template>

<script setup lang="ts">
  import { ref, defineProps, defineEmits } from 'vue';
  // parent's props
  const props = defineProps(['message']);
  const emit = defineEmits(["update"]);

  // local props
  const msg = ref(props.message);

  function updateText() {
    msg.value = 'hello';
    emit('update', msg.value); 
  }
</script>

-------------------------------------
<!-- App.vue -->

<template>
  <ButtonCounter :message="message" @update="selfUpdate">
    Something bad happened.<br />
  </ButtonCounter>
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  import ButtonCounter from './components/ButtonCounter.vue'

  const message = ref('hi');

  function selfUpdate(message: string) {
    console.log(123, message)
  }
</script>

```

## **is** 動態載入 **components**
```
<!-- Child_1.vue -->

<template>
  {{ test }}
  <slot></slot>
</template>

<script setup lang="ts">
  import { ref } from "vue"
  const test = ref('test1')
</script>

-------------------------------------
<!-- Child_2.vue -->

<template>
  {{ test }}
</template>

<script setup lang="ts">
  import { ref } from "vue"
  const test = ref('test2')
</script>

-------------------------------------
<!-- App.vue -->

<template>
  <button @click="onCurrentView">change component</button>
  <component :is="currentComp">
    <span>hello</span>
  </component>
</template>

<script setup lang="ts">
  import { shallowRef } from 'vue'
  import Child1 from "./components/Child_1.vue";
  import Child2 from "./components/Child_2.vue";

  let currentComp = shallowRef(Child1)
  
  function onCurrentView() {
    currentComp.value = currentComp.value === Child1 ? Child2 : Child1;
  }
</script>
```

## 依賴注入 **provide inject** (可跳層，不用一層一層傳遞)
```
<!-- ButtonCounter.vue -->

<template>
  {{ message }}
</template>

<script setup lang="ts">
  import { inject } from "vue"
  const message = inject('message')
</script>

-------------------------------------
<!-- App.vue -->

<template>
  <ButtonCounter />
</template>

<script setup lang="ts">
  import { ref, provide } from 'vue'
  import ButtonCounter from './components/ButtonCounter.vue'

  provide('message', 'hello!')
</script>
```

## 參考
[Vue.js](https://cn.vuejs.org/guide/essentials/template-refs.html "")
