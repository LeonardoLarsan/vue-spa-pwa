<template>
  <article>
    <header>
      <div>
        <data v-text="article.date"/>
        <img :src="article.banner">
        <h1 v-text="article.title"/>
        <h2 v-text="article.subTitle"/>
      </div>
      <h3>
        <i v-text="article.description"/>
      </h3>
    </header>
    <div v-for="(item, index) in article.content" :key="'contentItem'+index">
      <p v-if="item.type==='text'" v-text="item.value"/>
      <q v-if="item.type==='quote'" v-text="item.value"/>
      <quote v-if="item.type==='quoteFirm'">
        <p v-text="item.value1"></p>
        <footer v-text="item.value2"/>
      </quote>
      <img v-if="item.type==='image'" :src="item.value">
      <figure v-if="item.type==='photo'">
        <img :src="item.value1">
        <description v-text="item.value2"/>
      </figure>
      <h4 v-if="item.type==='title'" v-text="item.value"/>
      <h6 v-if="item.type==='subTitle'" v-text="item.value"/>
      <h7 v-if="item.type==='description'" v-text="item.value"/>
      <a v-if="item.type==='link'" :h-ref="item.value"/>
      <hr v-if="item.type==='separator'">
      <div v-if="item.type==='frame'" v-text="item.value"/>
      <div v-if="item.type==='block'" v-text="item.value"/>
      <div v-if="item.type==='bold'" v-text="item.value"/>
      <div v-if="item.type==='note'" v-text="item.value"/>
      <ul v-if="item.type==='list'">
        <li v-for="(value, index) in item.value" v-text="value" :key="'li'+index"/>
      </ul>
      <ol v-if="item.type==='orderList'">
        <li v-for="(value, index) in item.value" v-text="value" :key="'li'+index"/>
      </ol>
      <div v-if="item.type==='detail'">
        <div v-for="(value, index) in item.value" :key="'detail'+index">
          <label v-text="value.value1"/>
          <a v-text="value.value2"/>
        </div>
      </div>
    </div>
    <footer v-text="article.form"/>
  </article>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import { setTimeout } from "timers";

export default {
  components: {},
  methods: {
    ...mapActions(["seeArticle"]),
    disFormartLink(titleUrl) {
      return titleUrl.replace(/_/g, " ");
    }
  },
  computed: mapGetters({ article: "getArticle" }),
  mounted() {
    this.seeArticle({
      date: this.$route.params.date,
      title: this.disFormartLink(this.$route.params.title)
    });
  }
};
</script>