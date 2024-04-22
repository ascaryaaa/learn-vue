<template>
  <div>
    <h1>News Articles</h1>
    <ul>
      <li v-for="article in articles" :key="article.title">
        <a :href="article.url" target="_blank">{{ article.title }}</a>
        <p>{{ article.description }}</p>
        <img :src="article.urlToImage" alt="Article Image" style="max-width: 300px;">
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      articles: []
    };
  },
  mounted() {
    this.fetchArticles();
  },
  methods: {
    fetchArticles() {
      const apiUrl = 'https://newsapi.org/v2/everything?q=keyword&apiKey=c1c177f088e9441ea6b6f59d56a0313e';
      axios.get(apiUrl)
      .then(response => {
        this.articles = response.data.articles;
      })
      .catch(error => {
        console.error('Error fetching articles:', error);
      });
    }
  }
};
</script>
