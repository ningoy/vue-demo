<template>
  <div>
    <label>
      <input type="checkbox" v-model="myFooterCheckbox">
    </label>
    <span>
      <span>已完成{{ doneItemCount }}</span> / <span>全部{{ allItemCount }}</span>
    </span>
    <button @click="clearDoneItem">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  props: ["doneItemCount", "allItemCount", "clear", "checkAll"],
  methods: {
    clearDoneItem() {
      this.clear()
    }
  },
  computed: {
    myFooterCheckbox: {
      get() {
        return this.allItemCount > 0 && this.allItemCount === this.doneItemCount;
      },
      set(value) {
        this.checkAll(value)
      }
    }
  }
}
</script>

<style>

</style>
