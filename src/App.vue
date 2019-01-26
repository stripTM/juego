<template>
  <div id="app">
    <div>
      <input v-model="showVentana.jugador1" type="checkbox" id="showJugador1"/>
      <label for="showJugador1">Ver pantalla de jugador 1</label>
      <input v-model="showVentana.jugador2" type="checkbox" id="showJugador2"/>
      <label for="showJugador2">Ver pantalla de jugador 2</label>
    </div>
    <PantallaSeleccionCompaneros
      v-if="showPantalla1"
      v-bind:personajes="personajes"
      v-bind:showVentana="showVentana"
      v-on:cambiarPersonajes="cambiarPersonajes"
      v-on:empezarJuego="empezarJuego"
    />
    <PantallaRondaJuego
      v-if="showPantalla2"
      v-on:reiniciarJuego="reiniciarJuego"
      v-bind:inicioPartida="inicioPartida"
      v-bind:showVentana="showVentana"
    />
  </div>
</template>

<script>
import PantallaSeleccionCompaneros from './components/PantallaSeleccionCompaneros.vue'
import PantallaRondaJuego from './components/PantallaRondaJuego.vue'

export default {
  name: 'app',
  components: {
    PantallaSeleccionCompaneros,
    PantallaRondaJuego
  },
  data() {
    return {
      showVentana: {
        jugador1: true,
        jugador2: true
      },
      pantalla: 'seleccionCompaneros',
      personajes: [
        {
          id: 1,
          imgOn: 'personaje_1_on.png',
          imgOff: 'personaje_1_off.png',
          equipo: null
        },
        {
          id: 2,
          imgOn: 'personaje_2_on.png',
          imgOff: 'personaje_2_off.png',
          equipo: null
        },
        {
          id: 3,
          imgOn: 'personaje_1_on.png',
          imgOff: 'personaje_1_off.png',
          equipo: null
        },
        {
          id: 4,
          imgOn: 'personaje_2_on.png',
          imgOff: 'personaje_2_off.png',
          equipo: null
        },
        {
          id: 5,
          imgOn: 'personaje_2_on.png',
          imgOff: 'personaje_2_off.png',
          equipo: null
        },
        {
          id: 6,
          imgOn: 'personaje_1_on.png',
          imgOff: 'personaje_1_off.png',
          equipo: null
        }
      ],
      inicioPartida: null
    }
  },
  methods: {
    empezarJuego() {
      this.inicioPartida = new Date()
      this.pantalla = 'rondaJuego'
    },
    cambiarPersonajes(personajes) {
      this.personajes = personajes
    },
    reiniciarJuego() {
      this.personajes = this.personajes.map(
                personaje => {
                  personaje.equipo = null
                  return personaje
                }
      )
      this.pantalla = 'seleccionCompaneros'
    }
  },
  computed: {
    showPantalla1() {
      return this.pantalla === 'seleccionCompaneros'
    },
    showPantalla2() {
      return this.pantalla === 'rondaJuego'
    }
  }

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
