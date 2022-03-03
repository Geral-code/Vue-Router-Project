<template>
<div class="container mt-5 col-sm-6 offset-sm-3">
    <h3 class= "fst-italic text-center"> Listado de Usuarios</h3>
      <table class="table">
       <thead>
      <tr>
       <th>Nombre</th>
       <th>Nick</th>
       <th>Email</th>
       <th>Ciudad</th>
       <th>Compañia</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="user of users" :key="user.id" >
          <td> {{user.name}} </td>
          <td> {{user.username}}  </td>
          <td> {{user.email }}  </td>
          <td> {{user.address?.city}} </td>
           <td> {{user.company?.name}} </td>
      </tr>
      </tbody>       
     </table>
</div>
</template>
<script>
export default {
    // https://jsonplaceholder.typicode.com/users
    data(){
        return{
            users:[]
        }

        
    },
    methods: {
        async consumirUsers2() {
            try {
                const data = await fetch ('https://jsonplaceholder.typicode.com/users/');
                const getUsers2 = await data.json();
                this.users = getUsers2;
                console.log(this.users);

                
            } catch (error) {
                console.log(error);
                throw error;
                
            }

        },
    },
    created () {
        this.consumirUsers2();


    }
   

}
</script>

<style>

</style>