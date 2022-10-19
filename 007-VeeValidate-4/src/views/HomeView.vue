<script setup>
import { Form, Field, ErrorMessage } from 'vee-validate'
import AllRules from '@vee-validate/rules'
import { defineRule } from 'vee-validate'
import { configure } from 'vee-validate';

// import rules
Object.keys(AllRules).forEach(rule => {
  defineRule(rule, AllRules[rule]);
});

// Default values
configure({
  validateOnBlur: false,
  validateOnChange: false,
  validateOnInput: false,
  validateOnModelUpdate: false,
});

const mySubmit = () => {
  console.log("AAAAAA");
}
</script>

<template>
  <main>
    <div id="div1">
      Form1
      <Form @submit="mySubmit()">
        <label for="username">UserName: </label>
        <Field type="text" name="username" rules="required"></Field>
        <ErrorMessage style="color:red" name="username"></ErrorMessage>

        <label for="birthyear">BirthYear: </label>
        <Field type="text" name="birthyear" v-slot="abc">
          {{ debugger }}
        </Field>

        <button id="btn1">this will submit</button>
        <button id="btn2" type="button">this won't</button>
      </Form>
    </div>
  </main>
</template>


<style>
div {
  padding: 10px;
}

#div1 {
  background-color: lightpink;
}

form {
  display: flex;
  flex-direction: column;
}

button {
  width: 150px;
}
</style>