<template>
    <section>
        <h1>Pantalla 2 ronda de juego</h1>
        <div>{{ tiempoRestante }}</div>
        <button v-on:click="clickReiniciar">Reiniciar juego</button>
    </section>
</template>

<script>
export default {
    name: 'PantallaRondaJuego',
    props: {
        inicioPartida: Date,
        showVentana: Object
    },
    data() {
        return {
            actualPartida: new Date(),
            timer: null
        }
    },
    mounted() {
        this.timer = setInterval(() => {
            this.timerCount(this.start,this.end)
        }, 1000)
    },
    destroyed() {
        clearInterval(this.timer)
        this.timer = null
    },
    methods: {
        timerCount() {
            this.actualPartida = new Date()
            if (this.actualPartida.getTime() - this.inicioPartida.getTime() > 4 * 60 * 1000) {
                clearInterval(this.timer)
                this.timer = null
            }
        },
        clickReiniciar() {
            this.$emit('reiniciarJuego')
        }
    },
    computed: {
        tiempoRestante() {
            const limite = 4 * 60
            const restante = limite - Math.floor((this.actualPartida.getTime() - this.inicioPartida.getTime()) / 1000)
            const minutos = Math.floor(restante / 60)
            const segundos = (restante % 60 < 10) ? '0' + restante % 60 : restante % 60
            return minutos + ':' + segundos
        }
    }
}
</script>

