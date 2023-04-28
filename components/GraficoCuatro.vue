<template>
    <div>
        <canvas id="frec_colores"></canvas>
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
        this.getFrecColores()
    },
    methods: {
        getFrecColores () {
            axios.get('http://127.0.0.1:8000/colores')
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
            const ctx = document.getElementById('frec_colores').getContext('2d')
            this.chart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: "etiquetas",
                    datasets: [{
                        label: 'Colores',
                        backgroundColor: ["grey", "green", "black", "red", "blue", "white"],
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