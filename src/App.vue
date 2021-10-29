<template lang="pug">
  #app
    pm-header

    router-view

    pm-footer
</template>

<script>
import PmFooter from '@/components/layouts/Footer.vue'
import PmHeader from '@/components/layouts/Header.vue'

export default {
  name: 'app',

  components: { PmFooter, PmHeader }

}
</script>

<style lang="scss">
@import './scss/main.scss';
  .results {
    margin-top: 50px;
  }

  .is-active {
    border: 3px #48c78e solid;
  }
</style>
