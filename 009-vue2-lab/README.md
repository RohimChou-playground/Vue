project scaffold start by 

```
npm i @vue/cli
npx vue create 009-vue2-lab
  Manually select features
  only choose Router
  choose vue 2.x
  Use history mode? Y
  In dedicated config file
  use NPM
更新 HelloWorld.vue 成下面
移除 HomeView.vue 裡的 <img alt="Vue logo" src="../assets/logo.png">
cd 009-vue2-lab
npm run serve
```

components/HelloWorld.vue
```
<template>
    <h1>{{ msg }}</h1>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    msg: 'Hello World'
  },
}
</script>
```