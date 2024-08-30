<script>
export default {
  name: 'ConsultCardComponent',
  props: {
    patient: {
      type: Object,
      required: false
    }
  }
}
</script>

<template>
  <div
    :class="{
      low: patient.gravity === 'Baja',
      med: patient.gravity === 'Media',
      high: patient.gravity === 'Alta'
    }"
    class="consult"
    v-if="patient"
  >
    <h4>Paciente:</h4>
    <p>{{ patient.name }}</p>
    <h4>Fecha:</h4>
    <p>{{ patient.date }}</p>
    <h4>Hora:</h4>
    <p>{{ patient.time }}</p>
    <h4>Motivo:</h4>
    <p>{{ patient.motive }}</p>
    <br />
    <button @click="$emit('remove-patient', patient.id)">Eliminar</button>
  </div>
  <div v-else>
    <h2>Aún no hay consultas registradas</h2>
  </div>
</template>

<style scoped>
.consult {
  padding: 1rem;
  text-align: center;
  margin: 1rem;
}
h2 {
  text-align: center;
  color: red;
}
.low {
  background-color: #84dd22;
}
.med {
  background-color: #eedd22;
}
.high {
  background-color: #dd6911;
}
</style>
