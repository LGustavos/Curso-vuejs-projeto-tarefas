<template>
  <div class="grid-tarefas">
    <div class="grid">
      <div
        class="task"
        :class="task.pending ? 'done' : 'pending'"
        v-for="task in tasks"
        :key="task.id"
        @click="finishTask(task)"
      >
        <span class="" @click="deleteTask(task)">x</span>
        <h3>{{ task.name }}</h3>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    tasks: { type: Array, required: true },
  },
  methods: {
    finishTask(task) {
      this.$emit("finishTask", task);
    },
    deleteTask(task) {
      this.$emit("deleteTask", task);
    },
  },
};
</script>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");
.grid-tarefas {
  display: flex;
  justify-content: center;
  margin-top: 50px;
}

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-column-gap: 20px;
  grid-row-gap: 20px;
  justify-content: center;
}

.task {
  text-align: center;
  padding: 10px;
  border-radius: 8px;
  width: 250px;
  height: 80px;
  cursor: pointer;
  user-select: none;
}

.task span {
  float: right;
}

.pending {
  background-color: #f44336;
  border-left: solid 12px #b73229;
}

.task h3 {
  font-family: "Montserrat", sans-serif;
  font-size: 1.1rem;
}

.done {
  background-color: #4c4f;
  border-left: solid 12px #0a8f08;
  color: #ddd;
  text-decoration: line-through;
}
</style>