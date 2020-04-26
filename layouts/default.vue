<template>
  <div class="font-default">
    <navbar />
    <br />
    <nuxt />
  </div>
</template>

<script>
import Navbar from '~/components/Navbar.vue';

export default {
  name: 'Default',
  components: {
    Navbar
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Sarabun:wght@500&display=swap');

.font-default {
  font-family: 'Sarabun', sans-serif;
}
</style>
