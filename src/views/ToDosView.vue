<script setup>
import { ref } from "vue";
import ToDoCreator from "../components/ToDoCreator.vue";
import { uid } from 'uid';
import ToDoItem from "../components/ToDoItem.vue";
import { Icon } from '@iconify/vue';

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

const toggleToDoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
}

const toggleEditToDo = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
}

const updateToDo = (todoVal, todoPos) => {
  todoList.value[todoPos].todo = todoVal;
}

const deleteToDo = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
} 

</script>

<template>
  <main> 
    <h1>Create To Do</h1>
    <ToDoCreator @create-to-do="createToDo"/>
    <ul class="todo-list" v-if="todoList.length > 0">
      <ToDoItem v-for="(todo, index) in todoList" :todo="todo" :index="index" 
        @toggle-complete="toggleToDoComplete"
        @edit-todo="toggleEditToDo"
        @update-todo="updateToDo"
        @delete-todo="deleteToDo"
      />
    </ul>
    <p class="todos-msg" v-else>
      <Icon icon="noto-v1:sad-but-relieved-face" color="#531" />
      <span>You don't have to do's !</span>
    </p>
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

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>
