<template>
  <div id="app">
    <div id="todo-container">
      <div id="todo-wrap">
        <ToDoHeader @receive="receive"></ToDoHeader>
        <ToDoList :todos="todos"></ToDoList>
        <ToDoFooter :todos="todos" @changeAll="changeAll" @deleteComplete="deleteComplete"></ToDoFooter>
      </div>
    </div>
  </div>
</template>

<script>
import pubsub from "pubsub-js";

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
  data() {
    return {
      // 初始化todos，本地存储有则拿，没有则赋值空数组
      todos: JSON.parse(localStorage.getItem("todos")) || [],
    }
  },
  methods: {
    receive(todo) {
      this.todos.unshift(todo);
    },
    updateComplete(id) {
      // 遍历找到对应的todo
      this.todos.forEach((item) => {
        if (item.id === id) {
          // complete取反
          item.complete = !item.complete;
        }
      });
    },
    deleteToDo(id) {
      this.todos.forEach((item, index, arr) => {
        if (item.id === id) {
          arr.splice(index, 1)
        }
      });
    },
    // 全选或全不选，即全都变为目前全选按钮状态的反状态
    changeAll(checkValue) {
      this.todos.forEach((item) => {
        if (item.complete !== checkValue) {
          item.complete = checkValue;
        }
      });
    },
    // 删除所有已完成项
    deleteComplete() {
      this.todos = this.todos.filter((item) => {
        return !item.complete;
      });
    },
    // 修改todo的title
    editToDo(id,value){
      this.todos.forEach((item, index, arr) => {
        if (item.id === id) {
          arr[index].title = value;
        }
      });
    }
  },
  watch: {
    // 监视todos发生的变化
    todos: {
      // 数据多层开启深度监视
      deep: true,
      handler(value) {
        // 只要数据发生改变就更新本地存储的数据
        localStorage.setItem("todos", JSON.stringify(value));
      }
    }
  },
  mounted(){
    this.$bus.$on('updateComplete', this.updateComplete)
    // this.$bus.$on('deleteToDo', this.deleteToDo)

    // 订阅消息
    pubsub.subscribe('deleteToDo', (magName, data)=>{
      magName; // eslint不允许不使用参数，这里使用一下
      // 将接收到的数据（要删除的id）传给删除函数
      this.deleteToDo(data)
    })
    // 订阅修改todo的消息
    pubsub.subscribe('editToDo', (magName,arr)=>{
      magName;
      this.editToDo(arr[0],arr[1])
    })
  }
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
