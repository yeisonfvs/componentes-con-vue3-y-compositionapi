<script setup>
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';
import { onMounted, ref } from 'vue';

const posts = ref([]);
const postXpage = 10;
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true);

const favorito = ref('');

const cambiarFavorito = (id) => {
  favorito.value = id;
};

const next = () => {
  inicio.value = inicio.value + postXpage;
  fin.value = fin.value + postXpage;
};

const previus = () => {
  // inicio.value = inicio.value - postXpage;
  // fin.value = fin.value - postXpage;
  inicio.value += -postXpage;
  fin.value += -postXpage;
};

// onMounted(async () => {
//   // loading.value = true;
//   try {
//     const res = await fetch('https://jsonplaceholder.typicode.com/posts');
//     posts.value = await res.json();
//   } catch (error) {
//     console.log(error);
//   } finally {
//     setTimeout(() => {
//       loading.value = false;
//     },1000);
//   }
// });

// fetch('https://jsonplaceholder.typicode.com/posts')
//   .then((res) => res.json())
//   .then((data) => (posts.value = data))
//   .finally(() => {
//     setTimeout(() => {
//       loading.value = false;
//     }, 2000);
//   });

const fetchData = async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 1000);
  }
};
fetchData();
</script>

<template>
  <LoadingSpinner v-if="loading"></LoadingSpinner>

  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mi post favorito: {{ favorito }}</h2>

    <PaginatePost
      @next="next"
      @previus="previus"
      :inicio="inicio"
      :fin="fin"
      :maxLength="posts.length"
    ></PaginatePost>

    <BlogPost
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      :colorText="post.colorText"
      @cambiarFavoritoNombre="cambiarFavorito"
    >
    </BlogPost>
  </div>
</template>
