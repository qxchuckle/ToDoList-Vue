<template>
    <div id="todo-footer">
        <div v-show="this.todos.length">
            <input type="checkbox" v-model="checkValue">
            <div class="statistics">已完成{{ doneToDo }} / 全部{{ todos.length }}</div>
            <button @click="deleteComplete">清除已完成</button>
        </div>
        <div class="tip" v-show="!this.todos.length">没有ToDo</div>
    </div>
</template>

<script>
export default {
    name: 'ToDoFooter',
    props: ['todos'],
    computed: {
        // 计算已完成数量
        doneToDo() {
            // 通过reduce统计已完成
            return this.todos.reduce((pre, item) => {
                return pre + (item.complete ? 1 : 0)
            }, 0)
        },
        // 全选按钮的状态
        checkValue: {
            // checkValue无论是设置还是确定值，都要通过数据驱动，遍历所有数据来确定todo是否全部完成
            get() {
                // 比较已完成数量和全部todo数量，且todo至少要有一个才打勾
                return this.doneToDo === this.todos.length && this.todos.length > 0;
            },
            // 将changeAll()移到此处，点击checkbox后通过changeAll()修改数据后，自动触发计算属性的getter并更新视图
            set() {
                this.changeAll()
                return
            }
        }
    },
    methods: {
        // 全选或全不选，即全都变为目前全选按钮状态的反状态
        changeAll() {
            // 因为现在checkValue是计算属性，checkbox点击变化后的未来值要通过“非”体现
            // 数据变化，checkValue计算属性也自动触发getter更新视图，v-model更新checked
            this.$emit('changeAll', !this.checkValue)
        },
        // 删除所有已完成项
        deleteComplete() {
            this.$emit('deleteComplete')
        }
    }
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

    .tip {
        margin: 0 auto;
        width: fit-content;
        font-size: 30px;
        opacity: 0.9;
        color: #ccc;
    }
}
</style>