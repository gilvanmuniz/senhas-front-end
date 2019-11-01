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
                  <td><input class="btn btn-dark" @click="updateSenhas(user.id, user.user, user.site, user.password)" type="button" :value="'Update'"></td>
                  <td><input class="btn btn-danger" @click="deleteSenhas(user.id, user.user, user.site, user.password)" type="button" :value="'Delete'"></td>
              </tr>
          </tbody>
      </table>
      </div>
      
    <!-- <button class="btn btn-primary"  @click="aplicador = !aplicador">Update</button>     -->
    <findBySite :class="{update3:aplicador3}" msg="SENHAS"></findBySite> 
    <br>
    <button class="btn btn-primary" @click="showList()">List</button> 
    <button class="btn btn-primary" @click="openGetSenhas()">Find</button>    
    <button class="btn btn-primary" @click="save()">Save</button> 
    <update-senhas :class="{update:aplicador}" :id="id" :user="user" :site="site" :password="password"></update-senhas>      
    <save-senhas  :class="{update2:aplicador2}" :save="save"></save-senhas>
    
     
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
        senhas: {},
        users: null,
        id: null,
        ids : [],
        user: null,
        site: null,
        password: null,
        
     }  
  },
  methods: {
    
    getSenhas(){      
            fetch('http://localhost:8081/senhas')
            .then(resp => resp.json())
            .then(senhas=>  this.users = senhas)                      
            return this.users            

    },

    showList(){
        this.aplicador4 = !this.aplicador4
        if(!this.aplicador){
          this.aplicador = true;
        }
        if(!this.aplicador3){
          this.aplicador3 = true;
        }
        if(!this.aplicador2){
          this.aplicador2 = true;
        }
    },

    openGetSenhas(){
      this.aplicador3 = !this.aplicador3
       if(!this.aplicador){
          this.aplicador = true;
       }
       if(!this.aplicador2){
              this.aplicador2 = true;
       }
       if(!this.aplicador4){
              this.aplicador4 = true;
       } 
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
                if(!this.aplicador3){
                  this.aplicador3 = true;
                }
                if(!this.aplicador2){
                  this.aplicador2 = true;
                }
                if(!this.aplicador4){
                  this.aplicador4 = true;
                }               
    }, //updateSenhas_end
    
    deleteSenhas: function (id, user, site, password) {              
                this.senhas.id = id
                this.senhas.user = user
                this.senhas.site = site
                this.senhas.password = password                
                window.console.log(this.senhas)
                const json = JSON.stringify(this.senhas)
                var url = 'http://localhost:8081/senhas/' + this.senhas.id
                fetch(url, {
                  method: 'delete',
                    headers: {
                      'Accept': 'application/json',
                      'Content-Type': 'application/json'
                    },
                      body: json
                    })  
                    window.console.log(json)
                              
    }, //deleteSenhas_end

    save(){
      this.aplicador2 = !this.aplicador2
      if(!this.aplicador3){
        this.aplicador3 = true;
      }
      if(!this.aplicador4){
        this.aplicador4 = true;
      }
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
