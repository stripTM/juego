<template>
  <li class="personaje">
    <img v-bind:alt="alt" v-bind:src="urlImage"/>
    <button v-if="esElegible" v-on:click="clickElegir">Elegir</button>
  </li>
</template>

<script>
export default {
  name: 'PersonajeSeleccion',
  props: {
    personaje: Object
  },
  methods: {
    clickElegir() {
      this.$emit('elegirPersonaje', this.personaje)
    }
  },
  computed: {
    urlImage() {
      return (this.personaje.equipo === null) ? this.personaje.imgOn : this.personaje.imgOff
    },
    alt() {
      return 'Personaje ' + this.personaje.id
    },
    esElegible() {
      return this.personaje.equipo === null
    }
  }
}
</script>

