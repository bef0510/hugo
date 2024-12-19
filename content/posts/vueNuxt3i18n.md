+++
date = '2024-12-19T12:27:21+08:00'
draft = true
title = 'Vue Nuxt3 i18n'
tags = ['Html', 'Vue', 'TypeScript', 'Nuxt3']
categories = ['Html', 'Vue']
+++

### 1. 安裝 **i18n**
```
npm install -D @nuxtjs/i18n@next
```

### 2. 修改 **nuxt.config.ts**
```
export default defineNuxtConfig({
  modules: [
    '@nuxtjs/tailwindcss',
    ...
    '@nuxtjs/i18n'
  ],
  compatibilityDate: '2024-11-01',
  devtools: { enabled: true },
  i18n: {
    langDir: 'locales',
    locales: [
      { code: 'en', iso: 'en-US', file: 'en.json' },
      { code: 'zh', iso: 'zh-TW', file: 'zh.json' }
    ],
    defaultLocale: 'zh'
  }
})
```


## 參考
[Nuxt3](https://nuxt.com/modules/i18n "")