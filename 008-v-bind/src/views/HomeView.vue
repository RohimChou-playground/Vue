<script setup>
import { ref } from 'vue';
const msg = ref('Hello World')

const updateMsg = (e) => {
  msg.value = e.target.value;
}
</script>

<template>
    <h1 v-bind:aaa="msg">{{ msg }}</h1>
    <input type="text" v-bind:value="msg" @input="updateMsg" />
</template>