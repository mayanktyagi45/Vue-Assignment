<template>
  <main>
    <table class="dataTable">
      <thead class="tableHead">
        <tr class="tableRow">
          <th class="rowHeading">Topic</th>
          <th class="rowHeading">Content</th>
          <th class="rowHeading">Duration</th>
        </tr>
      </thead>
      <tbody v-for="(data, index) in formData" :key="index" class="tableBody">
        <tr class="tableRow">
          <td class="tableColumn">{{ data.topic }}</td>
          <td class="tableColumn">{{ data.content }}</td>
          <td class="tableColumn">{{ data.duration }} Days</td>
        </tr>
      </tbody>
    </table>
  </main>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const formData = ref([]);

onMounted(() => {
  const storedData = JSON.parse(localStorage.getItem('formData'));
  if (Array.isArray(storedData)) {
    formData.value = storedData;
  }
});
</script>

<style scoped>
.dataTable {
  border-collapse: collapse;
  margin-top: 2rem;
  width: 100%;
}

.dataTable tr:not(:last-child) {
  border-bottom: 0.0625rem solid #e8e7e7;
}

.dataTable tr td:not(:last-child) {
  border-left: 0.0625rem solid #e8e7e7;
}

.dataTable tr:first-child th:first-child {
  border-top-right-radius: 0.5rem;
}

.dataTable tr:first-child th:last-child {
  border-top-left-radius: 0.5rem;
}

.dataTable tr:last-child td:first-child {
  border-bottom-right-radius: 0.5rem;
}

.dataTable tr:last-child td:last-child {
  border-bottom-left-radius: 0.5rem;
}

.rowHeading, .tableColumn {
  padding: 1rem;
  text-align: center;
}

.tableRow .rowHeading {
  font-size: 0.875rem;
  font-weight: 500;
  color: #fff;
  background-color: #0066ff;
}

.tableBody tr:nth-child(odd) {
  background-color: #fff;
}

.tableBody tr:nth-child(even) {
  background-color: #f8f8f8;
}
</style>
