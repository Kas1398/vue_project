<template>
  <div  id="app">
    <h1>To-Do List</h1>
    <to-do-form @todo-added="addToDo"></to-do-form>
    <h2 id="list-summary" ref="listSummary" tabindex="-1">{{ listSummary }}</h2>
     <ul :aria-labelledby="list-summary" class="stack-large">
      <li v-for="item in ToDoItems" :key="item.id">
        <to-do-item  
          :label="item.label" 
          :done="item.done" 
          :id="item.id"
          @checkbox-changed="updateDoneStatus(item.id)"
          @item-deleted="deleteToDo"
          @item-edited="editToDo(item.id, $event)">
        </to-do-item>
      </li>
     </ul>
  </div>
</template>

<script>
import ToDoItemEditForm from "./components/ToDoItemEditForm.vue";
import ToDoItem from "./components/ToDoItem.vue";
import uniqueId from "lodash.uniqueid";
import ToDoForm from "./components/ToDoForm.vue";

export default {
  name:'App',
  components:{
    ToDoItem,
    ToDoForm,
    ToDoItemEditForm,
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
      list: "todo-list",
      summary: "todo-Ssummary"
    };
  },
  computed: {
    listSummary() {
      const numberFinishedItems = this.ToDoItems.filter((item) => item.done).length;
      return `${numberFinishedItems} out of ${this.ToDoItems.length} items completed`;
    },
  },
  methods: {
    addToDo(toDoLabel){
        this.ToDoItems.push({ id: uniqueId('todo-'), label: toDoLabel, done: false });
    },
  },
  
    updateDoneStatus(toDoId) {
      const toDoUpdate = this.ToDoItems.find((item)=> item.id === toDoId);
      toDoUpdate.done = !toDoUpdate.done;
  },
    deleteToDo(toDoId) {
      const itemIndex = this.ToDoItems.findIndex((item) => item.id === toDoId);
      this.ToDoItems.splice(itemIndex, 1);
      this.$refs.listSummary.focus();
  },
    editToDo(toDoId, newLabel) {
      const toDoEdit = this.ToDoItems.find((item) => item.id === toDoId);
      toDoEdit.label = newLabel;
  },
};
</script>

<style>
#app {
  font-family: Avenir, Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  margin-bottom: 0;
  }
  .stack-small > * + * {
    margin-top: 1.25rem;
  }
  .stack-large > * + * {
    margin-top: 2.5rem;
  }
  @media screen and (min-width: 550px) {
    .stack-small > * + * {
      margin-top: 1.4rem;
    }
    .stack-large > * + * {
      margin-top: 2.8rem;
    }
  }
  /* End global Styles */
  #app {
    background: #fff;
    margin: 2rem 0 4rem 0;
    padding: 1rem;
    padding-top: 0;
    position: relative;
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 2.5rem 5rem 0 rgba(0, 0, 0, 0.1);
  }
  @media screen and (min-width: 550px) {
    #app {
      padding: 4rem;
    }
  }
  #app > * {
    max-width: 50rem;
    margin-left: auto;
    margin-right: auto;
  }
  #app > form {
    max-width: 100%;
  }
  #app h1 {
    display: block;
    min-width: 100%;
    width: 100%;
    text-align: center;
    margin: 0;
    margin-bottom: 1rem;
  }
</style>