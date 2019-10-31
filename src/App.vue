<template>
  <div id="app">
    <h1 class="mt-3">{{ title }}</h1>
    <div class="container" :class="{update4:aplicador4}">    

      <table class="table">
          <thead>
              <tr>
                  <th>ID</th>
                  <th>User</th>
                  <th>Site</th>
                  <th>Password</th>
                  <th>Tratar</th>
              </tr>
          </thead>
          <tbody v-for="user in users" :key="user.id">
              <tr>
                  <td>{{ user.id }}</td>
                  <td>{{ user.user }}</td>
                  <td>{{ user.site }}</td>
                  <td>{{ user.password }}</td>
                  <td><input class="btn btn-danger" @click="updateSenhas(user.id, user.user, user.site, user.password)" type="button" :value="user.id"></td>
              </tr>
          </tbody>
      </table>
      </div>
    <button class="btn btn-primary" @click="aplicador4 = !aplicador4  ">List</button> 
    <button class="btn btn-primary" @click="aplicador3 = !aplicador3">Find</button>    
    <button class="btn btn-primary" @click="aplicador2 = !aplicador2">Salve</button>    
    <!-- <button class="btn btn-primary"  @click="aplicador = !aplicador">Update</button>     -->
    <findBySite :class="{update3:aplicador3}" msg="SENHAS"></findBySite> 
    <br>
    <update-senhas :class="{update:aplicador}" :id="id" :user="user" :site="site" :password="password"/>      
    <save-senhas  :class="{update2:aplicador2}"></save-senhas>
    
     
  </div>
  
</template>

<script>
import FindBySite from './components/FindBySite.vue'
import UpdateSenhas from './components/UpdateSenhas.vue'
import SaveSenhas from './components/SaveSenhas.vue'



export default {
  name: 'app',
  components: {
    FindBySite,
    UpdateSenhas,
    SaveSenhas,    
  },
  data(){
     return {
       aplicador: true,
       aplicador2: true,
       aplicador3: true,
       aplicador4: true,
        title: "Your passwords:",
        senhas: null,
        users: null,
        id: null,
        ids : [],
        user: null,
        site: null,
        password: null,
        element: null
     }  
  },
  methods: {
    
    getSenhas(){      
            fetch('http://localhost:8081/senhas')
            .then(resp => resp.json())
            .then(senhas=>  this.users = senhas)            
            return this.users
    },

    updateSenhas: function (id, user, site, password) {               
                var index = this.users.indexOf(user)
                this.id = id
                this.user = user
                this.site = site
                this.password = password
                this.users.splice(index, 1)
                window.console.log(this.id + ' - ' + this.user + ' - ' + this.site + ' - ' + this.password)
                this.aplicador = !this.aplicador               
        }    
  },
  mounted() {
        this.getSenhas()
        
    }


}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button{
  margin: 2px;
  margin-bottom: 4px;
}

.update{
  display: none;
}
.update2{
  display: none;
}
.update3{
  display: none;
}

.update4{
  display: none;
}
</style>
