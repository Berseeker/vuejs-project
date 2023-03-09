<script setup>
import {ref, computed} from 'vue';

import BlogPost from './components/BlogPost.vue'
import PaginatePost from './components/PaginatePost.vue'

const posts = ref([]);
const postXpage = 10;
const inicio = ref(0)
const fin = ref(postXpage)

const favorito = ref('');

const postFavorito = (title) => {
  favorito.value = title
}

const next = () => {
  inicio.value += + postXpage
  fin.value += + postXpage
}

const prev = () => {
  inicio.value += -postXpage
  fin.value += -postXpage
}

fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res => res.json())
  .then(data => posts.value = data)

const maxLength = computed(() => posts.value.length);

</script>

<template>
  <div class="container">
    <h1>APP TEST</h1>
    <h2>Mi Post favorito: {{ favorito }}</h2>
    <PaginatePost 
      class="mb-2"
      :inicio="inicio"
      :fin="fin"
      :maxLength="maxLength"
      @next="next"
      @prev="prev"></PaginatePost>
    <BlogPost 
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :title="post.title"
      :id="post.id" 
      :body="post.body"
      @postFavorito="postFavorito"
      class="mb-2"></BlogPost>
  </div>
</template>