<template>
    <div>
        <canvas id="myChart"></canvas>
    </div>
</template>

<script>
import axios from 'axios'
import { Chart, registerables } from 'chart.js';

export default {
    constructor() {
        Chart.register(...registerables);
    },
    name: 'GraficoUno',
    data () {
        return {
            chart: null
        }
    },
    mounted () {
        this.getData()
    },
    methods: {
        getData () {
            axios.get('http://127.0.0.1:8000/all_respuestas')
            .then(response => {
                const data = response.data.respuestas
                this.renderChart(data)
            })
            .catch(error => {
                console.log("Error=> ", error)
            })
        },
        renderChart (data) {
                let edades = data.map(function(element){
                    return `${element.edad}`;
                });
            const ctx = document.getElementById('myChart').getContext('2d')
            this.chart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: "etiquetas",
                    datasets: [{
                        label: 'Todas las Respuestas',
                        backgroundColor: ["red", "blue", "green", "grey", "black", "white"],
                        data: edades
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