<template>
  <div class="container" >
   
    <HeaderComp @addTodo="addTodo" />

    <MainComp :newTodo="newTodo" />


  </div>
</template>

<script>

import HeaderComp from './components/HeaderComp.vue';
import MainComp from './components/MainComp.vue';

export default {
  name: 'App',
  components: {
    HeaderComp,
    MainComp
  },
  data(){
    return{
      newTodo: ''
    }
  },
  methods:{
    addTodo(newTodo){
      this.newTodo = newTodo;
      console.log(newTodo);
    }
  }
}
</script>

<style lang="scss">
@import '~@fontsource/lato/index.css';
@import 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/css/all.css';
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
body{
    font-family: 'Lato';
}
.container{
    width: 90%;
    max-width: 1200px;
    margin: 0 auto;
}
</style>
