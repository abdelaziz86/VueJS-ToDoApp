<script setup>
import { ref } from "vue";
import ToDoCreator from "../components/ToDoCreator.vue";
import {uid} from 'uid';
const todoList = ref([]); 

const createToDo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: false,
    isEditing : false  
  });

  console.log(todoList.value);
}
</script>

<template>
  <main> 
    <h1>Create To Do</h1>
    <ToDoCreator @create-to-do="createToDo"/>
  </main>
</template>

<style lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
}
</style>
