<template>
    <li>
        <label>
            <input type="checkbox" :checked="todo.complete" @change="changeComplete(todo.id)">
            <span>{{ todo.title }}</span>
        </label>
        <button class="list-item-btn" @click="deleteToDo(todo.id)">删除</button>
    </li>
</template>

<script>
export default {
    name: 'ListItem',
    props: ['todo'],
    methods: {
        changeComplete(id) {
            // 由于ListItem是App的孙子，所以要先通过$emit()将数据传给父组件，再由父组件传给爷爷组件
            this.$emit('receiveId', id)
        },
        deleteToDo(id) {
            if (!confirm('确认删除吗?')) {
                return
            }
            this.$emit('deleteToDo', id)
        }
    }
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

    &:last-child {
        border-bottom: none;
    }

    &:hover {
        background: rgb(240, 240, 240);

        button {
            display: block;
        }
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
        display: none;
    }
}
</style>