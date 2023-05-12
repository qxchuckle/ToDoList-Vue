<template>
  <div class="todo-list">
    <ul>
      <transition-group name="todo">
        <ListItem v-for="item in todos" :key="item.id" :todo="item"></ListItem>
      </transition-group>
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
  props: ["todos"],
  methods: {},
};
</script>

<style lang="less" scoped>
@todo-border: 1px solid #ccc;
@todo-border-radius: 6px;

.todo-list {
  margin-bottom: 15px;
  border-radius: @todo-border-radius;
  border: @todo-border;
  overflow: hidden;
}

/* 动画 */
.todo-enter,
.todo-leave-to {
  opacity: 0;
  transform: translateX(-50%);
}

.todo-enter-to,
.todo-leave {
  opacity: 1;
  transform: translateX(0);
}
.todo-enter-active, .todo-leave-active {
    transition: all 0.3s;
}
</style>
