<template>
  <div id="app">
    <div class="conteiner">
      <div class="header">
      <Header @task-add="onAddTask"/>
      </div>
      <ToDoList @remove-task="onRemoveTask" :needDoList="needDoList" @add-task="onAddTask"/>
    </div>
    
  </div>
  
</template>

<script>
import Header from './components/Header.vue';
import ToDoList from './components/ToDoList.vue';

export default {
  name: 'App',
  components: {
    Header,
    ToDoList
  },

  data(){
    return{
      needDoList:[],
      }
    },

  methods:{
    onAddTask(task){
      this.needDoList.push(task)
    },

    onRemoveTask(index){
      this.needDoList.splice(index, 1)
    },

  }
  
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Chivo+Mono&display=swap');

body{
  font-family: 'Chivo Mono', monospace;
  font-weight: 400;
}

.header{
  background-color:#333;
  padding:10px 0;
  margin-bottom: 40px;
}

.container{
  width: 800px;
  margin: 0 auto;
  padding: 0 15px;
}

</style>
