<script setup>
import FormComponent from "~/component/FormComponent.vue";

const employeeArray = [
  {
    name: "name",
    type: "text",
    placeholder: "Enter Name",
    text: "Enter Name",
  },
  {
    name: "age",
    type: "number",
    placeholder: "Enter Age",
    text: "Enter Age",
  },
  {
    name: "gender",
    type: "select",
    selectedArray: ["male", "female"],
    placeholder: "Select Gender",
  },
  {
    name: "dateofjoining",
    type: "date",
  },
  {
    name: "designation",
    type: "text",
    placeholder: "Designation",
    text: "Designation",
  },
];
const getEmployee = ref([]);

onMounted(() => {
  getEmployee.value = JSON.parse(localStorage.getItem("employee Data")) || [];
});

const handleSubmit = (data) => {
  getEmployee.value.push(data);
  localStorage.setItem("employee Data", JSON.stringify(getEmployee.value));
};

const deleteEmployee = (index) => {
  getEmployee.value.splice(index, 1);
  localStorage.setItem("employee Data", JSON.stringify(getEmployee.value));
};
</script>

<template>
  <div class="flex flex-col items-center mt-4 h-screen">
    <h1 class="text-2xl">Employee Form</h1>
    <FormComponent
      :employeeArray="employeeArray"
      :handleSubmit="handleSubmit"
    />
  </div>
  <div class="formbox">
    <!-- v-if="getEmployee.length > 0" -->
    <div>
      <table class="w-full text-center border-collapse">
        <thead>
          <tr>
            <th class="border p-2">Name</th>

            <th class="border p-2">Age</th>

            <th class="border p-2">Gender</th>

            <th class="border p-2">Date of Joining</th>

            <th class="border p-2">Designation</th>

            <th class="border p-2">Action</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="(employee, index) in getEmployee" :key="index">
            <td class="border p-2">{{ employee.name }}</td>

            <td class="border p-2">{{ employee.age }}</td>

            <td class="border p-2">{{ employee.gender }}</td>

            <td class="border p-2">{{ employee.dateofjoining }}</td>

            <td class="border p-2">{{ employee.designation }}</td>

            <td class="border p-2">
              <button
                @click="editEmployee(employee)"
                class="bg-blue-500 text-white px-2 py-1 rounded mr-2"
              >
                Edit
              </button>

              <button
                @click="deleteEmployee(index)"
                class="bg-red-500 text-white px-2 py-1 rounded"
              >
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.formbox{
    /* border: 1px solid red; */
    margin-top: -600px;
}
</style>
