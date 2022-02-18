<template>
  <div id="main">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>{{title}}</h1>
    <!-- <button @click="title = 'DRUGI NAZIV'">Change Title</button> -->
    <button @click="changeNumber('minus')">-</button><br>
    <h3>{{number}}</h3>
    <button @click="changeNumber('plus')">+</button>
  </div>
</template>

<script>

export default {
  data(){
    return{
      title: 'VUE OBUKA',
      number: 0
    }
  },
  methods:{
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
</style>
