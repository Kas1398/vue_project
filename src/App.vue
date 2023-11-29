<template>
  <div  id="app">
    <h1>To-Do List</h1>
    <to-do-form></to-do-form>
     <ul>
      <li v-for="item in ToDoItems" :key="item.id">
        <to-do-item  
          :label="item.label" 
          :done="true" 
          :id="item.id "></to-do-item>
      </li>
     </ul>
  </div>
</template>

<script>
import ToDoItem from "./components/ToDoItem.vue";
import uniqueId from "lodash.uniqueid";
import ToDoForm from "./components/ToDoForm.vue";

export default {
  name:'App',
  components:{
    ToDoItem,
    ToDoForm,
  },
  data() {
    return {
      ToDoItems:[
        {id:uniqueId('todo-'), label: "Opiskele Vue.js", done: false},
        {id:uniqueId('todo-'), label: "Tee eka Vue.js app", done: true},
        {id:uniqueId('todo-'), label: "Pidä kivaa", done: true},
        {id:uniqueId('todo-'), label: "Tee to-do lista", done: false},
        {id:uniqueId('todo-'), label: "Ota opintopisteet kotiin", done: false},
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Arial, Helvetica, sans-serif;
  -webkit-font-something: antialiased;
  -moz-osx-font-something: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

</style>