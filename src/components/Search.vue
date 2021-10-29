<template lang="pug">
  main
    transition(name="move")
      pm-notification(v-show="showNotification", :isOk="isOk")
        p.has-text-white(slot="body", v-if="isOk") {{ searchMessage }}
        p(slot="body", v-else) No se encontraron resultados
    pm-loader(v-show="isLoading")
    section.section(v-show="!isLoading")
      nav.nav
        .container.has-text-centered
          input.input.is-primary.is-medium.mx-1(style="width: 33%", 
          type="text", 
          placeholder="Buscar canciones", 
          v-model="searchQuery", v-on:keyup.enter="search")
          a.button.is-success.is-medium.mx-1(v-on:click="search") Buscar
          a.button.is-primary.is-medium.mx-1 &times;
      .container.results
        .columns.is-multiline
          .column.is-one-quarter(v-for="t in tracks") 
            pm-track(v-blur="t.preview_url" v-bind:class="{ 'is-active': t.id === selectedTrack }", v-bind:track="t", v-on:select="setSelectedTrack")
</template>

<script>
import trackService from '@/services/track'

import PmTrack from '@/components/Track.vue'

import PmNotification from '@/components/shared/Notification.vue'
import PmLoader from '@/components/shared/Loader.vue'

export default {
  name: 'app',

  components: { PmTrack, PmLoader, PmNotification },

  data () {
    return {
      searchQuery: '',
      tracks: [],

      isLoading: false,

      showNotification: false,

      isOk: false,

      selectedTrack: ''
    }
  },

  computed: {
    searchMessage () {
      return `Encontrados: ${this.tracks.length}`
    }
  },

  watch: {
    showNotification () {
      if(this.showNotification) {
        setTimeout(() => {
          this.showNotification = false
        }, 3000);
      }
    }
  },

  methods: {
    search () {
      if(!this.searchQuery) { return }

      this.isLoading = true

      trackService.search(this.searchQuery).then(res => {
        if(res.tracks.total === 0) {
          this.isOk = false
        } else 
          this.isOk = true
          this.isLoading = false
          this.tracks = res.tracks.items
          this.showNotification = true
      })
    },
    setSelectedTrack (id) {
      this.selectedTrack = id
    }
  }
}
</script>

<style lang="scss">
  .results {
    margin-top: 50px;
  }

  .is-active {
    border: 3px #48c78e solid;
  }
</style>
