<template>
  <v-container fluid grid-list-md>
    <v-layout row wrap>
      <v-flex xs10 md6>
        <v-card>
          <v-card-text class="px2 text-md-center">
            <div ref="sale" style="width: 100%;height:500px"></div>
          </v-card-text>
        </v-card>
      </v-flex>

      <v-flex xs10 md6>
        <v-card>
          <v-card-text class="px2 text-md-center">
            <div ref="pie" style="width: 100%;height:500px"></div>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  // 引入 ECharts 主模块
  // 不能使用echarts/lib/echarts，会导致无法显示
  var echarts = require('echarts');
  require('echarts/lib/chart/bar');
  require('echarts/lib/chart/pie');

  export default {
    name: "dashboard",
    data() {
      return {}
    },
    mounted() {
      this.$nextTick(() => {
        let sale = echarts.init(this.$refs.sale);


        let data = [];

        for (let i = 0; i <= 100; i++) {
          let theta = i / 100 * 360;
          let r = 5 * (1 + Math.sin(theta / 180 * Math.PI));
          data.push([r, theta]);
        }
        // 指定图表的配置项和数据
        let option = {
          title: {
            text: '极坐标双数值轴'
          },
          legend: {
            data: ['line']
          },
          polar: {},
          tooltip: {
            trigger: 'axis',
            axisPointer: {
              type: 'cross'
            }
          },
          angleAxis: {
            type: 'value',
            startAngle: 0
          },
          radiusAxis: {},
          series: [{
            coordinateSystem: 'polar',
            name: 'line',
            type: 'line',
            data: data
          }]
        };


        // 使用刚指定的配置项和数据显示图表。
        sale.setOption(option);

        const pie = echarts.init(this.$refs.pie);


        let option1 = {
          tooltip: {
            formatter: "{a} <br/>{b} : {c}%"
          },
          toolbox: {
            feature: {
              restore: {},
              saveAsImage: {}
            }
          },
          series: [
            {
              name: '业务指标',
              type: 'gauge',
              detail: {formatter: '{value}%'},
              data: [{value: 50, name: '完成率'}]
            }
          ]
        };

        setInterval(() => {
          option.series[0].data[0].value = (Math.random() * 100).toFixed(2) - 0;
          myChart.setOption(option, true);
        }, 2000);
        pie.setOption(option1)
      })
    }
  }
</script>

<style scoped>

</style>
