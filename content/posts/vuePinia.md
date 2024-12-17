+++
date = '2024-12-16T17:06:34+08:00'
draft = true
title = 'Vue Pinia'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

### **Vue Pinia** 對應
![](/images/017_vuePinia/01.png)

### 1. 安裝 **Vue Pinia**
```
npm i pinia
```

### 2. 修改檔案 **main.js**
```
import './assets/main.css'

import router from './router';

import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'

const app = createApp(App)

app.use(router);
app.use(createPinia())
app.mount('#app')

app.config.errorHandler = (err) => {
  console.log('errorHandler', err)
}
```
![](/images/017_vuePinia/02.png)

### 3. 增加檔案 **src → stores → counter.js Option API**
```
import { defineStore } from "pinia";

export const useCounterStore = defineStore({
  id: 'counter',
  // 定義狀態初始值
  state: () => ({ count: 0, name: 'Darren'}),

  // 對狀態加工的 getters，如同 computed
  getters: {
    doubleCount: (state) => state.count * 2,
  },

  // 定義使用到的函式，可以為同步和非同歲，如同 method
  actions: {
    increment() {
      this.count++;
    },
  }
});
```
![](/images/017_vuePinia/03.png)

### 4. 增加檔案 **src → stores → counter.js Composition API**
```
import { computed, ref } from "vue";
import { defineStore } from "pinia";

export const useCounterStore = defineStore('counter', () => {
  const count = ref(0);

  const doubleCount = computed(() => {
    return count.value * 2
  });

  const increment = () => {
    count.value++;
  };

  return {
    count,
    increment,
    doubleCount
  };
});

```

### 使用方式 **Option API**
```
<template>
  <div>
    <h2>counter</h2>

    <!-- 取得的 state 會響應式更新 -->
     <p>{{ counterStore.count }}</p>

     <!-- 可以呼叫 store 內定義的方法來修改 state -->
      <button @click="counterStore.increment">+</button>

      <!-- 也可以直接修改 state -->
      <button @click="counterStore.count++">+</button>
  </div>
</template>

<script setup lang="ts">
  import { useCounterStore } from  '../stores/counter.js';

  const counterStore = useCounterStore();
</script>
```

### 使用方式
```
<template>
  <div>
    <h2>counter</h2>

    <!-- 取得的 state 會響應式更新 -->
     <p>{{ counterStore.count }}</p>

     <!-- 可以呼叫 store 內定義的方法來修改 state -->
      <button @click="counterStore.increment">+</button>

      <!-- 也可以直接修改 state -->
      <button @click="counterStore.count++">+</button>
  </div>
</template>

<script setup lang="ts">
  import { useCounterStore } from  '../stores/counter.js';

  const counterStore = useCounterStore();
</script>
```

### **Pinia** 呼叫 **api**
```
<!-- store → counter.js -->
import { computed, ref } from "vue";
import { defineStore } from "pinia";
import axios from "axios";

export const useCounterStore = defineStore('counter', () => {

  const cardList = ref([]);

  const fetchApiData = async () => {

    // then 寫法
    axios.get('https://60bd9841ace4d50017aab3ec.mockapi.io/api/post_card')
      .then(res => {
        cardList.value = res.data;
      }).catch(error => {
        console.log(error);
      });

    // promise 寫法
    try{
      const res = await axios.get('https://60bd9841ace4d50017aab3ec.mockapi.io/api/post_card');
      cardList.value = res.data;
    } catch(error) {
      console.log(error);
    }
  }

  return {
    cardList,
    fetchApiData
  };
});

-------------------------------------
<!-- 呼叫 vue -->

<template>
  <div>
    <h2>counter</h2>
    <pre>
      {{ counterStore.cardList }}
    </pre>

    <button @click="counterStore.fetchApiData">click fetch</button>
  </div>
</template>

<script setup lang="ts">
  import { storeToRefs } from 'pinia';
  import { useCounterStore } from  '../stores/counter.js';

  const counterStore = useCounterStore();
</script>
```

### 承上 **Pinia** 解構 + 響應式功能
```
<!-- 呼叫 vue -->
<template>
  <div>
    <h2>counter</h2>
    <pre>
      {{ cardList }}
    </pre>

    <button @click="fetchApiData">click fetch</button>
  </div>
</template>

<script setup lang="ts">
  import { storeToRefs } from 'pinia';
  import { useCounterStore } from  '../stores/counter.js';
  
  // 響應式
  const store = useCounterStore();

  // function 一律 store 來
  const { increment, fetchApiData } = store;

  // 解構 storeToRefs 回傳的物件
  const { count, cardList } = storeToRefs(store);
</script>
```

### **Pinia store** 交互使用
```
<!-- store about.js -->

import { ref } from "vue";
import { defineStore } from "pinia";

export const useAboutStore = defineStore('about', () => {
    const name = ref('Darren');

    const SetName = (userName) => {
        console.log(123)
        name.value = userName;
    }

    return {
        name,
        SetName
    };
});

-------------------------------------
<!-- store about.js -->

import { computed, ref } from "vue";
import { defineStore, storeToRefs } from "pinia";
import axios from "axios";
import { useAboutStore } from "./about.js";

export const useCounterStore = defineStore('counter', () => {
  const aboutStore = useAboutStore();

  const { SetName } = aboutStore;
  // 解構
  const { name } = storeToRefs(aboutStore);

  const cardList = ref([]);
  const count = ref(0);

  const doubleCount = computed(() => {
    return count.value * 2 + name.value;
  });

  const increment = () => {
    count.value++;
    SetName('Ya~');
  };

  const fetchApiData = async () => {
    try{
      const res = await axios.get('https://60bd9841ace4d50017aab3ec.mockapi.io/api/post_card');
      cardList.value = res.data;
    } catch(error) {
      console.log(error);
    }		
  }

  return {
    count,
    increment,
    doubleCount,
    cardList,
    fetchApiData
  };
});
```

### 監控值改變
```
<template>
  <div>
    <h2>counter</h2>
    <pre>
      {{ cardList }}
    </pre>
    <!-- 取得的 state 會響應式更新 -->
     <p>{{ count }}</p>
    <p>{{ doubleCount }}</p>
     <!-- 可以呼叫 store 內定義的方法來修改 state -->
      <button @click="increment">+</button>

      <!-- 也可以直接修改 state -->
      <button @click="count++">+</button>

      <button @click="fetchApiData">click fetch</button>
  </div>
</template>

<script setup lang="ts">
  import { watch } from 'vue';
  import { storeToRefs } from 'pinia';
  import { useCounterStore } from  '../stores/counter.js';
 
  const store = useCounterStore();
  const { increment, fetchApiData } = store;

  // 解構 storeToRefs 回傳的物件
  const { count, cardList, doubleCount } = storeToRefs(store);

  // 方式一 vue watch
  watch(doubleCount, (newVal, oldVal) => {
    console.log('newVal =>', newVal);
    console.log('oldVal =>', oldVal);
  });

  // 方式二 pinia subscribe
  store.$subscribe((mutation, state) => {
    console.log('mutation =>', mutation);
    console.log('state =>', state);
  });
</script>
```

## 參考
[Pinia](https://pinia.vuejs.org/introduction.html "")