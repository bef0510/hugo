+++
date = '2024-12-13T16:55:23+08:00'
draft = true
title = 'Vue Router'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

### 1. 安裝 **Vue Router**
```
npm i vue-router
```

### 2. 增加檔案 **src → router → index.js**
```
import { createRouter, createWebHashHistory } from "vue-router";
import HomeView from "@/components/HomeView.vue";
import TheWelcome from "@/components/TheWelcome.vue";

const routes = createRouter({
  history: createWebHashHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: "/",
      name: "home",
      component: HomeView
    },
    {
      path: "/welcome",
      name: "welcome",
      component: TheWelcome
    },
  ]
});

export default routes;
```
![](/images/016_vueRouter/01.png)

### 3. 修改檔案 **main.js**
```
import './assets/main.css'

import router from './router';

import { createApp } from 'vue'
import App from './App.vue'

const app = createApp(App)

app.use(router);

app.mount('#app')

app.config.errorHandler = (err) => {
  console.log('errorHandler', err)
}
```
![](/images/016_vueRouter/02.png)

### 4. 修改 **App.vue**
```
<template>
  <RouterView />
</template>

<script setup lang="ts">
  import { RouterView } from 'vue-router';
</script>
```

### 5. **RouterLink** 使用 **Html** 標籤換頁
```
<template>
  Hello world

  <RouterLink to="/welcome">Welcome</RouterLink>
</template>

<script setup lang="ts">
  import { RouterLink } from 'vue-router';
</script>
```

### 6. **useRouter** 使用 **ts** 換頁
```
<template>
  Hello world
  <button @click="onToChild">Go To Child</button>
</template>

<script setup lang="ts">
  import { useRouter } from 'vue-router';
  const router = useRouter();
  
  const onToChildParam = () => {
    router.push(`/child1`);
  };
</script>
```

### 7. **useRouter** 使用 **ts** 換頁傳值
```
<template>
  Hello world
  <button @click="onToChildParam(2)">Go To Child with param</button>
</template>

<script setup lang="ts">
  import { useRouter } from 'vue-router';
  const router = useRouter();
  
  const onToChildParam = () => {
    router.push(`/child1/${param}`);

    // or
    router.push({ name: 'child1', params: { id: param } });
  };
</script>
```

### 8. **useRoute** 抓取 **url param**
```
<template>
  <button @click="onGetParam">GetParam</button>
</template>

<script setup lang="ts">
  import { useRoute } from 'vue-router';
  const route = useRoute();

  const onGetParam = () => {
    console.log(123, route.params.id);
  };
</script>
```

### 9. 增加 **not found** 頁面
```
<!-- index.ts -->
...
import NotFoundView from "@/components/NotFoundView.vue";

const routes = createRouter({
  history: createWebHashHistory(import.meta.env.BASE_URL),
  routes: [
  ...
  {
    path: "/:catchAll(.*)*",
    name: "not-found",
    component: NotFoundView
    }
  ]
});

export default routes;

<!-- NotFoundView.vue -->
<template>
  <h1>Not found</h1>

  <RouterLink to="/">Go Back</RouterLink>
</template>

<script setup lang="ts">
  import { RouterLink } from "vue-router"
</script>
```
![](/images/016_vueRouter/03.png)

## 參考
[路由](https://cn.vuejs.org/guide/scaling-up/routing "")