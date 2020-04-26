<template>
  <b-row class="text-center">
    <b-col>
      <b-card title="ผู้ติดเชื้อทั้งหมด">
        <b-card-text>
          <h1 :title="todayCase">{{ cases | numberFormat }}</h1>
          <small>ราย</small>
        </b-card-text>
      </b-card>
    </b-col>
    <b-col>
      <b-card title="รักษาหายแล้ว">
        <b-card-text>
          <h1>{{ recovered | numberFormat }}</h1>
          <small>ราย</small>
        </b-card-text>
      </b-card>
    </b-col>
    <b-col>
      <b-card title="กำลังรักษา">
        <b-card-text>
          <h1>{{ active | numberFormat }}</h1>
          <small>ราย</small>
        </b-card-text>
      </b-card>
    </b-col>
    <b-col>
      <b-card title="เสียชีวิต">
        <b-card-text>
          <h1 :title="todayDeath">{{ deaths | numberFormat }}</h1>
          <small>ราย</small>
        </b-card-text>
      </b-card>
    </b-col>
  </b-row>
</template>

<script>
export default {
  name: 'CovidThailand',
  filters: {
    numberFormat(val) {
      return Intl.NumberFormat('th-Th').format(val);
    }
  },
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
    },
    todayCases: {
      type: Number,
      default: 0
    },
    todayDeaths: {
      type: Number,
      default: 0
    }
  },
  computed: {
    todayCase() {
      if (this.todayCases) {
        return `เพิ่มขึ้น ${this.todayCases} ราย`;
      }
      return `ไม่เพิ่มขึ้น`;
    },
    todayDeath() {
      if (this.todayDeaths) {
        return `เพิ่มขึ้น ${this.todayCases} ราย`;
      }
      return `ไม่เพิ่มขึ้น`;
    }
  }
};
</script>
