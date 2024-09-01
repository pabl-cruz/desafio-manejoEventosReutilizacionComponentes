<script>
import RegisterForm from './components/RegisterForm.vue'
import ConsultCard from './components/ConsultCard.vue'

export default {
  //traer componentes de elementos importados
  components: {
    RegisterForm,
    ConsultCard
  },
  data() {
    return {
      patients: []
    }
  },
  //metodo addpatient escucha evento emitido de componente hijo para agregar instancia de patient en arreglo patients
  methods: {
    addPatient(patient) {
      this.patients.push(patient)
    },
    //metodo deletepatient escucha evento emitido de componente hijo para filtrar a todas las cartas del arreglo patients que NO corresponden al id asignado al boton, eliminandola
    deletePatient(id) {
      this.patients = this.patients.filter((patient) => patient.id !== id)
    }
  }
}
</script>

<template>
  <!--escucha evento emitido desde componente hijo y asigna a metodo de componente padre-->
  <RegisterForm @add-patient="addPatient" />
  <section class="consults">
    <!--iterara por todos los pacientes e indices de patients, tiene como llave el id de patient-->
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
