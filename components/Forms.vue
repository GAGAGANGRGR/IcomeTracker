<template>
  <form @submit.prevent="FormHandler">
    <div v-for="(field, index) in inputData" :key="index">
      <input :type="field.type" :placeholder="field.placeholder" v-model="field.value" />
    </div>
    <input type="submit" value="Submit" />
  </form>
</template>


<script setup>
const formData = ref({})

const props = defineProps({
  inputData: "Object"
})
const emits = defineEmits(['formdata'])

const FormHandler = () => {
  props.inputData.forEach(field => {
    formData.value[field.var] = field.value;
  });

  // Clear form fields
  props.inputData.forEach(field => {
    field.value = '';
  });

  emits("formdata", formData.value)
};
</script>




<style scoped>
form {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

form input {
  color: #888;
  border: none;
  outline: none;
  font-size: 20px;
}

form input::placeholder {
  color: #AAA;
}

form input:not([type="submit"]) {
  display: block;
  background: #FFF;
  border: none;
  outline: none;
  padding: 5px 15px;
}

form input[type="submit"] {
  display: block;
  background: none;
  border: none;
  outline: none;

  color: #FFF;
  font-weight: 500;
  text-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
  padding: 5px 15px;
  background-color: #FFCE00;

  cursor: pointer;
}

form input:first-of-type {
  border-radius: 8px 0px 0px 8px;
}

form input:last-of-type {
  border-radius: 0px 8px 8px 0px;
}
</style>