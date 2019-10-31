<template>
  <div class="container">
    <h3>UPDATE PASSWORDS</h3>
      <form @submit.prevent="updateSenhas()" class="form-group" action="http://localhost:8081/senhas/id" method="put">
      <div class="form-row">       
        <input name="id" id="senha.id" class="form-control col-sm-8" type="hidden" v-model="id" >  
      </div>
      <div class="form-row">
        <label id="senha.user" for="usuario" class="col-sm-2 col-form-label" >User:</label>
        <input name="user" :placeholder="'atualizar o ' + user" class="form-control col-sm-8" type="text" v-model="senhas.user">  
      </div>
      <div class="form-row">
        <label  for="usuario" class="col-sm-2 col-form-label" >site:</label>
        <input :placeholder="'atualizar o '+ site" name="site" class="form-control col-sm-8" type="text" v-model="senhas.site" >  
      </div>
      <div class="form-row">
        <label for="usuario" class="col-sm-2 col-form-label" >Password:</label>
        <input :placeholder="'atualizar a senha'"  name="pass" class="form-control col-sm-8" type="password" v-model="senhas.password">  
      </div>
          <button class="btn btn-secondary"  type="submit">Update</button>
      </form>
  </div>
</template>

<script>


export default {
 data(){
   return  {
     senhas :{
       sid:null,
       user:null,
       site:null,
       password:null

     }
    
   }
 },
   props: {
        id:Number,    
        user: String,
        site: String,
        password: String 
   },
  methods: {
      updateSenhas(){               
      this.senhas.sid = this.id
      const json = JSON.stringify(this.senhas)
      var url = 'http://localhost:8081/senhas/' + this.id
      fetch(url, {
        method: 'put',
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          },
            body: json
          })  
          window.console.log(json)
                    
  } //updateSenhas end
  }

} //export default end
</script>

<style scoped>

</style>        
          
   
        
         
        
 