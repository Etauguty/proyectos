<template>
  <div id="app" class="container">
    <h2 style="text-align:left">LKMX - Front-end</h2>
    <TodoList />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList
  }
}
</script>

<style>

.container{
  max-width: 600px;
  max-height: 600px;
  margin: 0 auto;
  background-color: #E7E7E7;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 50px;
  font-size: 24px;
}
</style>
