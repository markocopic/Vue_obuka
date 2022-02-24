<template>
  <div id="main">

    <div v-if="!logged" class="login">
      <span>Username: </span>
      <input :class="{'red':noUsername}" v-model="username" type="text"><br>
      <span>Password: </span>
      <input :class="{'red':noPassword}" v-model="password" type="password"><br>
      <button @click="login">Login</button>
    </div>

    <div v-else>
      <div>
        <h3>Classes:</h3>
        <select name="" id="" v-model="idClass">
          <option v-for="cls in classes" :value="cls.id" :key="cls.id">{{cls.name}}</option>
        </select>
      </div>

      <div v-if="classSelected">
        <h3>Subclasses:</h3>
        <select name="" id="">
          <option v-for="cls in subclasses" :value="cls.id" :key="cls.id">{{cls.name}}</option>
        </select>
      </div>
      

    </div>  

  </div>
</template>

<script>
 import axios from 'axios'

export default {
  data(){
    return{
     username:'',
     password:'',
     noUsername:false,
     noPassword:false,
     logged:false,
     classes:[],
     idClass:null,
     classSelected:false,
     subclasses:[]
    }
  },
  mounted(){
    
  },
  watch:{
    idClass(newVal){
      if (newVal) {
        
        this.getClasses(newVal)
      }
    }
  },
  computed:{
  },
  methods:{
    login(){
      if (!this.username) {
        this.noUsername = true
      } else if(!this.password){
        this.noPassword = true

      }
      else {
        this.noUsername = false
        this.noPassword = false
        axios.post('http://fd2c1-d.eps.local:8080/fadoc/eps_dev/vue_els_demo/login',{
          username:this.username,
          password:this.password
        }).then(res=>{
          console.log(res.data);
          if (res.data.Success) {
            this.logged = true
            localStorage.setItem('token',res.data.Token)
            this.getClasses(null)
          }
        })
      }
    },
    getClasses(idClass){
      axios.get('http://fd2c1-d.eps.local:8080/fadoc/eps_dev/vue_els_demo/class',{
        params:{
          id_class:idClass
        },
        headers:{
          'custom-header':'vrednost',
          'Authorization':'Bearer ' + localStorage.getItem('token')
        }
      })
      .then(res=>{
        if (idClass) {
          this.subclasses = res.data.classes
          this.classSelected = true
        } else {
          this.classes = res.data.classes
          this.classSelected = false
        }
        
      })
    }
  }
}
</script>

<style>
#main {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.login{
  width:30%;
  margin: 20px auto;
  background-color: lightcyan;
  border: 1px solid blue;
}
span, input, button{
  margin: 5px;
  padding: 3px;
}
.red{
  border:1px solid red;
}
</style>
