<template>
  <div class="container">
    <h1>Doctor Management App</h1>
    <AddDoctor 
      :edit-doctor="editDoctorData" 
      @save-doctor="saveDoctor" 
      @cancel-edit="cancelEdit"
    />
    <DoctorList 
      :doctors="doctors" 
      @edit="editDoctor" 
      @delete="deleteDoctor"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import DoctorList from './components/DoctorList.vue'
import AddDoctor from './components/AddDoctor.vue'

const doctors = ref([
  { id: 1, name: "Dr. John", specialty: "Cardiology" },
  { id: 2, name: "Dr. Sara", specialty: "Dermatology" }
])

const editDoctorData = ref(null)

function saveDoctor(doctor) {
  if (doctor.id) {
    const existing = doctors.value.find(d => d.id === doctor.id)
    existing.name = doctor.name
    existing.specialty = doctor.specialty
  } else {
    doctor.id = Date.now()
    doctors.value.push(doctor)
  }
  editDoctorData.value = null
}

function editDoctor(doctor) {
  editDoctorData.value = { ...doctor }
}

function cancelEdit() {
  editDoctorData.value = null
}

function deleteDoctor(id) {
  doctors.value = doctors.value.filter(d => d.id !== id)
}
</script>

<style>
body {
  font-family: Arial, sans-serif;
}

.container {
  max-width: 400px;
  margin: auto;
  text-align: center;
}

h1 {
  margin-bottom: 20px;
}
</style>