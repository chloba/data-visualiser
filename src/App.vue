<template>
  <div class="container">
    <div class="row"></div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
// import LineChart from "./components/LineChart.vue";
export default {
  name: "App",
  components: {
    // LineChart,
  },
  data() {
    return {
      arrPositive: [],
      arrHospitalised: [],
      arrInIcu: [],
      arrOnVentilators: [],
      arrRecovered: [],
      arrDeaths: [],
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
