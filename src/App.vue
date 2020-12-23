<template>
  <div id="app">
    <barra-progresso :total="totalProgressValue" :actual="actualProgress" />
    <add-tarefa @addTask="addNewTask" />
    <tarefas-grid
      :tasks="tasks"
      @deleteTask="deleteTask"
      @finishTask="finishTask"
    />
  </div>
</template>

<script>
import barraProgresso from "../componentes/barraProgresso";
import addTarefa from "../componentes/addTarefa";
import tarefasGrid from "../componentes/tarefasGrid";
export default {
  components: { barraProgresso, addTarefa, tarefasGrid },
  data() {
    return {
      tasks: [],
    };
  },
  computed: {
    totalProgressValue() {
      return this.tasks.length;
    },
    actualProgress() {
      let COMPLETE = 0;
      this.tasks.map((item) => {
        if (item.pending) COMPLETE++;
      });
      return COMPLETE;
    },
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
    },
  },
  methods: {
    addNewTask(task) {
      this.tasks.push(task);
    },
    finishTask(task) {
      this.tasks.map((item) => {
        if (task.id === item.id) {
          item.pending = true;
        }
      });
    },
    deleteTask(task) {
      const index = this.tasks.indexOf(task);
      this.tasks.splice(index, 1);
    },
  },
  created() {
    const json = localStorage.getItem("tasks");
    const array = JSON.parse(json);
    this.tasks = Array.isArray(array) ? array : [];
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Texturina:ital@1&display=swap");
body {
  font-family: "Lato", sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #fff;
}

#app {
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-family: "Texturina", serif;
  font-size: 5rem;
}
</style>
