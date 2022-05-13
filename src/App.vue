<template>
  <h1>Tasks Vuejs</h1>
  <input
    type="text"
    v-model="text"
    @keyup.enter="addTask"
  />
  <button @click="addTask">+</button>
  
  <ul>
    <li v-for="(task, index) in tasks" :key="index" class="tasks">
      <div>
        <span :class="task.isDone ? 'isDone' : '' " @dblclick="doneTask(task)">{{ task.text }}</span>
        <input type="checkbox" :checked="task.isDone" @click="doneCheckedTask(task)" />
        <span @click="removeTask(task)">remover</span>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  data: () => ({
    tasks: [
      {text: "Terminar curso vuejs 3", isDone: true},
      {text: "Estudar Laravel", isDone: false},
      {text: "Ler o livro do Zeno Rocha", isDone: false},
    ],
    text: ''
  }),
  methods: {
    addTask() {
      this.tasks.push({
        text: this.text,
        isDone: false
      });

      this.text = "";
    },

    doneTask(task) {
      task.isDone = !task.isDone;
    },

    doneCheckedTask(task) {
      task.isDone = !task.isDone;
    },

    removeTask(task) {
      this.tasks = this.tasks.filter(el => el.text !== task.text);
    }
  },
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