<template>
  <div class="content">
    <h1>Tarefas</h1>
    <div class="progress-bar">
      <div class="progress" :style="getProgress"></div>
    </div>
    <h3>{{ getTotal }}%</h3>
  </div>
</template>
<script>
export default {
  props: {
    total: { type: Number, required: true },
    actual: { type: Number, required: true },
  },
  computed: {
    getProgress() {
      return `width: ${this.getTotal}%`;
    },
    getTotal() {
      let value = (this.actual / this.total) * 100 || 0;
      return Math.floor(value);
    },
  },
};
</script>

<style scoped>
.content {
  display: flex;
  justify-content: center;
  width: 100%;
  flex-direction: column;
  align-items: center;
}
.progress-bar {
  display: flex;
  border: solid 1px #bbb;
  width: 60%;
  height: 20px;
  border-radius: 8px;
  margin-top: 50px;
}

.progress {
  left: 0;
  height: 100%;
  border-radius: 8px;
  background-color: #4c4f;
}
</style>