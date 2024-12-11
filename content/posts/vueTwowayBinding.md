+++
date = '2024-12-11T16:58:28+08:00'
draft = true
title = 'Vue 雙向綁定'
tags = ['Html', 'Vue', 'TypeScript']
categories = ['Html', 'Vue']
+++

### **Two-way binding** 概念
```
<input 
  :value="text"
  @input="event => text = event.target.value" />
```

### **input**
```
<p>Message is: {{ message }}</p>
<input v-model="message" placeholder="edit me" />
```

### **textarea**
```
<p style="white-space: pre-line;">{{ message }}</p>
<textarea v-model="message" placeholder="add multiple lines"></textarea>
```

### **checkbox**
```
<!-- 單一選項，boolean -->
const checked = ref(false)

<input type="checkbox" id="checkbox" v-model="checked" />
<label for="checkbox">{{ checked }}</label>

<!-- 多選項，array -->
const checkedNames = ref([])

<div>Checked names: {{ checkedNames }}</div>

<input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
<label for="jack">Jack</label>

<input type="checkbox" id="john" value="John" v-model="checkedNames" />
<label for="john">John</label>

<input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
<label for="mike">Mike</label>

<!-- 透過屬性 binding -->
const toggle = ref('no')
const dynamicTrueValue = ref('yes')
const dynamicFalseValue = ref('no')

<input
  type="checkbox"
  v-model="toggle"
  :true-value="dynamicTrueValue"
  :false-value="dynamicFalseValue" />
```

### **radio button**
```
const picked = ref('')

<div>Picked: {{ picked }}</div>

<input type="radio" id="one" value="One" v-model="picked" />
<label for="one">One</label>

<input type="radio" id="two" value="Two" v-model="picked" />
<label for="two">Two</label>

<!-- 透過屬性 binding -->
const pick = ref('2')
const first = ref('1')
const second = ref('2')

<input type="radio" v-model="pick" :value="first" />
<input type="radio" v-model="pick" :value="second" />
```

### **select option**
```
<!-- 單一選項 -->
const selected = ref('')

<div>Selected: {{ selected }}</div>

<select v-model="selected">
  <option disabled value="">Please select one</option>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>

<!-- 多選項 -->
const selected = ref([])

<div>Selected: {{ selected }}</div>

<select v-model="selected" multiple>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>

<!-- for 渲染 -->
const selected = ref('A')

const options = ref([
  { text: 'One', value: 'A' },
  { text: 'Two', value: 'B' },
  { text: 'Three', value: 'C' }
])

<div>Selected: {{ selected }}</div>

<select v-model="selected">
  <option v-for="option in options" :value="option.value">
    {{ option.text }}
  </option>
</select>

<!-- 透過屬性 binding -->
const selected = ref({ value: 123 })

<select v-model="selected">
  <option :value="{ value: 123 }">123</option>
</select>
```

### 修飾語
```
<!-- .lazy change 事件後才會更新 -->
<input v-model.lazy="msg" @change="onChange" />
<div>{{ msg }}</div>

<!-- .number 要有 type="number" -->
<input type="number" v-model.number="age" />
<div>{{ age }}</div>

<!-- .trim -->
<input v-model.trim="msg" />
<div>{{ msg }}</div>
```

## 參考
[Vue.js](https://cn.vuejs.org/guide/essentials/forms.html "")