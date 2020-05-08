<template>
  <div id="app" class="container">
    <div class="row mt=5" v-if="arrPositive.length > 0">
      <div class="col">
        <h2> Positive </h2>
        <line-chart :charData="arrPositive" :options="chartOptions" :label="Positive" ></line-chart>

      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';
import LineChart from './Components/LineChart'
export default {
  name: 'App',
  components: {
    LineChart
  },
  data(){
    return{
      arrPositive :[],
    arrHospitalized:[],
    arrInIcu:[],
    arrOnVentilators:[],
    arrRecovered : [],
    arrDeaths : [],
    chartOptions:{
      responsive : true,
      maintainAspectRatio: false,
    }
    }
  }, 
  async created(){
    const{ data } = await axios.get("https:covidtracking.com/api/us/daily");
    data.forEach(d => {
const date = moment(d.date, "YYYYMMDD").format("MM/DD");

const {
  positive,
  hospitalizedCurrently,
  inIcuCurrently,
  onVentilatorCurrently,
  recovered,
  death
} = d;

this.arrPositive.push({date, total: positive});
this.arrhospitalized.push({date, total:hospitalizedCurrently});
this.arrInIcu.push({date, total:inIcuCurrently});
this.arrOnVentilators.push({date, total:onVentilatorCurrently});
this.arrRecovered.push({date, total:recovered});
this.arrDeaths.push({date, total:death});
console.log(this.arrDeaths);
    }

    )
  }
}
</script>

<style>

</style>
