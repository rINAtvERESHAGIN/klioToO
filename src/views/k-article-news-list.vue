<template>
  <b-row class="content-section">
    <b-col cols="12" md="10" offset-md="1">
      <b-breadcrumb :items="breadcrumbs"></b-breadcrumb>
      <h1 v-if="contentType === 'articles'">Статьи</h1>
      <h1 v-else-if="contentType === 'news'">Новости</h1>
      <b-row v-if="infoContent && infoContent.length">
        <ArticleNewsCard v-for="item in infoContent" :key="item.id" :infoData="item" :infoType="contentType" />
      </b-row>
      <p v-else>К сожалению, данный раздел пуст</p>
    </b-col>
  </b-row>
</template>

<script>
import ArticleNewsCard from '../components/k-article-news-card.vue'

export default {
  name: 'k-article-news-card',
  metaInfo: {
    title: 'Статьи и новости',
    meta: [
      { vmid: 'description', name: 'description', content: 'Статьи и новости о ювелирном и зуботехническом оборудовании на сайте Интернет-магазина Клио' },
      { vmid: 'keywords', name: 'keywords', content: 'статьи, новости, Клио, интернет-магазин, ювелирное оборудование, инструмент для ювелиров, зуботехническое оборудование, ювелирная упаковка' }
    ]
  },
  components: {
    ArticleNewsCard
  },
  data () {
    return {
      breadcrumbs: null,
      contentType: this.$route.path.slice(1),
      infoContent: null
    }
  },
  mounted () {
    this.do_axios()
  },
  watch: {
    $route (to, from) {
      this.contentType = this.$route.path.slice(1)
      this.do_axios()
    }
  },
  methods: {
    getBreadcrumbs () {
      var currentPage = '...'
      if (this.contentType === 'articles') {
        currentPage = 'Статьи'
      } else if (this.contentType === 'news') { currentPage = 'Новости' }
      return [
        { text: 'Главная', to: { name: 'home' } },
        { text: currentPage, active: true }
      ]
    },
    do_axios () {
      this.$axios
        .get(`general/${this.contentType}/list`)
        .then(response => {
          this.infoContent = response.data
          this.breadcrumbs = this.getBreadcrumbs()
        })
    }
  }
}
</script>

<style>

</style>
