<template lang="pug">
   section.hero.is-success
     .hero-head
       header.nav
         .container
            .nav-left.nav-item
              strong 🎵 Platzi Music
            .nav-right.nav-menu
              router-link.nav-item.has-text-white.ml-5(to="/") Buscar
              router-link.nav-item.has-text-white.ml-5(to="about") Nosotros
     .hero-body
        .container.has-text-centered
          h1.title Platzi Music
          h2.subtitle Canciones que estan ¡Vue-nísimas!
          pm-player
</template>

<script>
import PmPlayer from '@/components/Player.vue'

export default {
  components: { PmPlayer }
}
</script>

<style lang="scss" scoped>
  .nav-left {
    float: left;
  }
  .nav-right {
    float: right;
  }
</style>