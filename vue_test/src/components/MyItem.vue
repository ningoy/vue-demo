<template>
  <div v-if="!todo.status">
    <li>
      <label>
        <input type="checkbox" :checked="todo.done" @change="checkItem(todo.id)">
        <span v-show="!todo.isEdit">{{ todo.title }}</span>
        <input v-show="todo.isEdit" type="text" v-model="editingTitle" @blur="finishEdit(todo)" ref="inputTitle">
      </label>
      <button class="delete" @click="deleteItem(todo.id)">删除</button>
      <button v-show="!todo.isEdit" class="edit" @click="editItem(todo)">编辑</button>
    </li>
  </div>
</template>

<script>
export default {
  name: "MyItem",
  props: ["todo", "check", "del"],
  data() {
    return {
      editing: false,
      editingTitle: ''
    }
  },
  methods: {
    checkItem(id) {
      this.check(id)
    },
    deleteItem(id) {
      if (confirm('确定删除吗?')) {
        this.del(id)
      }
    },
    editItem(todo) {
      this.editingTitle = todo.title
      this.$set(todo, 'isEdit', true)
      this.$nextTick(function () {
        this.$refs.inputTitle.focus()
      })
    },
    finishEdit(todo) {
      this.$bus.$emit('editTodo', todo.id, this.editingTitle)
      todo.isEdit = false
    }
  }
}
</script>

<style>
li:hover {
  background-color: #8c939d;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li button.delete {
  background-color: #dd6161;
}

li button.edit {
  background-color: #1f97a7;
}

li:hover button {
  display: block;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}
</style>
