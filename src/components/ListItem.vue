<template>
    <li>
        <label>
            <input v-show="!isEdit" type="checkbox" :checked="todo.complete" @change="changeComplete(todo.id)">
            <span v-show="!isEdit" ref="titleToDo">{{ todo.title }}</span>
            <input v-show="isEdit" class="todo-title-input" type="text" :value="todo.title" ref="titleInput"
                @blur="editToDo(todo.id)" contenteditable="true">
        </label>
        <div class="btn-box">
            <button v-show="isEdit" class="list-item-btn" @click="editToDo(todo.id)">保存</button>
            <button v-show="isEdit" class="list-item-btn" @click="completeEdit()">取消</button>
            <button v-show="!isEdit" class="list-item-btn" @click="edit()">编辑</button>
            <button class="btn-delete" @click="deleteToDo(todo.id)">删除</button>
        </div>
    </li>
</template>

<script>
import pubsub from "pubsub-js";
export default {
    name: 'ListItem',
    props: ['todo'],
    data() {
        return {
            // 是否在修改，控制输入框显隐
            isEdit: false,
        }
    },
    methods: {
        changeComplete(id) {
            // 触发事件传入id
            this.$bus.$emit('updateComplete', id)
        },
        deleteToDo(id) {
            if (!confirm('确认删除吗?')) {
                return
            }
            // 触发事件传入id
            // this.$bus.$emit('deleteToDo', id)
            // 发布消息
            pubsub.publish('deleteToDo', id);
        },
        // 进行修改
        edit() {
            this.isEdit = true;
            // $nextTick的回调函数会在dom节点更新之后再执行
            this.$nextTick(()=>{
                // 让输入框获取焦点
                this.$refs.titleInput.focus();
            });
        },
        // 完成修改（取消也是完成）
        completeEdit() {
            this.isEdit = false;
            this.ifEdit = false;
        },
        // 修改todo并发生消息
        editToDo(id) {
            this.completeEdit()
            // 获取input框元素
            let input = this.$refs.titleInput;
            // 如果输入框内容没有变则返回
            if (input.value === this.todo.title) return;
            // 如果输入框内容为空提示为空并返回
            if (input.value.trim() === "") {
                alert('ToDo内容为空！请重新修改')
                return;
            }
            pubsub.publish('editToDo', [id, input.value]);
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
    height: auto;
    line-height: 1;
    justify-content: space-between;

    &:last-child {
        border-bottom: none;
    }

    &:hover {
        background: rgb(240, 240, 240);

        .btn-box {
            display: flex;
        }
    }

    label {
        margin-left: 6px;
        display: flex;
        white-space: normal;
        word-break: break-all;
        word-wrap: break-word;
        text-overflow: ellipsis;
        padding: 10px;
        flex: 1;

        input {
            top: -1px;
            position: relative;
            vertical-align: middle;
            margin-right: 10px;
            outline: none;
        }

        .todo-title-input {
            border-radius: @todo-border-radius;
            border: @todo-border;
            font-size: 16px;
            padding: 3px 6px;
            margin-right: 0px;
            width: 100%;

            &:focus {
                box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
                    0 0 8px rgba(82, 168, 236, 0.6);
                border-color: rgba(82, 168, 236, 0.8);
                outline: none;
            }
        }
    }

    button {
        border-radius: @todo-border-radius;
        border: @todo-border;
        font-size: 14px;
        margin: 5px;
        padding: 4px 5px;
        color: #fff;
    }

    .btn-box {
        display: none;
        min-width: fit-content;
        display: flex;
        flex-direction: row;
        align-items: center;

        .list-item-btn {
            background: rgb(78, 205, 183);
        }

        .btn-delete {
            background: #dc7878;
        }
    }
}
</style>