<script setup>
import { Form, Field, ErrorMessage } from 'vee-validate'
import AllRules from '@vee-validate/rules'
import { defineRule } from 'vee-validate'
import { configure } from 'vee-validate';
import { computed, ref } from "vue";

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

const mySubmit = (formValues) => {
  console.log("mySubmit");
  console.log(formValues);
}

const myInvalidSubmit = (formValues) => {
  console.log("myInvalidSubmit, focus on first error");
  console.log(formValues);
  const { errors, evt, results, values } = formValues;

  const inputs = evt.target.querySelectorAll('input, select');
  for (const input of inputs) {
    if (errors[input.name] !== undefined) {
      console.log(input.name);
      input.focus();
      return;
    }
  }
}
</script>

<template>
  <main>
    <div id="div1">
      Form1
      <Form v-slot="{ handleSubmit }" as="div" @invalid-submit="myInvalidSubmit">
        <form @submit="handleSubmit($event, mySubmit)" ref="myForm">
          <label for="username">UserName: </label>
          <Field type="text" name="username" rules="required"></Field>
          <ErrorMessage style="color:red" name="username"></ErrorMessage>

          <label for="birthyear">BirthYear: </label>
          <Field type="number" name="birthyear" rules="required|between:1,50"></Field>
          <ErrorMessage style="color:red" name="birthyear"></ErrorMessage>

          <button id="btn1">this will submit</button>
          <button id="btn2" type="button">this won't</button>
        </form>
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