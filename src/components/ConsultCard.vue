<script>
export default {
  name: 'ConsultCardComponent',
  //pasa como propiedad el objeto patient para capturar sus datos.
  props: {
    patient: {
      type: Object,
      required: false
    }
  },
  //metodo deletePatient emitira a metodo remove-patient del componenete padre para eliminar carta de usuario asignado basado en su id
  methods: {
    deletePatient() {
      this.$emit('remove-patient', this.patient.id)
    }
  }
}
</script>

<template>
  <!--estilos condicionales de fondo de carta basado en la gravedad asignada a la consulta del paciente-->
  <div
    :class="{
      low: patient.gravity === 'Baja',
      med: patient.gravity === 'Media',
      high: patient.gravity === 'Alta',
      white: patient.gravity === 'Alta'
    }"
    class="consult"
    v-if="patient"
  >
    <!--si existe instancia de paciente, renderizará contenido del paciente en carta-->
    <h4>Paciente:</h4>
    <p>{{ patient.name }}</p>
    <h4>Fecha:</h4>
    <p>{{ patient.date }}</p>
    <h4>Hora:</h4>
    <p>{{ patient.time }}</p>
    <h4>Motivo:</h4>
    <p>{{ patient.motive }}</p>
    <br />
    <!--button escuchara click y emitira evento deletePatient-->
    <button @click="deletePatient">Eliminar</button>
  </div>
  <!--si no existen cartas, mostrará texto-->
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
.white {
  color: white;
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
