<template>
  <b-container>
    <div v-if="covidTotal">
      <fieldset class="border p-3">
        <legend class="w-auto">
          <h2>สถานการณ์ในไทย</h2>
        </legend>
        <covid-thailand v-bind="covidTotal" />
      </fieldset>
      <br />
      <b-row align-v="stretch">
        <b-col>
          <pie-chart v-bind="covidTotal" />
        </b-col>
        <b-col>
          <covid-world class="h-100" />
        </b-col>
      </b-row>
    </div>
    <div v-else class="text-center">
      <b-spinner variant="primary" type="grow" label="Spinning" />
    </div>
    <br />
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
      covidTotal: null
    };
  },
  async created() {
    const data = await this.$axios.$get('/countries/thailand');
    this.$nuxt.$emit('status-updated', data.updated);
    this.covidTotal = data;
  }
};
</script>
