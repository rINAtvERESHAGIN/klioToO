<template>
  <b-carousel-slide :img-src="banner.img">
      <h1 v-if="banner.show_content" v-html="banner.name"></h1>
      <div v-html="banner.content" class="banner-content"></div>
      <b-link :href="banner.link">
        <b-button squared size="lg" :class="`btn-${banner.btn_color}`">{{ banner.btn_text }}</b-button>
      </b-link>
  </b-carousel-slide>
</template>

<script>
export default {
  props: ['bannerData'],
  data () {
    return {
      banner: this.bannerData
    }
  }
}
</script>

<style>

</style>
