<script setup>
import { defineProps, ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const props = defineProps(["arrayData"]);
const arrayData = props.arrayData;

let inputValues = {};
arrayData.forEach((input) => {
  inputValues[input.name] = ref("");
  // console.log(input.name)
});
// console.log(inputValues)

const submittedData = {};

const handleFormSubmit = () => {
    if (arrayData[0].formName === "login") {
    return validateUser();
  }
  for (const [key, value] of Object.entries(inputValues)) {
    submittedData[key] = value.value;
  }
  // console.log(submittedData)
  // Save submitted data to Local Storage
  let localData = JSON.parse(localStorage.getItem(arrayData[0].formName));
  if (!localData) {
    localData = [];
  }
  //console.log("localdata" + localData)
  localData.push(submittedData);
  console.log(localData);
  localStorage.setItem(arrayData[0].formName, JSON.stringify(localData));
  alert("Signedup Succesfully");
  // console.log(submittedData);
  router.push("/login");
};
const validateUser = () => {
  let userData = JSON.parse(localStorage.getItem("signup")) || [];
  const email = inputValues["email"].value;
  const password = inputValues["password"].value;
  let user = null;
  userData.forEach((item) => {
    if (item.email === email && item.password === password) {
      user = item;
      return;
    }
  });

  if (user) {
    console.log("user exist");
    console.log(user);
    // navigateTo("/");
    alert("welcome");
    router.push("/employee")
  } else {
    console.log("user does not exist");
    alert("user does not exist");
  }
};
</script>
<style></style>
<template>
  <form @submit.prevent="handleFormSubmit" class="form_containe">
    <div v-for="data in arrayData" :key="data.id" class="inputbox">
      <span class="ml-4 text-sm">
        {{ data.text }}
      </span>
      <input
        :type="data.type"
        :placeholder="data.placeholder"
        v-model="inputValues[data.name].value"
      />
    </div>
    <button class="form_submit">Submit</button>
  </form>
</template>

<style>
.inputbox {
  width: 300px;
}

h1 {
  text-align: center;
  color: black;
}

.form_containe {
  display: flex;
  gap: 20px;
  flex-direction: column;
  height: 40rem;
  justify-content: center;
  align-items: center;
  margin: auto;
  border: 1px solid black;
  width: 400px;
  border-radius: 10px;
}

.form_containe input {
  font-size: large;
  padding: 0.5rem 1rem;
  outline: none;
  border-radius: 10px;
}

.form_submit {
  padding: 0.3rem 0.5rem;
  outline: none;
  width: 100px;
  height: 40px;
  border-radius: 10px;
  /* background-color: grey; */
  border: 1px solid teal;
}

.form_submit:hover {
  background-color: teal;
}
</style>
