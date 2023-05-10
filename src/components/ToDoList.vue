<template>
  <div class="todo-list">
    <ul>
      <ListItem></ListItem>
      <ListItem></ListItem>
      <ListItem></ListItem>
      <ListItem></ListItem>
    </ul>
  </div>
</template>

<script>
import ListItem from "./ListItem.vue";
export default {
  name: "ToDoList",
  components: {
    ListItem,
  },
};
</script>

<style lang="less" scoped>
@todo-border: 1px solid #ccc;
@todo-border-radius: 6px;

.todo-list {
  margin-bottom: 15px;
  border-radius: @todo-border-radius;
  border: @todo-border;
}
</style>
