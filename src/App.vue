<script>

  export default {
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(i) {
      this.todos.splice(i,1)
    },
    addTodo() {
      const input = document.querySelector('.addTodoInput')
      this.todos.push({
        name: input.value,
        done: false
      })
      input.value = ''
    },
    markDone(i) {
      this.todos[i].done = true
    },
    clearDone() {
      let result = this.todos.filter(todo => todo.done == false)
      this.todos = result
    },
    editTodo(i) {
      const input = document.querySelector('.addTodoInput')
      const addBtn = document.querySelector('.addBtn')
      const editBtn = document.querySelector('.editBtn')

      input.placeholder = this.todos[i].name
      addBtn.classList.add('btn-disabled')
      editBtn.classList.remove('btn-disabled')
      editBtn.id = i
    },
    finishEdit() {
      const input = document.querySelector('.addTodoInput')
      const addBtn = document.querySelector('.addBtn')
      const editBtn = document.querySelector('.editBtn')
      this.todos.splice(editBtn.id, 1, {
        name: input.value,
        done: false
      })
      input.value = ''
      input.placeholder = 'New todo'
      addBtn.classList.remove('btn-disabled')
      editBtn.classList.add('btn-disabled')
    }
  }
}
</script>

<template>
  <div class="hero min-h-screen">
  <div class="hero-content card w-96 bg-base-100 shadow-xl">
    <div class="card-body items-center text-center">
      <h2 class="card-title">TodoList</h2>
      <input type="text" placeholder="New todo" class="addTodoInput input input-bordered w-full max-w-xs" />
      <button @click="addTodo" class="addBtn btn btn-primary">Add</button>
      <button @click="finishEdit" class="editBtn btn btn-primary btn-disabled">Finish Edit</button>
      <div v-for="(todo, index) in todos" :key="index">
        <div>
          <h1 :class="{ done: todo.done }" @click="markDone(index)">{{ todo.name }}</h1>
          <button @click="editTodo(index)" class="p-2 btn btn-primary">Edit</button>
          <button @click="deleteTodo(index)" class="p-2 m-2 btn btn-primary">Delete</button>
        </div>
      </div> 
      <div class="card-actions">
        <button @click="clearDone" class="btn btn-primary">Clear Done</button>
      </div>
    </div>
  </div>
  </div>
</template>

<style>
  .done {
    text-decoration: line-through;
  }
</style>