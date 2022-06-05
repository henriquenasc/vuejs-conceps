<template>
  <h1>Tasks Vuejs</h1>
  <input
    type="text"
    v-model="state.text"
    @keyup.enter="addTask"
  />
  <button @click="addTask">+</button>
  
  <ul>
    <li v-for="(task, index) in state.tasks" :key="index" class="tasks">
      <div>
        <span :class="task.isDone ? 'isDone' : '' " @dblclick="doneTask(task)">{{ task.text }}</span>
        <input type="checkbox" :checked="task.isDone" @click="doneCheckedTask(task)" />
        <span @click="removeTask(task)">remover</span>
      </div>
    </li>
  </ul>
</template>

<script>
import { reactive } from '@vue/reactivity';

const state = reactive({
  tasks: [
    {text: "Terminar curso vuejs 3", isDone: true},
    {text: "Estudar Laravel", isDone: false},
    {text: "Ler o livro do Zeno Rocha", isDone: false},
  ],

  text: '',
})

function addTask() {
  if(state.text != '') {
    state.tasks.push({
      text: state.text,
      isDone: false
    });
    state.text = "";
  } else {
    alert("Campo vazio!");
  }
}

function doneTask(task) {
  task.isDone = !task.isDone;
}

function doneCheckedTask(task) {
  task.isDone = !task.isDone;
}

function removeTask(task) {
  state.tasks = state.tasks.filter(el => el.text !== task.text);
}

export default {
  setup() {
    return {
      state,
      addTask,
      doneTask,
      doneCheckedTask,
      removeTask    
    }
  }
}
</script>

<style scoped>
  .tasks {
    cursor: pointer;
    font-family: sans-serif;
    font-weight: 450;
    list-style: none;
    color: green;
  }
  .isDone {
    color: red;
    text-decoration: line-through;
  }
</style>