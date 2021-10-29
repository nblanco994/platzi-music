<template lang="pug">
  .container
    .columns
      .column.is-5.is-offset-4
        .notification.has-text-centered(v-bind:class="{ 'has-background-primary-dark':isOk, 'is-danger': !isOk }")
          slot(name="body") Algo anduvo mal...
</template>

<script>
export default {
props: { isOk: { Type: Boolean } }
}
</script>
<style lang="scss" scoped>
.notification {
    margin: 10px;
}
</style>