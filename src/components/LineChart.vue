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
    chartColours: {
      type: Object,
    },
  },
  data() {
    return {
      data: {
        labels: this.chartData.map((d) => d.date).reverse(),
        datasets: [
          {
            label: this.label,
            backgroundColor: this.chartColours.backgroundColor,
            borderColor: this.chartColours.borderColor,
            data: this.chartData.map((d) => d.total).reverse(),
          },
        ],
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
      },
    };
  },
};
</script>
<style></style>
