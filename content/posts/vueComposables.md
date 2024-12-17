+++
date = '2024-12-17T16:03:58+08:00'
draft = true
title = 'Vue Composables 共用邏輯'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

### 新增資料夾 **src → Composables → useWindowPosition.js**
```
<!-- useWindowPosition.js -->
import { onMounted, onUnmounted, ref } from 'vue';

export function useWindowPosition() {
  const pageX = ref(0);
  const pageY = ref(0);

  const movePosition = (e) => {
    pageX.value = e.pageX;
    pageY.value = e.pageY;
  };

  onMounted(() => {
    window.addEventListener('mousemove', movePosition);
  });

  onUnmounted(() => {
    window.removeEventListener('mousemove', movePosition);
  });

  return {
    pageX,
    pageY
  };
}

-------------------------------------
<!-- 呼叫 vue -->

<template>
  <h1> pageX : {{ pageX }}</h1><br />
  <h1> pageY : {{ pageY }}</h1>
</template>

<script setup lang="ts">
  import { useWindowPosition } from '@/Composables/useWindowPosition.js';

  const { pageX, pageY } = useWindowPosition();
</script>
```
![](/images/018_vueComposables/01.png)

### 基本用法一
```
<!-- useSetData.js -->

import { ref } from "vue";

export function useSetData() {
  const count = ref(0);

  const addCount = () => {
    count.value++;
  };

  return { 
    count, 
    addCount 
  };
}

-------------------------------------
<!-- 呼叫 vue -->

<template>
  <h1>{{ count }}</h1>
  <button @click="addCount">Add Count</button>
</template>

<script setup lang="ts">
  import { useSetData } from '@/Composables/useSetData.js';

  const { count, addCount } = useSetData();
</script>
```

### 仿 **react hook**
```
<!-- useSetData.js -->

import { ref } from "vue";

export function useSetData(val) {
  const text = ref(val);

  const setDalue = (vl) => {
    text.value = vl;
  };

  return { 
    text, 
    setDalue 
  };
}

-------------------------------------
<!-- 呼叫 vue -->

<template>
  <h1>{{ text }}</h1>
  <button @click="setDalue(text++)">set Value</button>
</template>

<script setup lang="ts">
  import { useSetData } from '@/Composables/useSetData.js';

  const { text, setDalue } = useSetData(0);
</script>
```

### **call API**
```
<!-- useFetchCard.js -->

import axios from 'axios';
import { ref } from "vue";

export function useFetchCard() {

  const data = ref([]);
  const errorMessga = ref("");

  const fetchInit = async () => {
    try {
      const res = await axios.get('https://60bd9841ace4d50017aab3ec.mockapi.io/api/post_card')
      data.value = res.data;
    } catch (err) {
      errorMessga.value = "Api error";
    }	
  };

  return {
    data,
    errorMessga,
    fetchInit
  };
}

-------------------------------------
<!-- 呼叫 vue -->

<template>
  <h1 v-if="data.length === 0">loading ...</h1>
  
  <div v-else>
    <pre>{{ data }}</pre>
  </div>

  <div v-if="errorMessga">
    {{ errorMessga }}
  </div>
</template>

<script setup lang="ts">
  import { useFetchCard } from '@/Composables/useFetchCard.js';

  const { data, errorMessga, fetchInit } = useFetchCard();

  onMounted(() => {
    fetchInit();
  });

import { onMounted } from 'vue';
  
</script>
```

## 參考
[Composables](https://vuejs.org/guide/reusability/composables "")