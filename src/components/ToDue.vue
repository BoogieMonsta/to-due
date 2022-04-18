<script setup>

import {ref} from "vue";
import { Icon } from '@iconify/vue';

defineProps({
  title: String,
  tagline: String
})

const newToDo = ref('');
let lstToDos = ref([]);

function addToDo() {
  lstToDos.value.push({
    id: Date.now(),
    done: false,
    task: newToDo.value,
  })
  newToDo.value = '';
}

function deleteToDo(index) {
  lstToDos.value.splice(index, 1);
}

function toggleDone(toDo) {
  toDo.done = !toDo.done;
}

function markAllDone() {
  lstToDos.value.forEach(toDo => toDo.done = true);
}

function markAllToDo() {
  lstToDos.value.forEach(toDo => toDo.done = false);
}

function clearAll() {
  lstToDos.value = [];
}

function clearDone() {
  lstToDos.value.forEach(toDo => {
    if (toDo.done) {
      lstToDos.value.splice(lstToDos.value.indexOf(toDo), 1);
    }
  });
}

</script>

<template>
  <h1>{{ title }}</h1>
  <p class="tagline"><em>{{ tagline }}</em></p>
  <form @submit.prevent="addToDo" class="form">
    <label class="inputLabel">I need to... </label>
    <input v-model="newToDo" name="newToDo">
    <button class="addToDoBtn">
      <Icon icon="carbon:add-filled" :inline="true" :style="{ fontSize: '36px' }"/>
    </button>
  </form>
  <button class="btn" @click="markAllDone">ALL DONE</button>
  <button class="btn" @click="markAllToDo">ALL TO DO</button>
  <button class="btn" @click="clearDone">CLEAR DONE</button>
  <button class="btn" @click="clearAll">CLEAR ALL</button>
  <ul class="toDoWrapper">
    <li v-for="(toDo, index) in lstToDos" :key="toDo.id" class="toDo">
      <span :class="{ done: toDo.done }" @click="toggleDone(toDo)">
        <strong>{{ toDo.task }}</strong>
        <button @click="deleteToDo(index)" class="deleteBtn">
          <Icon icon="gridicons:cross-circle" :inline="true"/>
        </button>
      </span>
    </li>
  </ul>
</template>

<style scoped>
a {
  color: #42b983;
}

.btn {
  padding: 0.75em 0.85em 0.75em 0.85em;
  letter-spacing: 0.04em;
  border-radius: 0.3em;
  font-weight: bold;
  border: none;
  margin: 4em 0.5em 0 0.5em;
  color: white;
  background: #42b983;
  cursor: pointer;
}

.form {
  display: flex;
  justify-content: center;
}

.inputLabel {
  align-self: center;
  margin-right: 0.5em;
}

input {
  border-radius: 0.3em;
  padding: 0.8em;
  border-width: 0.1em;
  max-height: 20px;
  align-self: center;
}

.tagline {
  margin-top: -2.5em;
  margin-bottom: 5em;
  font-size: smaller;
}

.toDo {
  cursor: pointer;
  list-style-type: none;
  line-height: 2em;
}

.done {
  text-decoration: line-through;
  color: darkgray;
}

.deleteBtn {
  color: indianred;
  background: none;
  border: none;
  cursor: pointer;
}

.addToDoBtn {
  color: #42b983;
  background: none;
  border: none;
  cursor: pointer;
  margin-left: 0.5em;
}


</style>
