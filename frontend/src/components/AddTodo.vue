<template>
  <div id="app">
    <h1>Formulário Simples</h1>
    <form @submit.prevent="handleSubmit">
      <input 
        v-model="inputText" 
        type="text" 
        placeholder="Digite algo..." 
        required
      />
      <button type="submit">Enviar</button>
    </form>

    <ul>
      <li v-for="todo in todosArray" :key="todo.id">
        {{ todo.description }}
        <button type="submit" @click="handleDeleteTodo(todo.id)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { createClient } from '@supabase/supabase-js'

const supabaseUrl = 'https://fnzqgervsfmcxdohsvxj.supabase.co'
const supabaseKey = process.env.VUE_APP_SUPABASE_KEY
const supabase = createClient(supabaseUrl, supabaseKey)

export default {
  name: 'AddTodo',
  data() {
    return {
      inputText: '',
      todosArray: [],
    };
  },
  methods: {
    async handleSubmit() {
      await supabase
      .from('Todos')
      .insert([{ description: this.inputText }])

      this.inputText = '';

      await this.getAllTodos()
    },
    async getAllTodos() {
      let { data: Todos } = await supabase
        .from('Todos')
        .select('*')

      this.todosArray = Todos
    },
    async handleDeleteTodo(todoId) {
      await supabase
      .from('Todos')
      .delete()
      .eq('id', todoId)

      await this.getAllTodos()
    },
  },
  async mounted() {
    await this.getAllTodos()
  },
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
form {
  margin: 20px;
}
input {
  padding: 10px;
  font-size: 16px;
}
button {
  padding: 10px 20px;
  font-size: 16px;
  margin-left: 10px;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  padding: 10px 0;
  font-size: 18px;
}
</style>
