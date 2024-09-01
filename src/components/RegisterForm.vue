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
    //metodo de agregar paciente y emitirlo a add-patient en componente padre
    addPatient(e) {
      e.preventDefault
      //si estan todos los datos, se agregara paciente mediante emit a metodo a componente padre y se asigna id unico basado en la fecha y hora en que se agregó
      if (
        this.patient.name &&
        this.patient.date &&
        this.patient.time &&
        this.patient.gravity &&
        this.patient.motive
      ) {
        //id unico se asigna segun fecha y hora en que se agregó
        this.patient.id = Date.now()
        //emitir a evento addpatient de componente padre una vez que se realiza carga en formulario. ...this.patient crea una instancia de patient
        this.$emit('add-patient', { ...this.patient })
      }
    }
  },
  computed: {
    //funcion isDisabled retorna valor booleano si un campo tiene menos de un caracter. si todos los datos tienen mas de un caracter, devolverá true. sirve para activar o desactivar boton de agregar.
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
    <!--ejecutara addPatient al subir formulario. prevent hara que no se refresque y se pierdan los datos al cargar-->
    <form @submit.prevent="addPatient">
      <div class="row">
        <div>
          <!--asigna clase css red si campo de input asignado tiene menos de un caracter-->
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
          <!--itera en todos los elementos del arreglo gravity para mostrarlos como options. luego se captura el valor con el v-model patient.gravity-->
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
