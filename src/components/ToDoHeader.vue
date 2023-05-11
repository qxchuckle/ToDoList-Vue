<template>
    <div class="todo-header">
        <input type="text" placeholder="回车新增ToDo" @keyup.enter="addToDo" />
        <button @click="addToDo">新增</button>
    </div>
</template>

<script>
import { nanoid } from "nanoid";
export default {
    name: "ToDoHeader",
    props: ['receive'],
    methods: {
        addToDo(e) {
            // 获取input框元素
            let input = e.target.tagName === "INPUT" ? e.target : e.target.parentNode.firstElementChild
            // 输入框为空或只有空格就返回
            if (input.value.trim() === "") {
                input.value = "";
                return
            }
            // 生成数据对象
            let todo = {
                // 正常来说数据由后端返回，id由数据库维护，这里使用nanoid生成唯一id
                id: nanoid(),
                title: input.value,
                complete: false
            }
            // 清空input
            input.value = "";
            // 将用户输入通过接收到函数传给父组件
            // this.receive(todo);
            this.$emit('receive', todo)
        }
    }
};
</script>

<style lang="less" scoped>
@todo-border: 1px solid #ccc;
@todo-border-radius: 6px;

.input-focus {
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
        0 0 8px rgba(82, 168, 236, 0.6);
    border-color: rgba(82, 168, 236, 0.8);
    outline: none;
}

.todo-header {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    margin-bottom: 15px;

    input {
        width: 100%;
        font-size: 16px;
        padding: 8px 10px;
        border: @todo-border;
        border-radius: @todo-border-radius;

        &:focus {
            .input-focus();
        }
    }

    button {
        margin-left: 10px;
        width: 65px;
        border-radius: @todo-border-radius;
        border: @todo-border;
        background: rgb(52, 201, 238);
        font-size: 16px;
        color: #fff;
    }

}
</style>
