<template>
  <div class="hello container">
    <h1>{{ msg }}</h1>      
     
     <div>
       <input id="teste" type="text" v-on:keyup.enter="escolha()" v-model="user"/>
       <br/> 
       <br/>    
       <p>{{  usuario }}   -  {{ senha }}</p>       
     </div>

     <!-- <div>
       <input id="teste" type="text" v-model="user"/>
       <br/>      
       <button class="btn btn-success" v-on:click="escolha()"  >Procurar</button>
       <p>{{  usuario }}   - {{ senha }}</p>       
     </div> -->

     <!-- <ul>
       <li v-for="i in users" :key="i.id">
         <p v-if="user == i.site">{{ i.user }}  - {{ i.password }}</p>         
       </li>       
     </ul> -->
  
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {      
      users: null,
      id: null,
      user: null,
      usuario: null,
      senha: null    
    }
  },

  methods :{
     getSenhas(){      
      fetch('http://localhost:8081/senhas')
      .then(resp => resp.json())
      .then(senhas=>  this.users = senhas)
      return this.users
            
  },
   escolha: function(){    
    var i
    for(i of this.users){
      
        if(i.site == this.user){
          this.usuario = i.user
          this.senha = i.password
          this.user = ''          
        }     
        
    }
      
    
    //
    }
  
  },

  mounted() {
    this.getSenhas()
  }

  

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.container{

  border: solid 1px black;
  width: 50%;
  padding: 20px;
}
</style>
