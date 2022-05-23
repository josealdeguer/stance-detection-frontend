<template>
  <div class="container coronavirus">
  <v-row class="mb-6 mt-6" justify="center">
     <v-card>
       <GChart
        type="ColumnChart"
        :data="tweetsByStance"
        :options="tweetsByStanceOptionsColumn"
        />
        <v-card-subtitle class="subtitle-2 font-weight-medium">
          Número de tweets por cada polaridad
        </v-card-subtitle>
      </v-card>
  </v-row>
  <!-- <v-row class="mb-6 mt-6" justify="center">
    <v-card>
      <GChart
        type="PieChart"
        :data="tweetsByStance"
        :options="tweetsByStanceOptionsPie"
      />
      <v-card-subtitle class="subtitle-2 font-weight-medium">
        Número de tweets por cada polaridad
      </v-card-subtitle>
    </v-card>
  </v-row> -->
  <v-row class="mb-6 mt-6" justify="center">
    <v-card>
      <GChart
        type="LineChart"
        :data="tweetsByDate"
        :options="tweetsByDateOptionsLine"
      />
      <v-card-subtitle class="subtitle-2 font-weight-medium">
        Timeline del total de tweets
      </v-card-subtitle>
    </v-card>
  </v-row>
  <v-row class="mb-6 mt-6" justify="center">
      <v-card>
        <GChart
          type="AreaChart"
          :data="tweetsByStanceAndDate"
          :options="tweetsByStanceAndDateOptionsArea"
        />
        <v-card-subtitle class="subtitle-2 font-weight-medium">
          Timeline del número de tweets por cada polaridad
        </v-card-subtitle>
      </v-card>
  </v-row>
  </div>
</template>

<script>
// @ is an alias to /src
import { GChart } from "vue-google-charts";
// import Independencia from "@/components/Independencia.vue";

export default {
  name: "Independencia",
  components: {
    // Independencia,
    GChart
  },

  data() {
    return {
      tweetsByStance: null,
      tweetsByStanceOptionsColumn: {
        title: 'Número de tweets por polaridad',
        width: 800,
        height: 400,
        legend: 'none',
        backgroundColor: '#f2f7f7'
      },
      tweetsByStanceOptionsPie: {
        title: 'Porcentaje de tweets por polaridad',
        width: 800,
        height: 400,
        colors: ['brown', 'teal', 'gold'],
        backgroundColor: '#f2f7f7'
      },
      tweetsByDate: null,
      tweetsByDateOptionsLine: {
        title: 'Número de tweets por fecha',
        width: 1200,
        height: 400,
        legend: 'none',
        colors: ['#436f75'],
        backgroundColor: '#f2f7f7'
      },
      tweetsByStanceAndDate: null,
      tweetsByStanceAndDateOptionsArea: {
        title: 'Número de tweets por polaridad y fecha',
        width: 1200,
        height: 400,
        colors: ['brown', 'teal', 'gold'],
        backgroundColor: '#f2f7f7'
      },
    }
  },

  created() {
    this.$api
      .get("coronavirusCountByStance")
      .then(response => {
        var chartData = new Array(['Stance', 'Tweets', { role: 'annotation' }, { role: 'style' }])
        var i
        for(i=0; i<response.data.length;i++) {
          chartData[i+1] = response.data[i]
          chartData[i+1][2] = response.data[i][1]
        }
        chartData[1][0] = 'EN CONTRA'
        chartData[2][0] = 'A FAVOR'
        chartData[3][0] = 'NEUTRAL'

        chartData[1][3] = 'brown'
        chartData[2][3] = 'teal'
        chartData[3][3] = 'gold'
        this.tweetsByStance = chartData
    }),

    this.$api
      .get("coronavirusCountByDate")
      .then(response => {
        var chartData = new Array(['Fecha', 'Tweets'])
        var i
        // var dateFormat = require('dateformat');
        for(i=0; i<response.data.length;i++) {
          var d = new Date(response.data[i][0])
          var day = d.getDate().toString()
          var month = (d.getMonth()+1).toString()
          var year = d.getFullYear().toString().substr(2,2)
          if (day.length === 1) {
              day = "0" + day;
          }
          if (month.length === 1) {
            month = "0" + month;
          }
          var dateFormat = day + "/" + month + "/" + year;
          chartData[i+1] = response.data[i]
          chartData[i+1][0] = dateFormat
        }
        this.tweetsByDate = chartData
    }),

    this.$api
      .get("coronavirusCountByStanceAndDate")
      .then(response => {
        var chartData = new Array(['Fecha', 'EN CONTRA', 'A FAVOR', 'NEUTRAL'])
        var i
        for(i=0; i<response.data.length/3;i++) {
          var d = new Date(response.data[i][1])
          var day = d.getDate().toString()
          var month = (d.getMonth()+1).toString()
          var year = d.getFullYear().toString().substr(2,2)
          if (day.length === 1) {
              day = "0" + day;
          }
          if (month.length === 1) {
            month = "0" + month;
          }
          var dateFormat = day + "/" + month + "/" + year;

          chartData[i+1] = [
                              dateFormat,
                              response.data[i][2],
                              response.data[i+(response.data.length/3)][2],
                              response.data[i+(response.data.length/3)*2][2]
                            ]
        }
        this.tweetsByStanceAndDate = chartData
    })
  }
};
</script>

<style scoped>
.coronavirus {
  margin-top: 50px;
  max-width: 1200px;
  background: linear-gradient(rgba(255,255,255,.5), rgba(255,255,255,.5)), url("https://www.publico.es/uploads/2020/04/25/5ea44127d3f8b.jpeg");
}
</style>
