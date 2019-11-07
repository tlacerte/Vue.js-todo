<template>
    <div>
        <input type="text" 
        class="todo-input" 
        placeholder="what needs to be done"
        v-model="newTodo">
        <div v-for="todo in todos" :key="todo.id" class="todo-item">
            {{ todo.title }}
        </div>
    </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      newTodo: '',
      todos: [
        {
            'id': 1,
            'title': 'Sample todo 1',
            'completed': false,
        },
        {
            'id': 2,
            'title': 'Sample todo 2',
            'completed': false,
        },
      ]
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