<template>
 <div class="container mt-5 col-sm-6 offset-sm-3">
   <h3 class= "fst-italic text-center"> Listado de Usuarios</h3>
  <table class="table">
       <thead>
      <tr>
       <th>Nombre</th>
       <th>Nick</th>
       <th>Email</th>
       <th>Direccion</th>
      </tr>
      </thead>
      <tbody>
        <tr v-for="user of users" :key="user.id">
          <td>{{ user.name }}</td>
          <td>{{ user.username }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.address?.street}} - {{ user.address?.suite}}</td>
        </tr>

      </tbody>       
     </table>
 </div>  
</template>
<script>
export default {
  //https://jsonplaceholder.typicode.com/users/

  data(){
    return {
      users: []

    }
  },
  methods: {
    async consumirUsers(){
      try {
        const data = await fetch('https://jsonplaceholder.typicode.com/users/');
        const getUsers = await data.json();
        this.users = getUsers;
        console.log(this.users);
      } catch (error) {
        console.log(error);
        throw error;
      }
    },
  },
  created() {
    this.consumirUsers();
  }

}
</script>

<style>

</style>