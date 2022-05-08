<script>
import {ref} from 'vue';
export default{
  setup(){
    
    const newTodo = ref('');
    const todos = ref([]);
    let id = 0;

    function addTodo(){
      if(newTodo.value == ''){
        console.log('Empty to do')
      }else{
        console.log(newTodo);
        todos.value.push({edit: id + "edit", id: id++, content: newTodo.value});
        newTodo.value = '';
        
      }
      
    }
    function deleteTodo(index){
      todos.value.splice(index, 1)
    }
    function editTodo(todo, edit){
      document.getElementById(todo.id).style.display='none';
      document.getElementById(edit).style.display='flex';
    }
    function saveTodo(todo, edit){
      document.getElementById(todo.id).style.display='flex';
      document.getElementById(edit).style.display='none';
    }
    return{
      id,
      todos,
      newTodo,
      addTodo,
      editTodo,
      deleteTodo,
      saveTodo
    }
  }
}
</script>

<template onload="save();">
 <header>
    <img alt="LKMX" class="logo" src="./assets/logo.png" width="125" height="120" />
    <h1>LKMX - Front-end</h1>
  </header>

  <div id="todoCard">

     <h2>To Do List</h2>
     <form @submit.prevent="addTodo">
       <input name="newTodo" v-model="newTodo">
       <button class="addBtn">Agregar</button>
     </form>
     <section v-if="todos.length == 0">
       <label> Aun no has agregado ningun Todo a tu lista</label>
     </section>
     <ul v-else>
     <li v-for="(todo, index) in todos" :key="todo.id">

        <div :id="todo.id" >
        <label  class="todoLabel"> {{todo.content}}</label>
        <button class="icon" @click="editTodo(todo, todo.edit)"><img src="./assets/icon-pen.svg"></button>
        <button class="icon" @click="deleteTodo(index)"><img src="./assets/icon-trash.svg"></button>
        </div>
        <form class="hide" :id="todo.edit"  @submit.prevent="saveTodo(todo, todo.edit)"  >
          <input name="newTodo" v-model="todo.content">
          <button class="icon"><img src="./assets/icon-disk.svg"></button>
        </form>
     </li>
     </ul>

  </div>
</template>

<style>
@import './assets/base.css';

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}
header {
  padding: 6px;
  line-height: 1.5;
  margin-bottom: 10%;
  
}
header h1 {
    font-weight: bolder;
    color: #3b465d;
}
h2{
  font-weight: bolder;
}
input{
  width: 80%;
  border-radius: 5px;
  padding: 4px;
  border: 2px solid #d7dadd ;

}
ul{
  background-color: #f3f5fb;
  
  width: 95%;
  border-radius: 5px;
}
li label{
  font-weight: bold;
  color: #313234;
  width: 80%;
}
li div{
  width: 100%;
  display: flex;
}
.hide{
  display: none;
}

section{
  background-color: #f3f5fb;
  padding: 4px;
  width: 100%;
  border-radius: 5px;
}
section label{
  font-weight: bold;
  color: #313234;
}
form{
  display: flex;
  width: 100%;
  padding: 7px;
  gap: 4px;
}
img{
  align-self: center;
}
.addBtn{
  border-radius: 7px;
  padding: 7px;
  border: 0px;
  width: 17%;
  background-color: #2e60cd;
  color: #fff;
  cursor: pointer;
}
.addBtn:hover{
  background-color: #23458f;
}
li{
  display: flex;
  align-content: center;
  gap: 10px;
}
ul{
  display: flex;
  flex-flow: column;
  gap: 5px;
  padding: 4px;
}
.icon{
  border: 1px;
  background-color: #fff;
  border: 1px solid #d7dadd;
  border-radius: 5px;
  align-self: flex-end;
  cursor: pointer;
}
.icon:hover{
  background-color: #ddf;
}
i{
  height: 25px;
  width: 25px;
  font-size: 12pt;
}

#todoCard{
    display: flex;
    flex-wrap: wrap;
    background-color: #fff;
    color: #000;
    align-items: center;
    box-shadow: #e8e7ec 0px 7px 5px 0px;
    border-radius: 4px;
    padding: 5px;
    max-width: 29rem; 
  }


@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
  }

  #app {
    
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
