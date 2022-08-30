<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" @keyup.enter="addItem(title)" v-model="title">
  </div>
</template>

<script>
export default {
  name: "MyHeader",
  data() {
    return {
      title: ""
    }
  },
  props: ["add"],
  methods: {
    addItem(title) {
      if (title !== "") {
        this.add(title)
        this.title = ""
      }
    }
  }
}
</script>

<style>
.todo-header input {
  width: 560px;
  height: 28px;
}
</style>
