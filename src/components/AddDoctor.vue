<template>
  <div class="form">
    <input v-model="name" placeholder="Doctor Name" />
    <input v-model="specialty" placeholder="Specialty" />
    <button @click="handleSave">{{ isEdit ? "Update Doctor" : "Add Doctor" }}</button>
    <button v-if="isEdit" @click="$emit('cancel-edit')">Cancel</button>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  editDoctor: Object
})
const emit = defineEmits(['save-doctor', 'cancel-edit'])

const name = ref('')
const specialty = ref('')
const id = ref(null)
const isEdit = ref(false)

watch(() => props.editDoctor, (newVal) => {
  if (newVal) {
    name.value = newVal.name
    specialty.value = newVal.specialty
    id.value = newVal.id
    isEdit.value = true
  } else {
    name.value = ''
    specialty.value = ''
    id.value = null
    isEdit.value = false
  }
})

function handleSave() {
  if (!name.value || !specialty.value) return
  emit('save-doctor', { id: id.value, name: name.value, specialty: specialty.value })
  name.value = ''
  specialty.value = ''
  id.value = null
  isEdit.value = false
}
</script>

<style>
.form {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 20px;
}

input {
  padding: 8px;
  width: 100%;
}

button {
  padding: 8px;
  cursor: pointer;
}
</style>