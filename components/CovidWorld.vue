<template>
  <div class="h-100">
    <b-card v-if="covidWorld" class="h-100">
      <template #header>
        <h3 class="mb-0">สถานการณ์โดยรวมของโลก</h3>
      </template>
      <b-list-group>
        <b-list-group-item
          class="d-flex justify-content-between align-items-center"
        >
          ผู้ติดเชื้อทั้งหมด
          <b-badge variant="warning" pill>
            {{ covidWorld.cases | numberFormat }} ราย
          </b-badge>
        </b-list-group-item>
        <b-list-group-item
          class="d-flex justify-content-between align-items-center"
        >
          รักษาหายแล้ว
          <b-badge variant="warning" pill>
            {{ covidWorld.recovered | numberFormat }} ราย
          </b-badge>
        </b-list-group-item>
        <b-list-group-item
          class="d-flex justify-content-between align-items-center"
        >
          กำลังรักษา
          <b-badge variant="warning" pill>
            {{ covidWorld.active | numberFormat }} ราย
          </b-badge>
        </b-list-group-item>
        <b-list-group-item
          class="d-flex justify-content-between align-items-center"
        >
          เสียชีวิต
          <b-badge variant="warning" pill>
            {{ covidWorld.deaths | numberFormat }} ราย
          </b-badge>
        </b-list-group-item>
      </b-list-group>
    </b-card>
    <b-spinner v-else type="grow" variant="primary" />
  </div>
</template>

<script>
export default {
  name: 'CovidWorld',
  filters: {
    numberFormat(val) {
      return Intl.NumberFormat('th-Th').format(val);
    }
  },
  data() {
    return {
      covidWorld: null
    };
  },
  async mounted() {
    const world = await this.$axios.$get('/all');
    this.covidWorld = world;
  }
};
</script>
