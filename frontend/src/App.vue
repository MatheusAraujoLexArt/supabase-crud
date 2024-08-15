<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <AddTodoVue />
</template>

<script>
  import { createClient } from '@supabase/supabase-js'
  const supabaseUrl = 'https://fnzqgervsfmcxdohsvxj.supabase.co'
  const supabaseKey = process.env.VUE_APP_SUPABASE_KEY;
  export const supabase = createClient(supabaseUrl, supabaseKey)

  import AddTodoVue from './components/AddTodo.vue';

  const fetchTodos = async () => {
    let { data: Todos } = await supabase
      .from('Todos')
      .select('*')

      console.log(Todos)
  }

  const mounted = () => {
    fetchTodos();
  }

export default {
  name: 'App',
  components: {
    AddTodoVue,
  },
  mounted,
  methods: {
    fetchTodos,
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
