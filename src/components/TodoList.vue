<template>
    <div>
        <input type="text" 
        class="todo-input" 
        placeholder="what needs to be done"
        v-model="newTodo"
        @keyup.enter="addTodo">
        
        <div v-for="(todo, index) in todos" 
        :key="todo.id" 
        class="todo-item">
            <div class="todo-item-left">
                <input type="checkbox" v-model="todo.completed">
                <div v-if="!todo.editing"
                    @dblclick="editTodo(todo)" 
                    class="todo-item-label"
                    :class="{ completed : todo.completed }">
                    {{ todo.title }}
                </div>
                <input v-else class="todo-item-edit" 
                    type="text" 
                    v-model="todo.title"
                    @blur="doneEdit(todo)"
                    @keyup.enter="doneEdit(todo)"
                    @keyup.esc="cancelEdit(todo)"
                    v-focus>
            </div>
            <div class="remove-item" @click="removeTodo(index)">
                &times;
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      newTodo: '',
      idForTodo: 3,
      beforeEditCache: '',
      todos: [
        {
            'id': 1,
            'title': 'Sample todo 1',
            'completed': false,
            'editing': false,
        },
        {
            'id': 2,
            'title': 'Sample todo 2',
            'completed': false,
            'editing': false,
        },
      ]
    }
  },
  directives: {
      focus: {
          inserted: function(el) {
              el.focus()
          }
      }
  },
  methods: {
    addTodo() {
        if (this.newTodo.trim().length == 0) {
            return
        }

        this.todos.push({
            id: this.idForTodo,
            title: this.newTodo,
            completed: false,
            editing: false,
        })

        this.newTodo = ''
        this.idForTodo++
    },
    removeTodo(index) {
        this.todos.splice(index, 1)
    },
    editTodo(todo) {
        this.beforeEditCache = todo.title
        todo.editing = true
    },
    doneEdit(todo) {
        if (todo.title.trim() == '') {
            todo.title = this.beforeEditCache
        }

        todo.editing = false
    },
    cancelEdit(todo) {
        todo.title = this.beforeEditCache
        todo.editing = false
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

    .todo-input:focus {
        outline: black;
    }

    .todo-item {
        margin-bottom: 12px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .remove-item {
        cursor: pointer;
        margin-left: 14px;
    }

    .remove-item:hover {
        color: black;
    }

    .todo-item-left {
        display: flex;
        align-items: center;
    }

    .todo-item-label {
        padding: 10px;
        border: 1px solid white;
        margin-left: 12px;
    }

    .todo-item-edit {
        font-size: 24px;
        color: #2c3e50;
        margin-left: 12px;
        width: 100%;
        padding: 10px;
        border: 1px solid #ccc;
        font-family: 'Avenir', sans-serif;
    }

    .todo-item-edit:focus {
        outline: none;
    }

    .completed {
        text-decoration: line-through;
        color: gray;
    }
</style>