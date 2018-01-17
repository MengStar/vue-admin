<template>
    <section class="chart-container">
        <el-row>
            <el-col :span="12">
                <div id="chartColumn" style="width:100%; height:400px;"></div>
            </el-col>
            <el-col :span="12">
                <div id="chartBar" style="width:100%; height:400px;"></div>
            </el-col>
            <el-col :span="12">
                <div id="chartLine" style="width:100%; height:400px;"></div>
            </el-col>
            <el-col :span="12">
                <div id="chartPie" style="width:100%; height:400px;"></div>
            </el-col>
            <el-col :span="24">
                <a href="http://echarts.baidu.com/examples.html" target="_blank" style="float: right;">more>></a>
            </el-col>
        </el-row>
    </section>
</template>

<script>
    import echarts from 'echarts'
    import {getChartLine, getChartBar, getChartColumn, getChartPie} from '../../api/api';

    export default {
        data() {
            return {
                chartColumn: null,
                chartBar: null,
                chartLine: null,
                chartPie: null,
            }
        },

        methods: {
            drawColumnChart() {
                this.chartColumn = echarts.init(document.getElementById('chartColumn'));
                getChartColumn().then(res => {
                    this.chartColumn.setOption(res.data);
                })

            },
            drawBarChart() {
                this.chartBar = echarts.init(document.getElementById('chartBar'));
                getChartBar().then(res => {
                    this.chartBar.setOption(res.data);
                })
            },
            drawLineChart() {
                this.chartLine = echarts.init(document.getElementById('chartLine'));
                getChartLine().then((res) => {
                    this.chartLine.setOption(res.data);
                });


            },
            drawPieChart() {
                this.chartPie = echarts.init(document.getElementById('chartPie'));
                getChartPie().then(res => {
                    this.chartPie.setOption(res.data);
                })
            },
            drawCharts() {
                this.drawColumnChart()
                this.drawBarChart()
                this.drawLineChart()
                this.drawPieChart()
            },
        },

        mounted: function () {
            this.drawCharts()
        },
        updated: function () {
            this.drawCharts()
        }
    }
</script>

<style scoped>
    .chart-container {
        width: 100%;
        float: left;
    }

    /*.chart div {
        height: 400px;
        float: left;
    }*/

    .el-col {
        padding: 30px 20px;
    }
</style>
