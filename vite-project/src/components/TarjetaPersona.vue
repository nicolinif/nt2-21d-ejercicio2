<template>
  <div class="card mb-3">
    <div class="card-body">
      <h5 class="card-title">{{ getNombreCompleto(persona) }}</h5>
      <p class="card-text">dni {{ persona.dni }}</p>
      <a href="#" class="card-link">{{ persona.correo }}</a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    persona: Object
  },
  methods: {
    getNombreCompleto(p) {
      return `${p.nombre} ${p.apellido}`
    }
  }
}
</script>