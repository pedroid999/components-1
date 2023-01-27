<script setup>
import {onMounted, ref} from "vue";

  import PaginatePost from "@/components/PaginatePost.vue";
  import BlogPost from "./components/BlogPost.vue";
  import LoadingSpinner from "@/components/LoadingSpinner.vue";

  const posts = ref([])
  const postsXpage = 10
  const inicio =  ref(0)
  const fin = ref(postsXpage)
  const loading = ref(false)

  const favorito = ref('')
  const cambiarFavorito = (postFavorito) => {
    favorito.value = postFavorito
  }

  const next = () => {
    inicio.value += postsXpage
    fin.value += postsXpage
  }

  const previous = () => {
    inicio.value += -postsXpage
    fin.value += -postsXpage
  }

      const fetchData = async () => {
        try {
          loading.value=true
          const res = await fetch('https://jsonplaceholder.typicode.com/posts')
          posts.value = await res.json()
        } catch (error) {
          console(error)
        } finally {
          setTimeout(() => {
            loading.value=false
          }, 2000)
        }
      }
      fetchData()

</script>

<template>
    <LoadingSpinner v-if="loading"/>
    <div class="container" v-else>
      <h1>APP</h1>
      <h2 class="text-danger">Mis post favorito: {{ favorito }} </h2>

      <PaginatePost class="mb-2"
                    @nextPage="next"
                    @previousPage="previous"
                    :inicio="inicio"
                    :fin="fin"
                    :maxLength="posts.length"
      >
      </PaginatePost>

      <BlogPost class="mb-2" v-for="post in posts.slice(inicio,fin)"
                :key="post.id"
                :title="post.title"
                :id="post.id"
                :body="post.body"
                @cambiarFavoritoNombre="cambiarFavorito"
      >
      </BlogPost>
    </div>
</template>

<style>

</style>
