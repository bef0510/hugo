+++
date = '2024-12-12T08:48:25+08:00'
draft = true
title = 'Vue 生命週期'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

![](/images/011_vueLifeCycleHook/01.png)
![](/images/011_vueLifeCycleHook/02.png)
```
<script setup lang="ts">
import { ref,  
  onBeforeMount, onMounted, onBeforeUpdate, onUpdated,
  onBeforeUnmount, onUnmounted
 } from 'vue'

console.log('setup')

onBeforeMount(() => {
  console.log('onBeforeMount')
})

onMounted(() => {
  console.log('onMounted')
})

onBeforeUpdate(() => {
  console.log('onBeforeUpdate')
})

onUpdated(() => {
  console.log('onUpdated')
})

onBeforeUnmount(() => {
  console.log('onBeforeUnmount')
})

onUnmounted(() => {
  console.log('onUnmounted')
})
</script>
```
![](/images/011_vueLifeCycleHook/03.png)

## 監聽 Watch
### 監聽一個 ref
```
import { ref, watch } from 'vue'

const question = ref('')
const answer = ref('Questions usually contain a question mark. ;-)')
const loading = ref(false)

watch(question, async (newQuestion, oldQuestion) => {
  if (newQuestion.includes('?')) {
    loading.value = true;
    answer.value = 'Thinking...';

    setTimeout(()=>{
      loading.value = false;
      answer.value = '';
    }, 1000);
  }
})

<p>Ask a yes/no question:
  <input v-model="question" :disabled="loading" />
</p>
<p>{{ answer }}</p>
```

### 監聽數據源類型 (不能監聽一個 object ex： reactive({}))
```
import { ref, watch } from 'vue'

const x = ref(0)
const y = ref(0)

// 單個來源
watch(x, (newX) => {
  console.log(`x is ${newX}`, x.value)
})

// getter 函式
watch(
  () => x.value + y.value,
  (sum) => {
    console.log(`sum of x + y is: ${sum}`)
  }
)

// 多個來源
watch([x, () => y.value], ([newX, newY]) => {
  console.log(`x is ${newX} and y is ${newY}`)
})
```

### 監聽 即時回傳
```
watch(
  source,
  (newValue, oldValue) => {
    // 立即執行，且 source 改變時，再次執行
  },
  { immediate: true }
)
```

### 監聽 一次性
```
watch(
  source,
  (newValue, oldValue) => {
    // source 改變時，只執行一次
  },
  { once: true }
)
```

### 監聽 變數執行一次後，尚未完成，變數再執行時，停止前一次
```
import { ref, watch, onWatcherCleanup } from 'vue'

const id = ref('')
const data = ref(null)

watch(id, (newId) => {
  const controller = new AbortController()

  fetch(`/api/${newId}`, { signal: controller.signal }).then(() => {
    
  })

  onWatcherCleanup(() => {
    // 終止未完成的請求
    controller.abort()
  })
})
```

### 監聽 停止
```
// 自動停止
watchEffect(() => {})

// 手動停止
const unwatch = watchEffect(() => {})
unwatch()
```

## 參考
[Vue.js](https://cn.vuejs.org/api/composition-api-lifecycle#onmounted "")