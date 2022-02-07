<template>
  <div class="home">
    <Header subtitle="Home" />
    <img alt="Vue logo" src="../assets/tennis_logo.jpg">
  </div>
</template>

<script>

import Header from '@/components/Header.vue';

export default {
  name: 'Home',
  components: {
    Header
  }
}
</script>
