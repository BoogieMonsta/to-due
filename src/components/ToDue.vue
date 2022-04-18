<script setup>

import {ref} from "vue";

defineProps({
  title: String,
  tagline: String
})

const newToDo = ref('');
const lstToDos = ref([]);

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

function clearAll() {
  lstToDos.value = [];
}

</script>

<template>
  <h1>{{ title }}</h1>
  <p class="tagline"><em>{{ tagline }}</em></p>
  <form @submit.prevent="addToDo">
    <label>I need to... </label>
    <input v-model="newToDo" name="newToDo">
    <button>Add</button>
  </form>
  <button @click="markAllDone">Mark all done</button>
  <button @click="clearAll">Clear all</button>
  <ul>
    <li v-for="(toDo, index) in lstToDos" :key="toDo.id" class="toDo">
      <h3 :class="{ done: toDo.done }" @click="toggleDone(toDo)">{{ toDo.task }}
        <button @click="deleteToDo(index)" class="deleteBtn">Delete</button>
      </h3>
    </li>
  </ul>
</template>

<style scoped>
a {
  color: #42b983;
}

button {
  padding: 0.75em 0.85em 0.75em 0.85em;
  letter-spacing: 0.01em;
  border-radius: 0.3em;
  border: none;
  margin: 1em;
  color: white;
  background: #42b983;
}

input {
  border-radius: 0.3em;
  padding: 0.8em;
  border-width: 0.1em;
}

.tagline {
  margin-top: -2.5em;
  margin-bottom: 5em;
  font-size: smaller;
}

.toDo {
  cursor: pointer;
  list-style-type: none;
}

.done {
  text-decoration: line-through;
}

.deleteBtn {
}


</style>
