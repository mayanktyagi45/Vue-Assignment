<template>
  <main class="modal">
    <form class="addData">
      <label for="topic">
        <input type="text" class="formInput" required placeholder="Topic" v-model="topic" />
      </label>

      <label for="content" required>
        <input type="text" class="formInput"  placeholder="Content" v-model="content" />
      </label>

      <label for="duration" required>
        <input type="number" class="formInput"  placeholder="Duration" v-model="duration" />
      </label>
      <button class="submit" @click="handleSubmit">Submit</button>
    </form>
  </main>
</template>
<script setup>
import { ref } from 'vue';

const topic = ref('');
const content = ref('');
const duration = ref(null);
const existingData = ref([]);

const handleSubmit = (e) => {
  e.preventDefault();

  const newData = {
    topic: topic.value,
    content: content.value,
    duration: duration.value,
  };

  const storedData = JSON.parse(localStorage.getItem('formData'));
  if (Array.isArray(storedData)) {
    existingData.value = storedData;
  } else {
    existingData.value = [];
  }

  existingData.value.push(newData);
  localStorage.setItem('formData', JSON.stringify(existingData.value));

  topic.value = '';
  content.value = '';
  duration.value = null;

  console.log(localStorage.getItem('formData'));
};
</script>

<style scoped>

.addData {
  display: flex;
  justify-content: center;
}

.formInput {
  background: #e4e5e7;
  border: none;
  font-size: 0.9375rem;
  outline: none;
  padding: 0.625rem;
  width: 75%;
}

.modal {
  background: white;
  border: 0.0625rem solid black;
  border-radius: 0.625rem;
  margin-top: 1rem;
  padding: 1.25rem;
}

.submit {
  background: #0b6dff;
  border: 0;
  border-radius: 1.25rem;
  color: white;
  padding: 0.625rem 1.25rem;
}

</style>
