<template>
  <b-container>
    <div v-if="covidTotal">
      <fieldset class="border p-3">
        <legend :title="lastUpdated" class="w-auto">
          <h2>สถานการณ์ในไทย</h2>
        </legend>
        <covid-thailand v-bind="covidTotal" />
      </fieldset>
      <br />
      <b-row>
        <b-col>
          <pie-chart v-bind="covidTotal" />
        </b-col>
        <b-col>
          <covid-world />
        </b-col>
      </b-row>
    </div>
    <div v-else class="text-center">
      <b-spinner variant="primary" type="grow" label="Spinning" />
    </div>
  </b-container>
</template>

<script>
export default {
  components: {
    CovidThailand() {
      return import('~/components/CovidThailand.vue');
    },
    CovidWorld() {
      return import('~/components/CovidWorld.vue');
    },
    PieChart() {
      return import('~/components/PieChart.vue');
    }
  },
  data() {
    return {
      covidTotal: null,
      options: {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      }
    };
  },
  computed: {
    lastUpdated() {
      const lastDate = new Date(this.covidTotal.updated).toLocaleDateString(
        'th-Th',
        this.options
      );
      const lastTime = new Date(this.covidTotal.updated).toLocaleTimeString(
        'th-Th'
      );
      return `อัพเดทครั้งล่าสุดเมื่อ ${lastDate} ${lastTime} น.`;
    }
  },
  async mounted() {
    const data = await this.$axios.$get(
      'https://corona.lmao.ninja/v2/countries/thailand'
    );
    this.covidTotal = data;
  }
};
</script>
