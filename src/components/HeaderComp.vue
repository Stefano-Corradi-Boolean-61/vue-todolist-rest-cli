<template>
  <header>
    <h1 class="titolo">ToDo list</h1>

            <div class="new-todo">
                <!-- input del nuovo todo 
                con v-model.trim effetto il trim del value prima di associarlo al data
                -->
                <input 
                    v-model.trim="newTodo"
                    @keyup.enter="$emit('addTodo',newTodo)"
                    type="text" placeholder="Nuovo todo">
                <button
                    @click="$emit('addTodo',newTodo)"
                >Aggiungi</button>
            </div>
  </header>
</template>

<script>
export default {
  name: "HeaderComp",
  data(){
    return{
      newTodo:''
    }
  }
}
</script>

<style lang="scss" scoped>
header{
  .titolo{
      text-align: center;
      margin: 30px;
  }

  .new-todo{
      text-align: center;
      input{
        padding: 10px 20px;
        border-radius: 10px;
        width: 300px;
        border-width: 1px;
        margin-right: 20px;
    }
    button{
        padding: 10px 20px;
        border-radius: 10px;
        border-width: 1px;
        margin-right: 20px;
        cursor: pointer;
    }
  }

}
</style>