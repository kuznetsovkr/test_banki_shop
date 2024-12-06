<template>
  <div id="app" class="app-container">
    <Header @update-search="handleSearchUpdate" />
    <MainContent :search-query="searchQuery" />
    <Footer />
  </div>
</template>


<script>
import Header from './components/Header.vue';
import MainContent from './components/MainContent.vue';
import Footer from './components/Footer.vue';

export default {
  components: { Header, MainContent, Footer },
  data() {
    return {
      searchQuery: "",
    };
  },
  methods: {
    handleSearchUpdate(query) {
      this.searchQuery = query;
    },
  },
};
</script>

<style lang="scss">
@import './assets/scss/styles';
</style>