<script setup>
import UserAddition from '~/component/UserAddition.vue';
// import UserValidation from '~/component/UserValidation.vue';

const arrayData = [
  {
    id: 1,
    name: "name",
    placeholder: "Enter name",
    type: "text",
    formName: "signup",
    text: "Enter Name",
  },
  {
    id: 2,
    name: "email",
    placeholder: "Enter email",
    type: "text",
    formName: "signup",
    text: "Enter Email",
  },
  {
    id: 3,
    name: "number",
    placeholder: "Enter number",
    type: "number",
    formName: "signup",
    text: "Enter Number",
  },
  {
    id: 4,
    name: "password",
    placeholder: "Enter password",
    type: "password",
    formName: "signup",
    text: "Enter Password",
  },
];
</script>
<template>
  <div>
    <h1 class="text-5xl">Signup</h1>
    <UserAddition :arrayData="arrayData" />
  </div>
</template>

<style scoped>
h1 {
  margin-top: 80px;
  margin-bottom: 20px;
}
</style>
