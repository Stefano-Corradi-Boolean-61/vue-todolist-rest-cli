<template>
       <div class="todo-container">

                <!-- nel ciclo passo l'index perché mi serve per poter eliminare il singolo elemento
                con v-if stampo la lista oppure il messaggio di lista vuota
                -->
                <ul v-if="todos.length > 0">

                    <li 
                    v-for="(todo, index) in todos"
                    :key="index"
                    @click="toggleDone(index, todo.id)"
                    :class="{'done' : todo.done}"
                    >
                        <span>
                            {{todo.text}}</span>
                        <i 
                            @click.stop="removeTodo(index, todo.id)"
                            class="fa-solid fa-trash-can"></i>
                    </li>

                </ul>
                <h2 v-else>Non ci sono ToDo</h2>

            </div>
</template>

<script>
import axios from 'axios';
export default {
  name: "MainComp",
  mounted(){
    this.getApi()
  },
  props:{
    newTodo: String
  },
  watch:{
    // watch "vede" un data o una props quando cambia
    // si deve chiamare con lo stesso nome e riceve come primo parametro il nuovo status e come secondo il vecchio
    newTodo(newData, oldData){
      this.postTodo();
      console.log('sono cambiato da ',oldData, 'a', newData);
    }
  },
  data(){
    return{
      endPoint: 'http://localhost:3000/todos/',
      todos:[]
    }
  },
  methods:{
    postTodo(){
      axios.post(this.endPoint,{
        text: this.newTodo,
        done: false
      }).then(r => {
        console.log(r.data);
        this.getApi();
      })
    },
    toggleDone(index, id){
      axios.patch(this.endPoint + id, {
        done: !this.todos[index].done
      }).then(r => {
        console.log(r.data);
        this.getApi();
      })
    },
    getApi(){
      axios.get(this.endPoint)
      .then(r => {
        this.todos = r.data;
        console.log(r.data);
      })
    },
    addTodo(){
      // il v-model del input (newTodo) deve essere almene lungo 2 caratteri
      if(this.newTodo.length > 1) {
        // lo pusho nell'array principale
        const newTodoToPush = {
          text: this.newTodo,
          done: false
        }
        this.todos.push(newTodoToPush);
        // resetto
        this.newTodo = '';
      }   
    },
    removeTodo(index, id){

      // confirm restituisce true o false (ok, annulla)
      if(confirm(`Sei sicuro di eliminare: ${this.todos[index]}?`)){
        // effettuo lo splice in base all'index passato
        axios.delete(this.endPoint + id)
          .then(r => {
            console.log(r);
            this.getApi();
          })
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.todo-container{
    background-color: rgb(236, 234, 234);
    padding: 30px;
    border-radius: 10px;
    margin: 40px 20px;
    ul{
        list-style: none;
    }
    ul li{
        display: flex;
        justify-content: space-between;
        padding: 15px;
        border-bottom: 1px solid black;
        &:hover{
            background-color: white;
        }
        &.done span{
            text-decoration: line-through;
        }
        i{
          color: gray;
          cursor: pointer;
          &::hover{
              color: black;
          }
        }
    }
}

</style>