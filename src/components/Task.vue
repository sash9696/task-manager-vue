<template>
  <div @dblclick="$emit('toggle-reminder',task.id)" :class="[task.reminder ? 'reminder' : '' , 'task']">
    <h3>
      {{ task.text }}
      <i @click="$emit('delete-task', task.id)" class="fas fa-times"> </i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
};
</script>

<style>
.fas {
  color: red;
}
.task {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  background: #f4f4f4;
  margin: 2px;
  cursor: pointer;
  padding: 10px 20px;
  width: 300px;
  height: 100px;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  width: 300px;
  align-items: center;
  justify-content: space-between;
}
.task p {
  display: flex;
  width: 300px;
  align-items: center;
  justify-content: flex-start;
}
</style>