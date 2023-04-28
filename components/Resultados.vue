<template>
    <div class="container mt-5">
        <div class="row">
            <h2 class="mt-3 align-center">GRÁFICOS</h2>
            <div class="col-sm-6 col-md-6 mt-3">
                <div class="card">
                    <div class="card-body">
                        <h5 class="card-title">Todas las Respuestas</h5>
                        <GraficoUno />
                    </div>
                </div>
            </div>
            <div class="col-sm-6 col-md-6 mt-3">
                <div class="card">
                    <div class="card-body">
                        <h5 class="card-title">Respuestas por Día</h5>
                        <GraficoDos />
                    </div>
                </div>
            </div>
            <div class="col-sm-6 col-md-6 mt-3">
                <div class="card">
                <div class="card-body">
                    <h5 class="card-title">Frecuencia de Edades</h5>
                    <GraficoTres />
                </div>
                </div>
            </div>
            <div class="col-sm-6 col-md-6 mt-3">
                <div class="card">
                <div class="card-body">
                    <h5 class="card-title">Frecuencia de Colores</h5>
                    <GraficoCuatro />
                </div>
                </div>
            </div>
            <div class="col-sm-6 col-md-6 mt-3">
                <div class="card">
                <div class="card-body">
                    <h5 class="card-title">Frecuencia de Colores por Edad</h5>
                    <GraficoCinco />
                </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import GraficoUno from './GraficoUno.vue'
    import GraficoDos from './GraficoDos.vue'
    import GraficoTres from './GraficoTres.vue'
    import GraficoCuatro from './GraficoCuatro.vue'
    import GraficoCinco from './GraficoCinco.vue'

    export default {
        name: 'Resultados',
        components: {
            GraficoUno,
            GraficoDos,
            GraficoTres,
            GraficoCuatro,
            GraficoCinco
        }
    }
</script>