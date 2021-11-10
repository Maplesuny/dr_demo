<template>
    <div class="echarts-box">
        <div id="Banana" :style="{ width: '2000px',height: 44 * channel.length +100 + 'px' }"></div>
    </div>
</template>

<script lang="js">
import { onMounted, ref } from 'vue';
import * as echarts from 'echarts';
import json from 'assets/10s.json';
export default {
    setup () {
        // Channel Name
        const channel = [
            'Fp1-A1',
            'F3-A1',
            'C3-A1',
            'P3-A1',
            'O1-A1',
            'Fp2-A2',
            'F4-A2',
            'C4-A2',
            'F4-A2',
            'Q2-A2',
            'F7-A1',
            'T3-A1',
            'T5-A1',
            'F8-A2',
            'T4-A2',
            'T6-A2',
            'PZ',
            'Cz',
            'Fz',
            'ECG',
        ];
        onMounted(() => {

            // 將數量換算成秒 ,number : 有幾筆資料
            function Convert_sec (number) {
                const dataArray = [];
                // 基底
                let base = end_time / number;
                let sum = 0;
                for (let i = 0; i < number; i++) {
                    sum = sum + base;
                    dataArray.push(sum);
                }
                return dataArray;
            }

            const chartDom = document.getElementById('Banana')
            const mychart = echarts.init(chartDom)
            let start_time = 0
            let end_time = 10
            let option = {
                animation: false,
                grid: {
                    top: 40,
                    left: 50,
                    right: 40,
                    bottom: 50
                },
                xAxis: {
                    name: 'x',
                    minorTick: {
                        show: true
                    },
                    minorSplitLine: {
                        show: true
                    }
                },
                yAxis: {
                    name: 'y',
                    min: -100,
                    max: 100,
                    minorTick: {
                        show: true
                    },
                    minorSplitLine: {
                        show: true
                    }
                },
                dataZoom: [
                    {
                        show: true,
                        type: 'inside',
                        filterMode: 'none',
                        xAxisIndex: [0],
                        startValue: -20,
                        endValue: 20
                    },
                    {
                        show: true,
                        type: 'inside',
                        filterMode: 'none',
                        yAxisIndex: [0],
                        startValue: -20,
                        endValue: 20
                    }
                ],
                series: [
                    {
                        type: 'line',
                        showSymbol: false,
                        clip: true,
                        data: Convert_sec(512 * end_time),
                    }
                ]
            };

            option && mychart.setOption(option);
            return {channel }
        })

    },
}
</script>
