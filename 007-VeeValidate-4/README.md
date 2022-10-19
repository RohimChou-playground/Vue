project scaffold start by 

```
npm init vue@latest
# choose vue-router only
# enter to the end
del src\components\WelcomeItem.vue
del src\components\TheWelcome.vue
rmdir /s /q src\components\icons
notepad src\views\HomeView.vue # 改成下面
npm install vee-validate@4.7.0
npm install @vee-validate/rules@4.7.0
npm install
npm run dev
```

File:HomeView.vue
```
<script setup>
</script>

<template>
  <main>
    <h1>Hello World</h1>
  </main>
</template>
```