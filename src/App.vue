<template>
  <div>
    <loading :loading="loading"/>
    <search-control :onSearch="handleSearch"/>
    <article-list :articles="articles"/>
  </div>
</template> 

<script>

import SearchControl from './components/SearchControl.vue';
import ArticleList from './components/ArticleList.vue';
import Loading from './components/Loading.vue';
import { getArticles } from '../services/api.js';

export default {
  data() {
    return {
      articles: null,
      loading: false
    };

  },

  components: {
    ArticleList,
    SearchControl,
    Loading
  },

  methods: {
    handleSearch(keyword) {
      this.loading = true;

      getArticles(keyword).then(data => {
        this.articles = data.articles;
        this.loading = false;
      });
    }
  }
};
</script>