<template>
  <div>
    <h1>Artigos</h1>
    <ul>
      <li v-for="article in articles" :key="article.title">
        {{ article.title }} - {{ article.author }}
        <p>{{ article.description }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import newsApi from '../services/news-api';

export default {
  data() {
    return {
      articles: [],
    };
  },
  mounted() {
    newsApi
      .get('/top-headlines?country=br&apiKey=aa52eaffb95149db935bbc9999e1c8ae')
      .then(response => {
        console.log(response)
        this.articles = response.data.articles;
      })
      .catch(error => {
        console.error(error);
      });
  },
};
</script>