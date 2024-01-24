<template>
  <div><Line :data="data" :options="options" height="500px" /></div>
</template>
<script>
import { Line } from "vue-chartjs";
import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend,
} from "chart.js";

ChartJS.register(
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend
);
export default {
  components: {
    Line,
  },
  props: {
    label: {
      type: String,
      required: true,
    },
    chartData: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      data: {
        labels: [
          "January",
          "February",
          "March",
          "April",
          "May",
          "June",
          "July",
        ],
        datasets: [
          {
            label: this.label,
            backgroundColor: "#f87979",
            data: [40, 39, 10, 40, 39, 80, 40],
          },
        ],
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
      },
    };
  },
  // mounted() {
  //   const dates = this.data.map((d) => d.date).reverse();
  //   const totals = this.data.map((d) => d.totals).reverse();
  //   this.renderChart(
  //     {
  //       labels: dates,
  //       datasets: [
  //         {
  //           label: this.label,
  //           data: totals,
  //         },
  //       ],
  //     },
  //     this.options
  //   );
  // },
};
</script>
<style scoped>
div {
  height: 500px;
}
</style>
