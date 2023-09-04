<template>
  <main class="container">
    <button @click="toggleModal" class="addContent">{{ buttonTitle }}</button>
    <section v-if="showModal">
      <ContentModal />
    </section>
    <DataTable />
    <section v-if="hasData()">
      <button class="deleteButton" type="submit" @click="handleDelete">Delete</button>
    </section>
  </main>
</template>

<script setup>
import { ref } from 'vue';
import ContentModal from './ContentModal.vue';
import DataTable from './DataTable.vue';

const showModal = ref(false);
const buttonTitle = ref('Add Content');

const toggleModal = () => {
  console.log('clicked');
  showModal.value = !showModal.value;
  if (!showModal.value) {
    buttonTitle.value = 'Add Content';
  } else {
    buttonTitle.value = 'Close Modal';
  }
};

const hasData = () => localStorage.getItem('formData') !== null;

const handleDelete = () => {
  console.log('Deleted');
  localStorage.clear();
};
</script>

<style scoped>
.addContent {
  background: #58b558;
  border: 0;
  border-radius: 1.25rem;
  color: white;
  padding: 0.625rem 1.25rem;
}

.container {
  background-color: #ffffff;
  border-radius: 0.625rem;
  margin: 1rem;
  padding: 1.25rem;
}

.deleteButton {
  background-color: #ec5757;
  border: none;
  border-radius: 1rem;
  color: #ffffff;
  cursor: pointer;
  height: auto;
  padding: 1rem;
  position: relative;
  overflow: hidden;
  width: 10rem;
}
</style>
