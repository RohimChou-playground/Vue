project scaffold start by 

```
npm init vue@latest
# choose vue-router only
# enter to the end
del src\components\WelcomeItem.vue & del src\components\TheWelcome.vue & del src\components\HelloWorld.vue
rmdir /s /q src\components\icons
notepad src\views\HomeView.vue # 改成下面
notepad src\views\HomeView.vue # 改成下面 (移除HelloWorld相關的)
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
    <h1>Hello World</h1>
</template>
```

File:HelloWorld.vue
```
<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>
...
...
```