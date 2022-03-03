<template>
  <div class="container mt-5">
    <h2 class="fst-italic text-center mb-5">Lista de Posts</h2>
    <div class="row" v-for="post of posts" :key="post.id">
      <div class="col">
        <h3>{{ post.title.charAt(0).toUpperCase() + post.title.slice(1) }}</h3>
        <!-- Autor -->
        <router-link :to="`/user/${post.userId}`">Autor</router-link>
        <!-- Contenido del post -->
        <p>{{ post.body }}</p>
        <button class="btn btn-secondary" @click="comentariosId(post.id)"> Ver Comentarios</button>
        
        <template v-for="comentarioFiltrado of comentariosFiltrados" :key="comentarioFiltrado.id">
         <div class="mt-3 col-sm-10 offset-sm-1" v-if="comentarioFiltrado.postId === post.id">
          <p class="fw-bold"> User: {{comentarioFiltrado.email}}</p>
          <br>
          <p>Respuesta</p>
          <p> {{comentarioFiltrado.body}}</p>
         </div>

        </template>
        <hr/>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'HomeView',
  components: {
  },
  data() {
    return {
      posts: [],
      comentarios: [],
      comentariosFiltrados: []
    }
  },
  methods: {
    comentariosId(id) {
      this.comentariosFiltrados = this.comentarios.filter(comentario => comentario.postId == id);
      console.log (this.comentariosFiltrados);

    },


    async consumirPosts() {
      try {
        const data = await fetch(`https://jsonplaceholder.typicode.com/posts`);
        const getposts = await data.json();
        this.posts = getposts;
        console.log(this.posts)
      } catch (error) {
        console.log(error);
        throw error;
      }
    },
    async consumirComentarios(){
      try {
        const data = await fetch(`https://jsonplaceholder.typicode.com/comments`);
        const getComentarios = await data.json();
        this.comentarios = getComentarios;
        console.log(this.comentarios);
      
      
      } catch (error) {
        console.log(error);
        throw error;
        
      }
    }

  },
  created() {
    this.consumirPosts();
    this.consumirComentarios();
  }
}
</script>

<style scoped>
 h3 {
   font-size: 16px !important;
 }

 a {
   text-decoration: none;
   color: #544e4e;
   background: bisque;
   padding: 2px 7px;
   border-radius: 5px;
   border: 1px solid grey;

 }
</style>
