<template>
    <div class="todo-header">
        <input type="text" placeholder="回车新增ToDo" />
        <button>新增</button>
    </div>
</template>

<script>
export default {
    name: "ToDoHeader",
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
