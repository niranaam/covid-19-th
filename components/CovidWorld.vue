<template>
  <div>
    <div v-if="covidWorld" class="h-100">
      <b-card class="h-100">
        <template #header>
          <h3 class="mb-0">สถานการณ์โดยรวมของโลก</h3>
        </template>
        <b-list-group>
          <b-list-group-item :class="cssClass">
            ผู้ติดเชื้อทั้งหมด
            <b-badge variant="warning" pill>
              {{ covidWorld.cases | numberFormat }} ราย
            </b-badge>
          </b-list-group-item>
          <b-list-group-item :class="cssClass">
            รักษาหายแล้ว
            <b-badge variant="warning" pill>
              {{ covidWorld.recovered | numberFormat }} ราย
            </b-badge>
          </b-list-group-item>
          <b-list-group-item :class="cssClass">
            กำลังรักษา
            <b-badge variant="warning" pill>
              {{ covidWorld.active | numberFormat }} ราย
            </b-badge>
          </b-list-group-item>
          <b-list-group-item :class="cssClass">
            เสียชีวิต
            <b-badge variant="warning" pill>
              {{ covidWorld.deaths | numberFormat }} ราย
            </b-badge>
          </b-list-group-item>
        </b-list-group>
      </b-card>
    </div>
    <div v-else>
      <b-spinner type="grow" variant="primary" />
    </div>
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
      covidWorld: null,
      cssClass: 'd-flex justify-content-between align-items-center'
    };
  },
  async created() {
    const world = await this.$axios.$get('/all');
    this.covidWorld = world;
  }
};
</script>
