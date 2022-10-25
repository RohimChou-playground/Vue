<script setup>
import { RouterLink, RouterView } from 'vue-router'
import { useRouter } from 'vue-router'
let route = useRouter();

// Note: Inside of a Vue instance, you have access to the router instance as $router. 
// You can therefore call this.$router.push.
function test_default() {
  route.push({ path: '/test' });
}

function test_query() {
  route.push({ path: '/test', query: { userName: 'John' } });
}

// 'path' cannot be used with params, params would be ignored
// Changed on this version: https://github.com/vuejs/router/blob/main/packages/router/CHANGELOG.md#414-2022-08-22
// 
function test_params() {
  route.push({ name: 'test', params: { userName: 'John' } });
}

function test_hist_state() {
  route.push({ name: 'test', state: { userName: 'John' } });
}
</script>

<template>
  <header>
    <div class="wrapper">
      <button @click="test_default">Test</button>
      <button @click="test_query">Test With Query Url Params</button>
      <button @click="test_params">Test With Params</button>
      <button @click="test_hist_state">Test With Hitory State</button>
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
button {
  margin-right: 10px;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
