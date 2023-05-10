<template>
    <div id="todo-footer">
        <input type="checkbox">
        <div class="statistics">已完成0 / 全部4</div>
        <button>清除已完成</button>
    </div>
</template>

<script>
export default {
    name: 'ToDoFooter',
}
</script>

<style lang="less" scoped>
@todo-border: 1px solid #ccc;
@todo-border-radius: 6px;

#todo-footer {
    width: 100%;
    height: 40px;
    line-height: 40px;
    padding-left: 10px;

    input {
        top: 1px;
        position: relative;
    }

    .statistics {
        width: fit-content;
        display: inline-block;
        margin-left: 20px;
    }

    button {
        float: right;
        padding: 5px 10px;
        margin: 5px 0;
        border-radius: @todo-border-radius;
        border: @todo-border;
        color: #fff;
        background: rgb(220, 120, 120);
        font-size: 15px;
    }
}
</style>