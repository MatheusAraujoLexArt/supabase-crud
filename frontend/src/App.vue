<template>
  <div>
    <AddTodoVue />
  </div>
</template>

<script>
import AddTodoVue from './components/AddTodo.vue';

export default {
  name: 'App',
  data() {
    return {
      todosArray: [],
    };
  },
  components: {
    AddTodoVue,
  },
  methods: {
  }
}
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
</style>
