<template>
  <div v-if="!todo.status">
    <li>
      <label>
        <input type="checkbox" :checked="todo.done" @change="checkItem(todo.id)">
        <span v-show="!todo.isEdit">{{ todo.title }}</span>
        <input v-show="todo.isEdit" type="text" :value="todo.title" @blur="finishEdit(todo)">
      </label>
      <button class="delete" @click="deleteItem(todo.id)">删除</button>
      <button class="edit" @click="editItem(todo)">编辑</button>
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
      this.$set(todo, 'isEdit', true)
    },
    finishEdit(todo) {
      console.log("11")
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
