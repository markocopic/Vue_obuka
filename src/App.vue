<template>
  <div id="main">
    <img alt="Vue logo" src="./assets/logo.png">
     <h1>{{title}}</h1>
<!-- 
    <h3>Volume: {{volume}}</h3>
    <button @click="volume--">Decrease</button>
    <button @click="volume++">Increase</button> -->



     <!-- <p @click="showRed = !showRed"
      class="red-x"
      :class="{'bg-red':showRed,'nova-klasa':nova}"> Petar Petrovic </p> -->

<!-- 
    <span>First name</span><input v-model="firstName" type="text"><br>
    <span>Last name</span><input v-model="lastName" type="text"><br>

    <p>{{ username }}</p> -->


      <!-- <button @click="a++">Add to A</button>
      <button @click="b++">Add to B</button>

     <p>Age + a = {{ addToA }}</p>
     <p>Age + b = {{ addToB }}</p> -->
    <!-- <ul>
      <li v-for="(name,index) in names" :key="index" 
      @click="name.showRed = !name.showRed"
       :class="{'bg-red':name.showRed}"> {{name.name}} -->
         <!-- <span @click="removeName(index)" class="red-x">X</span> -->
      <!-- </li>
    </ul>
    <input v-if="listFull" @keyup.enter="addName()" v-model="inputName" type="text">   -->
    <!-- <button @click="addName()">Add Name</button> -->
    <!-- <br>
    <small style="color:red;" v-if="emptyValue">Empty value !!!</small> -->
    <!-- <button v-if="show" @click="hideTitle()">Hide title</button>
    <button v-else @click="show=true">Show title</button> -->
    <!-- <button @click="title = 'DRUGI NAZIV'">Change Title</button> -->
    <!-- <button @click="changeNumber('minus')">-</button><br>
    <h3>{{number}}</h3>
    <button @click="changeNumber('plus')">+</button> -->
    <!-- <input v-model="name" type="text"> -->
    <!-- <button @click="addName()">Add Name</button> -->
    <!-- <p>{{name}}</p> -->
    <!-- <input type="radio" value="One" v-model="picked">
    <label for="One">One</label>
    <br>
    <input type="radio" value="Two" v-model="picked">
    <label for="Two">Two</label>
    <br>
    <span>Picked: {{picked}}</span> -->
    <!-- <button @click="catchEvent($event)">Catch Event</button>
    <div class="area" @mousemove="getCoo($event)" @mouseleave="resetCoo()">
      <p>{{x}}, {{y}}</p>
    </div> -->
<!-- <br>
    <input type="checkbox" name="Milos" id="milos" value="Milos" v-model="names">
    <label for="milos">Milos</label>
    <br>
    <input type="checkbox" name="Zoran" id="zoran" value="Zoran" v-model="names">
    <label for="zoran">Zoran</label>
    <br>
    <input type="checkbox" name="Goran" id="goran" value="Goran" v-model="names">
    <label for="goran">Goran</label>
    <br>
    <span>Names: {{names}}</span> -->

  <!-- <select v-model="selected">
    <option v-for="option in options" 
    :value="option"
    :key="option.value">
      {{option.text}}
    </option>
  </select>
  <p>{{ selected }}</p> -->

  <button @click="getData()">Get data from service</button>

  <ul>
    <li v-for="user in users" :key="user.id">
      {{user.name}} , {{user.address.street}} - {{user.address.suite}}

    </li>
  </ul>



  </div>
</template>

<script>
import axios from 'axios'

export default {
  data(){
    return{
      volume:0,
      showRed:true,
      age:20,
      a:0,
      b:0,
      title: 'VUE OBUKA',
      number: 0,
      name:'Mirko',
      inputValue:'',
      picked:'Two',
      x:0,
      y:0,
      // names:[
      //   {name:'Goran', showRed:false},
      //   {name:'Zoran', showRed:false},
      //   {name:'Petar', showRed:false},
      //   {name:'Jovan', showRed:false}
      //   ],
      inputName:'',
      emptyValue:false,
      selected:'',
      options:[
        {value:1, text:'Jedan'},
        {value:2, text:'Dva'},
        {value:3, text:'Tri'}
      ],
      firstName:'',
      lastName:'',
      users:[]
    }
  },
  watch:{
    volume(newVal,oldVal){
      if (newVal == 8 && oldVal<newVal) {
        alert('Too loud !!!')
      }
    }
  },
  computed:{
    listFull(){
      if (this.names.lenght > 4) {
        return false
      } else {
        return true
      }
    },
    username(){
      if (this.firstName && this.lastName) {
      return this.firstName.toUpperCase() +'.'+ this.lastName.toUpperCase()
      } else {
        return ''
      }
    },
    addToA(){
      console.log('Calculate A');
      return this.age + this.a
    },
    addToB(){
      console.log('Calculate B');
      return this.age + this.b
    }
  },
  methods:{
    getData(){
      axios.get('https://jsonplaceholder.typicode.com/users').then(
        response=>{
          console.log(response.data);
          this.users = response.data
        }
      )
    },
    removeName(i){
      this.names.splice(i,1)
    },
    addName(){
      if (this.inputName) {
        this.names.push(this.inputName)
        this.emptyValue = false
      }else{
        this.emptyValue = true
      }
      this.inputName = ''
    },
    hideTitle(){
      this.show = false
    },
    resetCoo(){
      this.x = 0
      this.y = 0
    },
    getCoo(e){
      this.x = e.offsetX
      this.y = e.offsetY
    },
    catchEvent(e){
      console.log('EVENT OBJEKAT',e);
    },
    changeNumber(operation){
      if (operation == 'plus') {
        this.number = this.number + 1
      } else if(operation == 'minus') {
        this.number = this.number - 1
      }
      console.log(this.number)

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
.area{
  background-color:light-grey;
  min-height: 500px;
  border: 1px solid grey;
}
.red-x{
  cursor: pointer;
  color:red;
}
.bg-red{
  background-color: red;;
}
</style>
