<template>
  <div>
    <div v-for="doctor in doctors" :key="doctor.id" class="card">
      <p><strong>{{ doctor.name }}</strong></p>
      <p>{{ doctor.specialty }}</p>
      <button @click="$emit('edit', doctor)">Edit</button>
      <button @click="$emit('delete', doctor.id)">Delete</button>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  doctors: Array
})
const emit = defineEmits(['edit', 'delete'])
</script>

<style>
.card {
  border: 1px solid #ddd;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
}

button {
  margin: 5px 5px 0 0;
  padding: 5px;
  cursor: pointer;
}
</style>