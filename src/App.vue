<template>
  <div class="container">
    <div class="row mt-5">
      <div class="col text-center">
        <h1>COVID-19 Data Visualiser</h1>
      </div>
    </div>
    <div class="row mt-5" v-if="arrPositive.length > 0">
      <div class="col">
        <h2>Positive</h2>
        <line-chart
          :chartData="arrPositive"
          label="Positive"
          :chartColours="positiveChartColors"
        />
      </div>
    </div>
    <div class="row mt-5" v-if="arrHospitalised.length > 0">
      <div class="col">
        <h2>Hospitalised</h2>
        <line-chart
          :chartData="arrHospitalised"
          label="Hospitalised"
          :chartColours="hospitalisedChartColors"
        />
      </div>
    </div>
    <div class="row mt-5" v-if="arrInIcu.length > 0">
      <div class="col">
        <h2>In ICU</h2>
        <line-chart
          :chartData="arrInIcu"
          label="In ICU"
          :chartColours="inIcuChartColors"
        />
      </div>
    </div>
    <div class="row mt-5" v-if="arrOnVentilators.length > 0">
      <div class="col">
        <h2>On Ventilators</h2>
        <line-chart
          :chartData="arrOnVentilators"
          label="On Ventilators"
          :chartColours="onVentilatorChartColors"
        />
      </div>
    </div>
    <div class="row mt-5" v-if="arrRecovered.length > 0">
      <div class="col">
        <h2>Recovered</h2>
        <line-chart
          :chartData="arrRecovered"
          label="Recovered"
          :chartColours="recoveredChartColors"
        />
      </div>
    </div>
    <div class="row mt-5" v-if="arrDeaths.length > 0">
      <div class="col">
        <h2>Deaths</h2>
        <line-chart
          :chartData="arrDeaths"
          label="Deaths"
          :chartColours="deathsChartColors"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
import LineChart from "./components/LineChart.vue";
export default {
  name: "App",
  components: {
    LineChart,
  },
  data() {
    return {
      arrPositive: [],
      positiveChartColors: {
        borderColor: "#077187",
        backgroundColor: "#74A57F",
      },
      arrHospitalised: [],
      hospitalisedChartColors: {
        borderColor: "#251F47",
        backgroundColor: "#858EAB",
      },
      arrInIcu: [],
      inIcuChartColors: {
        borderColor: "#190B28",
        backgroundColor: "#E55381",
      },
      arrOnVentilators: [],
      onVentilatorChartColors: {
        borderColor: "#784F41",
        backgroundColor: "#BBE5ED",
      },
      arrRecovered: [],
      recoveredChartColors: {
        borderColor: "#4E5E66",
        backgroundColor: "#31E981",
      },
      arrDeaths: [],
      deathsChartColors: {
        borderColor: "#E06D06",
        backgroundColor: "#402A2C",
      },
    };
  },
  async created() {
    const { data } = await axios.get(
      "https://api.covidtracking.com/v1/us/daily.json"
    );
    data.forEach((d) => {
      const date = moment(d.date, "YYYYMMDD").format("DD/MM");
      const {
        positive,
        hospitalizedCurrently,
        inIcuCurrently,
        onVentilatorCurrently,
        recovered,
        death,
      } = d;
      this.arrPositive.push({ date, total: positive });
      this.arrHospitalised.push({ date, total: hospitalizedCurrently });
      this.arrInIcu.push({ date, total: inIcuCurrently });
      this.arrOnVentilators.push({ date, total: onVentilatorCurrently });
      this.arrRecovered.push({ date, total: recovered });
      this.arrDeaths.push({ date, total: death });
    });
  },
};
</script>

<style></style>
