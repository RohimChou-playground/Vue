<script setup>
import { Form, Field, ErrorMessage } from 'vee-validate'
import AllRules from '@vee-validate/rules'
import { defineRule, configure } from 'vee-validate'
import { computed, ref, onUpdated } from "vue";
import { setLocale, localize } from '@vee-validate/i18n';

// import rules
Object.keys(AllRules).forEach(rule => {
  defineRule(rule, AllRules[rule]);
});

defineRule('positive', (value, limits, event) => {
  console.log(value, limits, event);
  if (value !== undefined) {
    return value >= 1 ? true : '必須是正數';
  } else {
    return true;
  }
});

configure({
  generateMessage: localize('zh_TW', {
    messages: {
      required: '必填欄位',
    },
  })
});

setLocale('zh_TW');

// Default values
configure({
  validateOnBlur: false,
  validateOnChange: false,
  validateOnInput: false,
  validateOnModelUpdate: false,
});


// Data
const data = ref({ brands: ['addidas', 'nike' ], selected: "1" });
onUpdated(() => {
  console.log("AAAA");
  console.log(data.value.selected);
});

const mySubmit = (formValues) => {
  console.log("mySubmit");
  console.log(formValues);
}

const myInvalidSubmit = (formValues) => {
  console.log("myInvalidSubmit, focus on first error");
  const { errors, evt, results, values } = formValues;

  const inputs = evt.target.querySelectorAll('input, select');
  for (const input of inputs) {
    if (errors[input.name] !== undefined) {
      input.focus();
      return;
    }
  }
}
</script>

<template>
  <main>
    <div id="div1">
      Form1 {{data.selected}}
      <Form v-slot="{ handleSubmit }" as="div" @invalid-submit="myInvalidSubmit">
        <form @submit="handleSubmit($event, mySubmit)" ref="myForm">
          <label for="username">UserName: </label>
          <Field type="text" name="username" rules="required"></Field>
          <ErrorMessage style="color:red" name="username"></ErrorMessage>

          <label for="birthyear">BirthYear: </label>
          <Field type="number" name="birthyear" rules="positive:abc"></Field>
          <ErrorMessage style="color:red" name="birthyear"></ErrorMessage>

          <Field name="field" as="select" v-model="data.selected">
            <option value="1">Coffee</option>
            <option value="2">Tea</option>
            <option value="3">Coke</option>
          </Field>
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