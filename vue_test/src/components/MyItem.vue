<template>
  <div v-if="!todo.status">
    <li>
      <label>
        <input type="checkbox" :checked="todo.done" @change="checkItem(todo.id)">
        <span>{{ todo.title }}</span>
      </label>
      <button @click="deleteItem(todo.id)">删除</button>
    </li>
  </div>
</template>

<script>
export default {
  name: "MyItem",
  props: ["todo", "check", "del"],
  methods: {
    checkItem(id) {
      this.check(id)
    },
    deleteItem(id) {
      if (confirm('确定删除吗?')) {
        this.del(id)
      }
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
  background-color: #dd6161;
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
