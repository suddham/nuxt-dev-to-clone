<template>
  <div class="page-wrapper">
    <div class="article-cards-wrapper">
      <article-card-block
        v-for="(article, index) in articles"
        :key="article.id"
        :article="article"
        class="article-card-block"
      />
    </div>
  </div>
</template>

<script>
import ArticleCardBlock from "~/components/blocks/ArticleCardBlock";
export default {
  components: {
    ArticleCardBlock
  },
  data() {
    return {
      currentPage: 1,
      articles: []
    };
  },
  async fetch() {
    const articles = await fetch(
      `https://dev.to/api/articles?tag=nuxt&state=rising&page=${this.currentPage}`
    ).then(res => res.json());

    this.articles = this.articles.concat(articles);
  }
};
</script>

<style scoped></style>
