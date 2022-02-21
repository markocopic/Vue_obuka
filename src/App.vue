<template>
  <div id="main">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <h1 v-if="show">{{title}}</h1>
    <ul>
      <li v-for="(name,index) in names" :key="index"> {{name}}
        <span @click="removeName(index)" class="red-x">X</span>
      </li>
    </ul>
    <input @keyup.enter="addName()" v-model="inputName" type="text"> -->
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
<br>
    <input type="checkbox" name="Milos" id="milos" value="Milos" v-model="names">
    <label for="milos">Milos</label>
    <br>
    <input type="checkbox" name="Zoran" id="zoran" value="Zoran" v-model="names">
    <label for="zoran">Zoran</label>
    <br>
    <input type="checkbox" name="Goran" id="goran" value="Goran" v-model="names">
    <label for="goran">Goran</label>
    <br>
    <span>Names: {{names}}</span>



  </div>
</template>

<script>

export default {
  data(){
    return{
      title: 'VUE OBUKA',
      number: 0,
      name:'Mirko',
      inputValue:'',
      picked:'Two',
      x:0,
      y:0,
      show:true,
      names:[],
      inputName:'',
      emptyValue:false
    }
  },
  methods:{
    removeName(index){
      this.names.splice(index,1)
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
</style>
