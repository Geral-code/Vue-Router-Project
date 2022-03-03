<template>
 <div class="container">
   <h1 class="text-center"> Información del Usuario</h1>
   <table class="table">
     <thead>
       <tr>
         <th>Nombre</th>
         <th>Nick</th>
         <th>Email</th>
         <th>Dirección</th>
       </tr>
     </thead>
     <tbody>
       <tr>
         <td>{{user.name}}</td>
         <td>{{user.username }}</td>
         <td>{{user.email}}</td>
         <td>{{ user.address?.street}} - {{user.address?.suite}}</td>
       </tr>
     </tbody>
   </table>
 </div>
</template>

<script>
 export default {
   data() {
     return {
       user: {}
     }
   },
   methods: {
     async mostrarUser() {
      try {
        const data = await fetch(`https://jsonplaceholder.typicode.com/users/${this.$route.params.id}`);
        const getUser = await data.json();
        this.user = getUser;
      
      } catch (error) {
        console.log(error);
        throw error;
      }
     }
   },
   created() {
     this.mostrarUser();
   }
 }
</script>

<style>

</style>