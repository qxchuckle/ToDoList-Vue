<template>
  <div class="todo-list">
    <ul>
      <ListItem v-for="item in todos" :key="item.id" :todo="item" @receiveId="receiveId" @deleteToDo="deleteToDo">
      </ListItem>
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
  props: ['todos'],
  methods: {
    receiveId(id) {
      this.$emit('updateComplete', id)
    },
    deleteToDo(id) {
      this.$emit('deleteToDo', id)
    }
  }
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
