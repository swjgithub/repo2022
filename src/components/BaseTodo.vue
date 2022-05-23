<template>
    <header>
        <section>
            <h1>ToDoList</h1>
            <form action="#" @submit.prevent>
                <input v-model="newTodo" @keyup.enter="addData" type="text" autocomplete="off" placeholder="添加ToDo">
            </form>
        </section>
    </header>
    <section>
        <h2>{{ title[0] }} <span>{{ unCompleted.length }}</span></h2>
        <ol>
            <li v-for="item in unCompleted" :key="item.id">
                <input type="checkbox" @click="changeState(item)"> {{ item.title }} <span
                    @click="removeData(item.id)">&minus;</span>
            </li>
        </ol>
        <h2>{{ title[1] }} <span>{{ completed.length }}</span></h2>
        <ul> 
            <li :class="{ 'gray': true }" v-for="item in completed" :key="item.id">
                <input type="checkbox" @click="changeState(item)" checked> {{ item.title }} <span
                    @click="removeData(item.id)">&minus;</span>
            </li>
        </ul>
    </section>
</template>

<script>
import { reactive, ref, computed, watch, watchEffect } from 'vue'
export default {
    setup() {
        //描述数据
        const title = ["正在进行", "已经完成"];
        let state;
        // state = [{ id: 1, title: 453254423, completed: false }]
        if (localStorage.getItem("todos")) {
            state = JSON.parse(localStorage.getItem("todos"));
        } else {
            state = [];
        }
        const todos = reactive(state);

        watch(todos, (newValue, oldValue) => {
            // console.log('watch 已触发', newValue);
            localStorage.setItem('todos', JSON.stringify(newValue))
        });

        //添加数据
        let newTodo = ref("");
        let nextId = 1;
        function addData() {
            //关键点：正确的获取id
            nextId = Math.max(...todos.map(function (item) {
                return item.id;
            })) + 1;
            //添加newTodo
            todos.push({ id: nextId, title: newTodo.value, completed: false });
            newTodo.value = "";
            // localStorage.setItem("todos", JSON.stringify(todos));
        }
        // 改变待办事项的状态
        function changeState(item) {
            item.completed = !item.completed;
            // localStorage.setItem("todos", JSON.stringify(todos));
        }

        //删除数据
        let index = 0;
        function removeData(id) {
            //关键点：正确的获取数组下标index
            index = todos.findIndex((item) => item.id === id);
            todos.splice(index, 1);
            // localStorage.setItem("todos", JSON.stringify(todos));
        }

        //处理（计算）数据
        let unCompleted = [];
        let completed = []
        unCompleted = computed(function () {
            return todos.filter(item => item.completed === false);
        });
        completed = computed(() => todos.filter(item => item.completed === true));


        //返回数据
        return { changeState, removeData, title, todos, newTodo, addData, unCompleted, completed }
    }
}
</script>

<style scoped>
header {
    height: 50px;
    background: rgba(47, 47, 47, 0.98);
}

header>section {
    display: flex;
    flex-flow: row nowrap;
    justify-content: space-between;
    align-items: center;
    height: 50px;
}

header h1 {
    flex: 2;
    color: #fff;
}

header form {
    flex: 3;
}

header form>input {
    width: 100%;
    height: 24px;
    text-indent: 10px;
    border-radius: 5px;
    border: none;
    outline: none;
    box-shadow: 0 1px 0 rgba(255, 255, 255, 0.24), 0 1px 6px rgba(0, 0, 0, 0.45) inset;
}

section>h2 {
    position: relative;
    margin: 15px 0;
}

section li {
    margin: 10px 0;
    height: 32px;
    line-height: 32px;
    background: #fff;
    position: relative;
    padding: 0 16px;
    border-left: 5px #629a9c solid;
    box-shadow: 0 1px 2px rgb(0, 0, 0, .1);
    border-radius: 3px;

}

section li>input[type=checkbox] {
    width: 22px;
    height: 22px;
    vertical-align: middle;
}

section li>span {
    position: absolute;
    right: 20px;
    top: 6px;
    display: inline-block;
    width: 20px;
    height: 20px;
    line-height: 16px;
    box-sizing: border-box;
    text-align: center;
    background: #ccc;
    border: 3px #fff solid;
    border-radius: 10px;
    outline: 3px #ccc solid;
    font-weight: 900;
    color: #fff;
    cursor: pointer;
}

section h2>span {
    position: absolute;
    right: 20px;
    top: 6px;
    width: 22px;
    height: 22px;
    line-height: 22px;
    text-align: center;
    background: #e6e6f9;
    border-radius: 11px;
    color: #333;
    font-size: 12px;
    box-shadow: 1px 2px 3px #999;
}

.gray {
    border-left: 5px solid #b3b3b3;
    opacity: 0.5;
}
</style>