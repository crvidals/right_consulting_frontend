<template>
    <div>
        <canvas id="frec_colores_edad"></canvas>
    </div>
</template>

<script>
import axios from 'axios'
import { Chart, registerables } from 'chart.js';

export default {
    constructor() {
        Chart.register(...registerables);
    },
    name: 'GraficoDos',
    data () {
        return {
            chart: null
        }
    },
    mounted () {
        this.getFrecColoresEdad()
    },
    methods: {
        getFrecColoresEdad () {
            axios.get('http://127.0.0.1:8000/colores_edad')
            .then(response => {
                const data = response.data.respuestas
                this.renderChart(data)
            })
            .catch(error => {
                console.log("Error=> ", error)
            })
        },
        renderChart (data) {
                let resp = data.map(function(element){
                    return `${element.cantidad}`;
                })
            const ctx = document.getElementById('frec_colores_edad').getContext('2d')
            this.chart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: "etiquetas",
                    datasets: [{
                        label: 'Colores por Edad',
                        backgroundColor: ["red", "cyan", "blue", "green", "grey", "black", "white"],
                        data: resp
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false
                }
            })
        }
    }
}
</script>