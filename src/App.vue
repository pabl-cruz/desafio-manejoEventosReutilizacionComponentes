<script>
import RegisterForm from './components/RegisterForm.vue'
import ConsultCard from './components/ConsultCard.vue'

export default {
  components: {
    RegisterForm,
    ConsultCard
  },
  data() {
    return {
      patients: []
    }
  },
  methods: {
    addPatient(patient) {
      this.patients.push(patient)
    },
    deletePatient(id) {
      this.patients = this.patients.filter((patient) => patient.id !== id)
    }
  }
}
</script>

<template>
  <RegisterForm @add-patient="addPatient" />
  <section class="consults">
    <div v-for="(patient, index) in patients" :key="patient.id">
      <ConsultCard :patient="patient" :id="index" @remove-patient="deletePatient" />
    </div>
  </section>
</template>

<style scoped>
.consults {
  display: flex;
  flex-direction: row;
}
</style>
