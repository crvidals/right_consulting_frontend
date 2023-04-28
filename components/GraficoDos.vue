<template>
    <div>
        <canvas id="resp_por_dia"></canvas>
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
        this.getRespuestasPorDia()
    },
    methods: {
        getRespuestasPorDia () {
            axios.get('http://127.0.0.1:8000/respuestas_por_dia')
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
                return `${element.resps}`;
            });
            //console.log("resp=> ", resp)
            const ctx = document.getElementById('resp_por_dia').getContext('2d')
            this.chart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: "etiquetas",
                    datasets: [{
                        label: 'Respuestas por Día',
                        backgroundColor: ["grey", "black", "white", "red", "blue", "green", "cyan"],
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