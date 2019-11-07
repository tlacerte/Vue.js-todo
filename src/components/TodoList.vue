<template>
    <div>
        <input type="text" 
        class="todo-input" 
        placeholder="what needs to be done"
        v-model="newTodo">
        Todo list goes here
    </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style>
    .todo-input {
        width: 100%;
        padding: 10px 18px;
        font-size: 18px;
        margin-bottom: 16px;
    }
</style>