<template>
    <section>
        <h2>Equipo {{ equipo }} seleccion compañeros</h2>
        <ul class="personajes">
            <PersonajeSeleccion
                v-for="personaje in personajes"
                v-bind:key="personaje.id"
                v-bind:personaje="personaje"
                v-on:elegirPersonaje="elegirPersonaje"
            />
        </ul>
        <button v-on:click="clickEmpezar">Empezar juego</button>
    </section>
</template>

<script>
import PersonajeSeleccion from './PersonajeSeleccion.vue'

export default {
    name: 'EquipoSeleccionCompaneros',
    props: {
        equipo: String,
        personajes: Array
    },
    components: {
        PersonajeSeleccion
    },
    methods: {
        elegirPersonaje(personaje) {
            this.$emit(
                'elegirPersonaje',
                {
                    idEquipo: this.equipo,
                    idPersonaje: personaje.id
                }
            )
        },
        clickEmpezar() {
            this.$emit('empezarJuego')
        },
    }
}
</script>

