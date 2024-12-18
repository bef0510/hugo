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
const routes = createRouter({
  history: createWebHashHistory(import.meta.env.BASE_URL),
  routes: [
  ...
  {
    path: "/:catchAll(.*)*",
    name: "not-found",
    component: import("../components/NotFoundView.vue")
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

### 10. 子路由
```
<!-- index.ts -->
import { createRouter, createWebHashHistory } from "vue-router";
import HomeView from "@/components/HomeView.vue";
import AboutView from "@/views/AboutView.vue";
import a from "@/views/about/a.vue";
import b from "@/views/about/b.vue";
import c from "@/views/about/c.vue";

const routes = createRouter({
  history: createWebHashHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: "/",
      name: "home",
      component: HomeView
    },
    {
      path: "/about",
      name: "about",
      component: AboutView,
      children: [
        {
          path: "a",
          component: a
        },
        {
          path: "b",
          component: b
        },
        {
          path: "c",
          component: c
        }
      ]
    },
    {
      path: "/:catchAll(.*)*",
      name: "not-found",
      component:  () => import("../views/NotFoundView.vue"),
    }
  ]
});

export default routes;

-------------------------------------
<!-- 呼叫 vue -->

<template>
  <nav>
    <RouterLink to="/about/a">a</RouterLink>
    <RouterLink to="/about/b">b</RouterLink>
    <RouterLink to="/about/c">c</RouterLink>

    <RouterView />
  </nav>
</template>

<script setup lang="ts">
  import { RouterLink, RouterView } from 'vue-router';
</script>
```

### **useRoute、useRouter** 差異
```
seRoute 抓取網址參數
useRouter 網址動作

<!-- 換頁，會記鍵上一次頁面 -->
router.push('/about/a');

<!-- 換頁，不會記鍵上一次頁面，大多有參數時使用 -->
router.replace('/about/a');
```

### **history** 改使用 **createWebHashHistory**
```
<!-- index.ts -->

...
history: createWebHashHistory(),
...
```

## 參考
[路由](https://cn.vuejs.org/guide/scaling-up/routing "")