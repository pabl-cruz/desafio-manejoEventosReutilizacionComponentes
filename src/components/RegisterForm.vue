<script>
export default {
  name: 'RegisterFormComponent',
  data() {
    return {
      patient: {
        name: '',
        date: '',
        time: '',
        gravity: '',
        motive: '',
        id: ''
      },
      gravityType: ['Baja', 'Media', 'Alta']
    }
  },
  methods: {
    addPatient(e) {
      e.preventDefault
      if (
        this.patient.name &&
        this.patient.date &&
        this.patient.time &&
        this.patient.gravity &&
        this.patient.motive
      ) {
        this.$emit('add-patient', { ...this.patient })
      }
    }
  },
  computed: {
    isDisabled() {
      return (
        this.patient.name.length < 1 ||
        this.patient.date.length < 1 ||
        this.patient.time.length < 1 ||
        this.patient.gravity.length < 1 ||
        this.patient.motive.length < 1
      )
    }
  }
}
</script>

<template>
  <div class="register-card">
    <form @submit.prevent="addPatient">
      <div class="row">
        <div>
          <label :class="{ red: patient.name.length < 1 }" class="label-form-title" for="name"
            >Paciente</label
          >
          <input type="text" id="name" name="name" v-model="patient.name" />
        </div>
        <div>
          <label :class="{ red: patient.date.length < 1 }" class="label-form-title" for="date"
            >Fecha</label
          >
          <input type="date" id="date" name="date" v-model="patient.date" />
        </div>
        <div>
          <label :class="{ red: patient.time.length < 1 }" class="label-form-title" for="time"
            >Hora</label
          >
          <input type="time" id="time" name="time" v-model="patient.time" />
        </div>
        <div>
          <label :class="{ red: patient.gravity.length < 1 }" class="label-form-title" for="gravity"
            >Gravedad</label
          >
          <select name="gravity" id="gravity" v-model="patient.gravity">
            <option v-for="gravity in gravityType" :value="gravity">
              {{ gravity }}
            </option>
          </select>
        </div>
        <div>
          <label :class="{ red: patient.motive.length < 1 }" class="label-form-title" for="motive"
            >Motivo</label
          >
          <input type="text" name="motive" id="motive" v-model="patient.motive" />
        </div>
      </div>
      <br />
      <input :disabled="isDisabled" type="submit" value="Agregar" id="add" />
    </form>
  </div>
</template>

<style scoped>
form {
  display: grid;
}

.label-form-title {
  text-align: center;
  font-size: 1.4rem;
  display: block;
  font-weight: 700;
}

.register-card {
  background-color: #ffffff;
  border: 1px solid #888888;
  box-shadow: 1px 1px 1px 1px #222222;
  border-radius: 20px;
  padding: 1.5rem;
}
.row {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}
.red {
  color: red;
}

#add {
  justify-self: center;
}
</style>
