<template>
    <div>
        <canvas id="frec_edades"></canvas>
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
        this.getFrecEdades()
    },
    methods: {
        getFrecEdades () {
            axios.get('http://127.0.0.1:8000/edades')
            .then(response => {
                const data = response.data.respuestas
                this.renderChart(data)
            })
            .catch(error => {
                console.log("Error=> ", error)
            })
        },
        renderChart (data) {
            let cantidad = data.map(function(element){
                return `${element.cantidad}`;
            });
            /*let edad = data.map(function(element){
                return `${element.edad}`;
            });*/
            const ctx = document.getElementById('frec_edades').getContext('2d')
            this.chart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: "etiquetas",
                    datasets: [{
                        label: 'Edades',
                        backgroundColor: ["black", "red", "green", "blue", "grey", "white"],
                        data: cantidad
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