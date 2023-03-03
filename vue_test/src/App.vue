<template>
  <div>
    <MyHeader :add="add"></MyHeader>
    <MyList :todos="todos" :check="check" :del="del"></MyList>
    <MyFooter :doneItemCount="doneItemCount" :allItemCount="allItemCount" :clear="clear"
              :checkAll="checkAll"></MyFooter>
  </div>
</template>
<script>
import MyHeader from "./components/MyHeader";
import MyList from "./components/MyList";
import MyFooter from "./components/MyFooter";
import {nanoid} from 'nanoid'


export default {
  name: 'App',
  components: {
    MyHeader,
    MyList,
    MyFooter
  },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || []
    }
  },
  methods: {
    add(title) {
      if (title !== "") {
        const todo = {
          id: nanoid(), title: title, done: false, status: 0
        }
        this.todos.unshift(todo)
      }
    },
    check(id) {
      this.todos.forEach(todo => {
        if (todo.id === id) {
          todo.done = !todo.done
        }
      })
    },
    del(id) {
      this.todos.forEach(todo => {
        if (todo.id === id) {
          todo.status = 1
        }
      })
    },
    clear() {
      this.todos.forEach(todo => {
        if (todo.done) {
          todo.status = 1
        }
      })
    },
    checkAll(value) {
      this.todos.forEach(todo => {
        if (todo.status === 0) {
          todo.done = value
        }
      })
    }
  },
  computed: {
    doneItemCount: function () {
      return this.todos.filter(todo => {
        return todo.status === 0
      }).filter(todo => {
        return todo.done
      }).length
    },
    allItemCount: function () {
      return this.todos.filter(todo => {
        return todo.status === 0
      }).length
    }
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem("todos", JSON.stringify(value))
      }
    }
  },
  mounted() {
    this.$bus.$on('editTodo', (id, newTitle) => {
      this.todos.forEach(todo => {
        if (todo.id === id) {
          todo.title = newTitle
        }
      })
    })
  },
  beforeDestroy() {
    this.$bus.$off('editTodo')
  }
}
</script>
<style>
div {
  width: 500px;
}
</style>
