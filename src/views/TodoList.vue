<script setup>
import { ref } from "vue";
const todo = ref('');
const todoList = ref([]);

const handleAddButton = () => {
    if (todo.value.trim() === '') return;
    todoList.value.push({
        text: todo.value,
        checked: false
    });
    todo.value = '';
}

const handleDeleteButton = (index) => {
    todoList.value.splice(index, 1);
}

const handleCheckBox = (index) => {
    todoList.value[index].checked = !todoList.value[index].checked;
}
</script>

<template>
    <div class="wrapper">
        <h1>TODO</h1>
        <div class="inputWrapper">
            <input v-model="todo" class="input" type="text">
            <button class="addButton" @click="handleAddButton">추가</button>
        </div>
        <div class="contentWrapper">
            <!-- vue에선 map 대신 v-for를 사용해서 리스트 반복 구현 -->
            <!-- todoList가 반복할 대상 배열이고 item은 배열의 각 요소, index는 말그대로 인덱스.. -->
            <div class="content" v-for="(item, index) in todoList" :key="index">
                <p :style="{ textDecoration: item.checked ? 'line-through' : 'none' }">{{ item.text }}</p>
                <div class="buttonWrapper">
                    <input type="checkBox" :checked="item.checked" @change="handleCheckBox(index)">
                    <button class="deleteButton" @click="handleDeleteButton(index)">삭제</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.inputWrapper {
    display: flex;
    align-items: center;
    gap: 20px;
}
.input {
    width: 500px;
    height: 35px;
    padding-left: 20px;
    padding-right: 20px;
    border-radius: 30px;
    border: none;
    box-shadow: 0px 4px 10px 4px rgba(0,0,0,0.1);
    outline: none;
}
.addButton {
    width: 55px;
    height: 35px;
    border-radius: 30px;
    border: none;
    background-color: black;
    align-items: center;
    justify-content: center;
    color: white;
    cursor: pointer;
    transition: 0.2s;
}
.addButton:hover {
    background-color: rgb(110, 110, 110);
}
.contentWrapper {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin-top: 40px;
}
.content {
    display: flex;
    align-items: center;
    width: 600px;
    justify-content: space-between;
    height: 35px;
}
.buttonWrapper {
    display: flex;
    align-items: center;
    gap: 20px;
}
.deleteButton {
    width: 55px;
    height: 35px;
    border-radius: 30px;
    border: none;
    background-color: rgb(252, 72, 72);
    align-items: center;
    justify-content: center;
    color: white;
    cursor: pointer;
    transition: 0.2s;
}
.deleteButton:hover {
    background-color: rgb(255, 99, 99);
}
</style>