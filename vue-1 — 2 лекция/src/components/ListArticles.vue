<template>
    <main class="list-articles">
      <div class="list-articles__container">
        <div class="list-articles__list">
          <CardArticle
            v-for="item in newsList"
            :key="item.id"
            :id="item.id"
            :title="item.title"
            :description="item.description"
            class="list-articles__card"
          />
        </div>
      </div>
    </main>
  </template>
  
<script>
import CardArticle from "@/components/card/CardArticle.vue";

export default {
  components: {
    CardArticle,
  },
  data() {
    return {
      newsList: [],
    };
  },
  methods: {
    getNewsList() {
      this.$axios("https://jsonplaceholder.typicode.com/posts").then(
        (response) => {
          if (response) {
            this.newsList = response.data.map((item) => {
              item.description = item.body;
              delete item.body;
              return item;
            });
          }
        }
      );
    },
  },
  created() {
    this.getNewsList();
  }
};
</script>

<style lang="less">
.list-articles {
  &__container {
    .container();
  }
  &__card {
    margin-bottom: 15px;
  }
}

</style>