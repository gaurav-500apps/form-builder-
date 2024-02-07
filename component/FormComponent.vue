<script setup>
const props = defineProps(["employeeArray", "handleSubmit"]);
const employeeArray = props.employeeArray;
const inputValues = ref({});

// to prefill the inputValues to show inside the v-model for editing them
const fillValuesForEdit = () => {
  employeeArray.forEach((element) => {
    inputValues.value[element.name] = element.value;
  });
};
fillValuesForEdit();

const handleFormSubmit = () => {
  props.handleSubmit({ ...inputValues.value });
};
</script>

<template>
  <form class="custom-form" @submit.prevent="handleFormSubmit">
    <div v-for="data in employeeArray" :key="data.id" class="form-group">
      <label class="form-label">{{ data.handleFormSubmittext }}</label>
      <select
        v-if="data.type === 'select'"
        v-model="inputValues[data.name]"
        required
      >
        <option v-for="item in data.selectedArray" :value="item">
          {{ item }}
        </option>
      </select>
      <input
        v-else
        :type="data.type"
        :placeholder="data.placeholder"
        class="form-input"
        v-model="inputValues[data.name]"
        required
      />
    </div>
    <button class="btn" type="submit">Submit</button>
  </form>
</template>

<style scoped>
.custom-form {
  max-width: 20rem;
  margin: 0 auto;
  background-color: #ffffff;
  padding: 1rem;
  border-radius: 0.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.form-group {
  margin-bottom: 0.4rem;
}

.form-label {
  font-size: 0.875rem;
  color: #333333;
  margin-bottom: 0.25rem;
}

.form-input {
  width: 100%;
  padding: 0.5rem;
  font-size: 0.875rem;
  border: 1px solid #cccccc;
  border-radius: 0.25rem;
}

.btn {
  background-color: #007bff;
  color: #ffffff;
  padding: 0.5rem 1rem;
  font-size: 0.875rem;
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;
}

.btn:hover {
  background-color: #0056b3;
}
</style>
