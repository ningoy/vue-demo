<template>
  <div>
    <ul>
      <MyItem v-for="todo in todos" :key="todo.id" :todo="todo" :check="check" :del="del"></MyItem>
    </ul>
  </div>
</template>

<script>
import MyItem from "@/components/MyItem";

export default {
  name: "MyList",
  components: {
    MyItem
  },
  props: ["todos", "check", "del"],
  methods: {}
}
</script>

<style>

</style>
