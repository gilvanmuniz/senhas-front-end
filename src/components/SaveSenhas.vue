<template>
  <div class="container">
    <h3>SAVE PASSWORDS</h3>
    
      <form @submit.prevent="salvarSenhas()" name="saveForm" class="form-group" action="http://localhost:8081/senhas">
      <div class="form-row">
        <label for="usuario" class="col-sm-2 col-form-label" >User:</label>
        <input name="user" class="form-control col-sm-8" type="text" v-model="senhas.user">  
      </div>
      <div class="form-row">
        <label for="usuario" class="col-sm-2 col-form-label" >site:</label>
        <input name="site" class="form-control col-sm-8" type="text" v-model="senhas.site">  
      </div>
      <div class="form-row">
        <label for="usuario" class="col-sm-2 col-form-label" >Password:</label>
        <input name="password" class="form-control col-sm-8" type="password" v-model="senhas.password">  
      </div>
          <button class="btn btn-secondary" >Save</button>
      </form>
  </div>
</template>

<script>


export default {
 data(){
    return {      
      senhas:{
        id:null,
        user:null,
        site:null,
        password:null
      }   
    }
  },

  props :{
    aplicador:Boolean,
    aplicador3:String,
    aplicador4:String,
    save: String
  },
  
    
  methods :{
     salvarSenhas(){       
       const json = JSON.stringify(this.senhas)
      fetch("http://localhost:8081/senhas", {
        method: 'post',
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          },
            body: json
          })  
          window.console.log(json);
          
          
                    
  } //saveSenhas end
}

} //export default end

</script>

<style scoped>

</style>