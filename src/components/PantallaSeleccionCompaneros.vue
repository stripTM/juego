<template>
    <section>
        <h1>Pantalla 1 selección de compañeros</h1>
        <EquipoSeleccionCompaneros
            equipo="1"
            v-if="showVentana.jugador1"
            v-bind:personajes="personajes"
            v-on:elegirPersonaje="elegirPersonaje"
            v-on:empezarJuego="empezarJuego"
        />
        <hr/>
        <EquipoSeleccionCompaneros
            equipo="2"
            v-if="showVentana.jugador2"
            v-bind:personajes="personajes"
            v-on:elegirPersonaje="elegirPersonaje"
            v-on:empezarJuego="empezarJuego"
        />
    </section>
</template>

<script>
import EquipoSeleccionCompaneros from './EquipoSeleccionCompaneros.vue'

export default {
    name: 'PantallaSeleccionCompaneros',
    components: {
        EquipoSeleccionCompaneros
    },
    props: {
        personajes: Array,
        showVentana: Object
    },
    methods: {
        empezarJuego() {
            this.$emit('empezarJuego')
        },
        elegirPersonaje(seleccion) {
            let nuevosPersonajes = [
                {
                id: 1,
                imgOn: 'personaje_2_on.png',
                imgOff: 'personaje_2_off.png',
                equipo: null
                },
                {
                id: 2,
                imgOn: 'personaje_1_on.png',
                imgOff: 'personaje_1_off.png',
                equipo: null
                }
            ]
            nuevosPersonajes = this.personajes.map(
                personaje => {
                    if(seleccion.idPersonaje === personaje.id) {
                        personaje.equipo = seleccion.idEquipo
                    }
                    return personaje
                }
            )
            this.$emit('cambiarPersonajes', nuevosPersonajes)
        }
    }
}
</script>

