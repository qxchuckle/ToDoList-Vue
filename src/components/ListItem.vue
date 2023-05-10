<template>
    <li>
        <label>
            <input type="checkbox">
            <span>这是一个ToDo</span>
        </label>
        <button class="list-item-btn">删除</button>
    </li>
</template>

<script>
export default {
    name: 'ListItem',
}
</script>

<style lang="less" scoped>
@todo-border: 1px solid #ccc;
@todo-border-radius: 6px;

li {
    border-bottom: @todo-border;
    display: flex;
    height: 38px;
    line-height: 37px;
    justify-content: space-between;

    &:last-child{
        border-bottom: none;
    }

    label {
        margin-left: 10px;

        input {
            top: -1px;
            position: relative;
            vertical-align: middle;
            margin-right: 10px;
        }
    }

    button {
        border-radius: @todo-border-radius;
        border: @todo-border;
        font-size: 14px;
        margin: 5px;
        padding: 0 5px;
        background: #dc7878;
        color: #fff;
    }
}
</style>