<template>
  <b-card>
    <template #header>
      <h3 class="mb-0">อัตราส่วนทั้งหมด</h3>
    </template>
    <canvas ref="pie" />
  </b-card>
</template>

<script>
import Chart from 'chart.js';

export default {
  name: 'PieChart',
  props: {
    cases: {
      type: Number,
      default: 0
    },
    recovered: {
      type: Number,
      default: 0
    },
    active: {
      type: Number,
      default: 0
    },
    deaths: {
      type: Number,
      default: 0
    }
  },
  mounted() {
    this.$nextTick(() => {
      const ctx = this.$refs.pie.getContext('2d');
      const pieChart = new Chart(ctx, {
        type: 'pie',
        data: {
          labels: [
            'ผู้ติดเชื้อทั้งหมด',
            'รักษาหายแล้ว',
            'กำลังรักษา',
            'เสียชีวิต'
          ],
          datasets: [
            {
              labels: [
                'ผู้ติดเชื้อทั้งหมด',
                'รักษาหายแล้ว',
                'กำลังรักษา',
                'เสียชีวิต'
              ],
              data: [this.cases, this.recovered, this.active, this.deaths],
              backgroundColor: ['#f0ad4e', '#5cb85c', '#5bc0de', '#d9534f']
            }
          ]
        }
      });
      return pieChart;
    });
  }
};
</script>
