<template>
<div>
    <img src="../assets/RT.png" alt="Rotten tomatoes logo" height="80 " id="rt-logo">

    <GChart
    :settings="{ packages: ['corechart', 'gauge'] }"
    type="Gauge"
    :data="chartData"
    :options="{width: 220, height: 220,
            redColor: '#7a2323',
            redFrom: 90, redTo: 100,
            yellowFrom:75, yellowTo: 90,
            greenColor: '#18abe9',
            greenFrom:25, greenTo: 75,
            minorTicks: 5
            }"
    />
    <img src="../assets/well.gif" alt="well done gif" height="120">
</div>
</template>

<script>
import { eventBus } from '../main'
import { GChart } from 'vue-google-charts'
export default {
    name: 'charts',
    props: ['selectedMovie'],
    components: { GChart },
    computed: {
        
        chartData: function(){          
            const exitData = []
            const name = ['Label', 'RtScore']
            const data =['Tomatometr', parseInt(this.selectedMovie.rt_score)]
                    exitData.push(data)
                exitData.unshift(name)
            return exitData
        },   
    }, 
}
</script>

<style lang="css">
#rt-logo {
box-shadow:  0 0 100px black;
opacity: 0.7
}
</style>