<template>
  <b-navbar toggleable="lg" type="dark" variant="info">
    <b-container>
      <b-navbar-brand href="#">
        Covid-19 Thailand
      </b-navbar-brand>
      <b-navbar-toggle target="nav-collapse" />
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="https://corona.lmao.ninja/" target="_blank">
            <b-badge variant="success">
              ใช้ API ของ Novel COVID API
            </b-badge>
          </b-nav-item>
          <b-nav-item v-if="updated">
            <b-badge variant="secondary">{{ lastUpdate }}</b-badge>
          </b-nav-item>
        </b-navbar-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item to="/">หน้าแรก</b-nav-item>
          <b-nav-item to="/about">เกี่ยวกับ</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-container>
  </b-navbar>
</template>

<script>
export default {
  name: 'Navbar',
  props: {
    lastUpdated: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      updated: null
    };
  },
  computed: {
    lastUpdate() {
      const options = {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      };
      const lastDate = new Date(this.updated).toLocaleDateString(
        'th-Th',
        options
      );
      const lastTime = new Date(this.updated).toLocaleTimeString('th-Th');
      return `อัพเดทครั้งล่าสุดเมื่อ ${lastDate} เวลา ${lastTime} น.`;
    }
  },
  mounted() {
    this.$nuxt.$on('status-updated', (d) => (this.updated = d));
  },
  beforeDestroy() {
    this.$nuxt.$off('status-updated');
  }
};
</script>
