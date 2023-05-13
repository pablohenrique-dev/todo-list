<template>
  <main>
    <h1>TODOLIST</h1>
    <ToDoList />
    <span class="direitos">© 2023 - Todos os direitos reservados</span>
  </main>
</template>

<script>
import ToDoList from "./components/ToDoList.vue";

export default {
  name: "App",
  components: {
    ToDoList,
  },
};
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
  color: #687078;
  position: absolute;
  bottom: 25px;
  left: 0;
  right: 0;
}
</style>
