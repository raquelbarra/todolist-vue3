<script>
let id = 0;

export default {
  data() {
    return {
      newTodo: '',
      hideCompleted: false,
      todos: [
        {id: id++, text: 'Aprender HTML'},
        {id: id++, text: 'Aprender CSS'},
        {id: id++, text: 'Aprender Javascript'},
        {id: id++, text: 'Aprender VUE3'},
      ]
    }
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted ? this.todos.filter((t) => !t.done) : this.todos
    }
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo, done: false })
      this.newTodo = ''
    },
    removeTodo(todo){
      this.todos = this.todos.filter((t)=> t !== todo)
    }
  }
}

</script>

<template>
  <div class="formTodo">
    <h1> Lista de tarefas </h1>
    <form
      @submit.prevent="addTodo"
    >
      <input v-model="newTodo">
      <button class="btn btn-submit">
        Adicionar Tarefa
      </button>
    </form>
    <ul class="list">
      <li
        v-for="todo in filteredTodos"
        :key="todo.id"
      >
        <input
          v-model="todo.done"
          type="checkbox"
        >
        <span :class="{done: todo.done}">{{ todo.text }}</span>
        <button
          class="btn-check"
          @click="removeTodo(todo)"
        >
          X
        </button>
      </li>
    </ul>
    <button
      class="btn btn-hide"
      @click="hideCompleted = !hideCompleted"
    >
      {{ hideCompleted ? 'Mostrar tudo' : 'Ocultar tarefas finalizadas' }}
    </button>
  </div>
</template>

<style>
  .done {
    text-decoration: line-through;
  }
  .formTodo {
    padding: 50px;
    background-color: #263238;
    color: white;
    border-radius: 5px;
    text-align: center;
  }
  .list {
    text-align: left;
  }

  ul {
    margin:0;
    padding: 0;
  }

  li {
    list-style: none;
    margin-top: 10px;
  }

  .btn {
    padding: 10px;
    margin: 2px;
    cursor: pointer;
  }

  .btn-hide {
    margin-top: 20px;
    background-color: #d1949e;  
    border-color: #d48995;
    border-radius: 5px;
    color: whitesmoke;
  }

  .btn-hide:hover{
    background-color: #d67a89;
  }

  .btn-submit {
    background-color: #aac84e;
    border-color: #acc955;
    border-radius: 5px;
  }

  .btn-submit:hover{
    background-color: #b3e51b;
  }

  .btn-check{
    margin-left: 10px;
    cursor: pointer;
    background-color: #a376ef;
    border: 0;
    border-radius: 3px;
  }

  .btn-check:hover{
    background-color: #73359f;
    color: white;
  }


  input{
    padding: 10px;
  }
</style>
