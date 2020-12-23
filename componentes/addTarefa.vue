<template>
  <div class="tarefas">
    <input
      @keydown.enter="addTask"
      v-model="newTask.name"
      type="text"
      class="tarefas-add"
      placeholder="Adicionar mais uma tarefa"
    /><button @click="addTask" class="add">+</button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      newTask: {
        id: 0,
        name: "",
        pending: false,
      },
    };
  },
  methods: {
    addTask() {
      this.$emit("addTask", { ...this.newTask });
      this.newTask.id++;
      this.newTask.name = "";
    },
  },
};
</script>
<style scoped>
.tarefas {
  display: flex;
  justify-content: center;
  margin-top: 50px;
}

.tarefas-add {
  border: solid 1px #bbb;
  width: 300px;
  height: 35px;
  outline: none;
  padding-left: 10px;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
  background-color: rgb(95, 95, 95);
}

.add {
  height: 39px;
  background-color: rgb(61, 170, 61);
  width: 35px;
  border: solid 1px #bbb;
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
  outline: none;
  cursor: pointer;
  color: white;
  font-size: 20px;
}
</style>