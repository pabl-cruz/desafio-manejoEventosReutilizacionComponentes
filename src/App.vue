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
      patients: [],
      currentPatient: null
    }
  },
  methods: {
    addPatient(patient) {
      this.currentPatient = patient
      this.patients.push(patient)
    }
  }
}
</script>

<template>
  <RegisterForm @add-patient="addPatient" />
  <section class="consults">
    <div v-for="(patient, id) in patients" :key="patient.id">
      <ConsultCard :patient="patient" :id="id" />
    </div>
  </section>
</template>

<style scoped>
.consults {
  display: flex;
  flex-direction: row;
}
</style>
