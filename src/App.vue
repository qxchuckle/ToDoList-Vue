<template>
  <div id="app">
    <div id="todo-container">
      <div id="todo-wrap">
        <ToDoHeader></ToDoHeader>
        <ToDoList></ToDoList>
        <ToDoFooter></ToDoFooter>
      </div>
    </div>
  </div>
</template>

<script>
import ToDoHeader from "./components/ToDoHeader.vue";
import ToDoList from "./components/ToDoList.vue";
import ToDoFooter from "./components/ToDoFooter.vue";

export default {
  name: "App",
  components: {
    ToDoHeader,
    ToDoList,
    ToDoFooter,
  },
};
</script>

<style lang="less">
@todo-border: 1px solid #ccc;
@todo-border-radius: 6px;

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

ul {
  list-style: none;
}

#app {
  margin: 20px 10px;
  font-size: 16px;
}

#todo-container {
  max-width: 600px;
  min-width: 300px;
  height: auto;
  margin: 0 auto;
  padding: 10px;
  border: @todo-border;
  border-radius: @todo-border-radius;

  #todo-wrap {
    width: 100%;
  }

}
</style>
