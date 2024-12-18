+++
date = '2024-12-18T12:20:11+08:00'
draft = true
title = 'Vue Nuxt3'
tags = ['Html', 'Vue', 'TypeScript', 'Nuxt3']
categories = ['Html', 'Vue']
+++

### 1. 安裝 **Nuxt3**
```
npx nuxi@latest init nuxt-start
```
![](/images/019_vueNuxt3/01.png)

### 2. 切換進專案
```
cd nuxt-start

// 預設 3000
npm run dev

// 修改 port
npm run dev -- -p 5172
```
![](/images/019_vueNuxt3/01.png)

### 3. **build**
```
npx nuxi build
```
![](/images/019_vueNuxt3/02.png)

### 4. **preview**
```
npx nuxi preview
```

## **ESLint**
### 1. 安裝 **ESLint**
```
npm i -D eslint @nuxtjs/exlint-config
```

### 2. 新增一個 **.eslintrc.cjs** 檔
```
module.exports = {
  env: {
    browser: true,
    es2021: true,
  },
  extends: ['@nuxtjs'],
  parserOptions: {
    ecmaVersion: 2023,
    sourceType: 'module',
  },
  plugins: [],
  rules: {
    'no-undef': 'off',
  }
}
```
![](/images/019_vueNuxt3/03.png)

### 安裝 **Tailwind css**
```
npm i -D @nuxtjs/tailwindcss

<!-- nuxt.config.ts -->
export default defineNuxtConfig({
  modules: ['@nuxtjs/tailwindcss'],
  ...
})

<!-- tailwind.config.js -->
module.exports = {
  content: [
    `./components/**/*.{vue,js}`,
    `./layouts/**/*.vue`,
    `./pages/**/*.vue`,
    `./composables/**/*.{js,ts}`,
    `./plugins/**/*.{js,ts}`,
    `./utils/**/*.{js,ts}`,
    `./{App,app}.{js,ts,vue}`,
    `./{Error,error}.{js,ts,vue}`,
    `./app.config.{js,ts}`,
  ],
  theme: {
    extend: {}
  },
  plugins: []
}
```

### 刪除 **npx** 快取
```
npx clear-npx-cache
```

## 參考
[Nuxt3](https://nuxt.com.cn/docs/getting-started/installation "")