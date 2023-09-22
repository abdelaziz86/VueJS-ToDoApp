<script setup>
import ToDoCreator from "../components/ToDoCreator.vue";
</script>

<template>
  <main> 
    <h1>Create To Do</h1>
    <ToDoCreator/>
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
