<template>
  <div id="app">
    <todo-list />
  </div>
</template>

<script>
import TodoList from "./components/TodoList";
export default {
  name: "app",
  components: { TodoList },
};
</script>

<style>
#app {
  font-family: "Roboto", sans-serif;
  font-weight: 600;
  font-size: 20px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 500px;
  margin: 0 auto;
}
</style>
