<script setup>
import { ref, onMounted } from "vue";
import FormComponent from "~/component/FormComponent.vue";

const employeeArray = [
  {
    name: "name",
    type: "text",
    placeholder: "Enter Name",
    text: "Enter Name",
    value: "",
  },
  {
    name: "age",
    type: "number",
    placeholder: "Enter Age",
    text: "Enter Age",
    value: "",
  },
  {
    name: "gender",
    type: "select",
    selectedArray: ["male", "female"],
    placeholder: "Select Gender",
    value: "",
  },
  {
    name: "dateofjoining",
    type: "date",
    value: "",
  },
  {
    name: "designation",
    type: "text",
    placeholder: "Designation",
    text: "Designation",
    value: "",
  },
];

const showForm = ref(false);
const showEditForm = ref(false);
const editIndex = ref(null);
const editValues = ref([]);

const toggleForm = () => {
  showEditForm.value = false;
  showForm.value = !showForm.value;
};

const getEmployee = ref([]);
console.log(getEmployee);

onMounted(() => {
  getEmployee.value = JSON.parse(localStorage.getItem("employee Data")) || [];
});

// for creating ---------------------------------------------------------
const handleSubmit = (data) => {
  getEmployee.value.push(data);
  localStorage.setItem("employee Data", JSON.stringify(getEmployee.value));
};

// for deleting ---------------------------------------------------------
const deleteEmployee = (index) => {
  getEmployee.value.splice(index, 1);
  localStorage.setItem("employee Data", JSON.stringify(getEmployee.value));
};

// for editing ---------------------------------------------------------
// to edit the value
const editEmployee = (employee, index) => {
  showForm.value = false;
  showEditForm.value = !showEditForm.value;
  editIndex.value = index;
  editValues.value = [];
  const newArray = JSON.parse(JSON.stringify(employeeArray));

  editValues.value = newArray.map((item) => {
    item.value = employee[item.name];
    return item;
  });
};

// will run on submitting the data from the component
const handleEditEmployeeSubmit = (employee) => {
  getEmployee.value[editIndex.value] = employee;
  localStorage.setItem("employee Data", JSON.stringify(getEmployee.value));
  editValues.value = [];
  showForm.value = false;
  showEditForm.value = false;
};

const searchQuery = ref("");
const searchedFilteredEmployee = ref([]);

const handleSearch = () => {
  if (searchQuery.value.trim() === "") {
    // If the search query is empty, show all employees
    searchedFilteredEmployee.value = [...getEmployee.value];
  } else {
    // Otherwise, filter the employees based on the search query
    searchedFilteredEmployee.value = getEmployee.value.filter((el) => {
      return el.name.toLowerCase().includes(searchQuery.value.toLowerCase());
    });
  }
};

// Watch for changes in the search query
watchEffect(() => {
  handleSearch();
});
</script>

<template>
  <p class="mt-4 text-xl ml-4">Search Employee</p>
  <input
    type="text"
    class="appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline mt-2"
    placeholder="Enter Name"
    v-model="searchQuery"
    @input="handleSearch"
  />

  <h1 class="text-2xl mt-4">Employee Details</h1>
  <div class="flex flex-col items-center mt-4 h-screen">
    <button class="addbutton" @click="toggleForm">Add Employee</button>
    <!-- component to create an employee -->
    <FormComponent
      v-if="showForm"
      :employeeArray="employeeArray"
      :handleSubmit="handleSubmit"
    />
    <!-- component to edit an employee -->
    <FormComponent
      v-if="showEditForm"
      :employeeArray="editValues"
      :handleSubmit="handleEditEmployeeSubmit"
    />
  </div>

  <div class="formbox">
    <div v-if="!showForm && !showEditForm">
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
          <tr
            v-for="(employee, index) in searchedFilteredEmployee"
            :key="index"
          >
            <td class="border p-2">{{ employee.name }}</td>
            <td class="border p-2">{{ employee.age }}</td>
            <td class="border p-2">{{ employee.gender }}</td>
            <td class="border p-2">{{ employee.dateofjoining }}</td>
            <td class="border p-2">{{ employee.designation }}</td>
            <td class="border p-2">
              <button
                @click="editEmployee(employee, index)"
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
.formbox {
  margin-top: -600px;
}
.addbutton {
  background-color: teal;
  color: #ffffff;
  padding: 0.5rem 1rem;
  font-size: 0.875rem;
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;
}
</style>
