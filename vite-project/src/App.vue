<template>
  <div class="container-fluid mt-3">
    <input
      type="text"
      class="form-control mb-2"
      v-model="filtroNombre"
      placeholder="Buscar por nombre o apellido..."
    />

    <input
      type="text"
      class="form-control mb-3"
      v-model="filtroDni"
      placeholder="Buscar por DNI..."
    />

    <!-- ALERTA Bootstrap -->
    <div
      v-if="mostrarAlerta"
      class="alert alert-warning"
      role="alert"
    >
      Debe ingresar al menos 3 caracteres en alguno de los filtros para realizar la búsqueda.
    </div>

    <div class="card-deck m-0">
      <div class="row">
        <div class="col" v-for="persona in personasFiltradas" :key="persona.dni">
          <TarjetaPersona :persona="persona" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TarjetaPersona from './components/TarjetaPersona.vue'

export default {
  components: { TarjetaPersona },
  data() {
    return {
      filtroNombre: '',
      filtroDni: '',
      personas: [
        {
          nombre: 'Daniel',
          apellido: 'Sanchez',
          correo: 'danielsanchez68@hotmail.com',
          dni: '20442873'
        },
        {
          nombre: 'Juan',
          apellido: 'Perez',
          correo: 'j@p.gmail.com',
          dni: '12345678'
        },
        {
          nombre: 'Ana',
          apellido: 'Suarez',
          correo: 'a@s.gmail.com',
          dni: '87654321'
        },
        {
          nombre: '...',
          apellido: '...',
          correo: '...',
          dni: '...'
        }
      ]
    }
  },
  computed: {
    personasFiltradas() {
      return this.personas.filter((p) => {
        const nombreCompleto = `${p.nombre} ${p.apellido}`.toLowerCase()
        const dni = p.dni.toLowerCase()
        let tieneQueAparecer = true;
        if (this.filtroNombre.length >= 3) {
          tieneQueAparecer = nombreCompleto.includes(this.filtroNombre.toLowerCase())
        }
        if (this.filtroDni.length >= 3) {
          tieneQueAparecer = tieneQueAparecer && dni.includes(this.filtroDni.toLowerCase())
        }
          return (
            tieneQueAparecer
          )    
        })
      },  
    mostrarAlerta() {
      // Verifica si alguno de los filtros está entre 1 y 2 caracteres
      const nombreLen = this.filtroNombre.length
      const dniLen = this.filtroDni.length

      const filtroNombreInvalido = nombreLen > 0 && nombreLen < 3
      const filtroDniInvalido = dniLen > 0 && dniLen < 3

      return filtroNombreInvalido || filtroDniInvalido
    }
  }
}
</script>