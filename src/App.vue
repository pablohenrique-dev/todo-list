<template>
  <main>
    <h1>TODOLIST V1.0</h1>
    <!-- <ToDoList /> -->
    <ToDoListCopy />
    <span class="direitos">© 2023 - Todos os direitos reservados</span>
  </main>
</template>

<script setup>
// import ToDoList from "./components/ToDoList.vue";
import ToDoListCopy from "./components/ToDoListCopy.vue";

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  list-style: none;
  text-decoration: none;
}

h1 {
  margin-bottom: 40px;
}

.direitos {
  display: block;
  margin-top: 24px;
  margin-bottom: 24px;
  color: #687078;
  
}
</style>
