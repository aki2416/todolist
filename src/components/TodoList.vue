<script setup lang="ts">
import { ref } from 'vue'

interface Todo{
    text: string
    done: boolean
}

const todos = ref<Todo[]>([
    { text: 'レポートの作成', done: false },
    { text: '寝る', done: false },
    { text: '買い物', done: true },
])

const newTodoText = ref('')
const addTodo = () => {
    if (newTodoText.value != ''){
        todos.value.push({ text: newTodoText.value, done: false})
    }
}
const removeTodo = (todo: Todo) => {
    const index = todos.value.indexOf(todo)
    if (index !== -1) {
        todos.value.splice(index, 1)
    }
    newTodoText.value = ''
}
</script>

<template>
    <div>
        <h2>TodoList</h2>
        <h3>完了済みのタスク</h3>
        <ul>
            <il v-for="todo in todos" :key="todo.text">
                <div v-if="todo.done == true">
                    <button @click="removeTodo(todo)">削除</button>
                    <button @click="todo.done = false">未完了にする</button>
                    タスク名:
                    {{ todo.text }}
                    
                </div> 
            </il>
        </ul>
    </div>
    <h3>未完了のタスク</h3>
    <div>
        <ul>
            <il v-for="todo in todos" :key="todo.text">
                <div v-if="todo.done == false">
                    <button @click="removeTodo(todo)">削除</button>
                    <button @click="todo.done = true">完了済みにする</button>
                    タスク名:
                    {{ todo.text }}
                </div>
            </il>
        </ul>
    </div>
    <div>
        <label>
            <h3>タスクの追加</h3>
            タスク名:
            <input v-model="newTodoText" type="text" />
        </label>
        <button @click="addTodo">追加</button>
    </div>
</template>

<style></style>