<script setup>
import { reactive } from 'vue';
import Header from './components/Header.vue';
import Form from './components/Form.vue';
import TaskList from './components/TaskList.vue';

const state = reactive({
  filter: 'all',
  taskTemp: '',
  tasks: [
  ],
});

const getPendingTasks = () => {
  return state.tasks.filter(task => !task.completed);
};

const getCompletedTasks = () => {
  return state.tasks.filter(task => task.completed);
};

const getFilteredTasks = () => {
  const { filter } = state;
  switch (filter) {
    case 'pending':
      return getPendingTasks();
    case 'completed':
      return getCompletedTasks();
    default:
      return state.tasks;
  }
};

const addTask = () => {
  const newTask = {
    title: state.taskTemp,
    completed: false,
  };
  state.tasks.push(newTask);
  state.taskTemp = '';
};
</script>

<template>
<div class="container-fluid">
  <Header :pending-tasks="getPendingTasks().length" />
  <Form :change-filter="event => state.filter = event.target.value" :task-temp="state.taskTemp" :edit-task-temp="event => state.taskTemp = event.target.value" :add-task="addTask" />
  <TaskList :tasks="getFilteredTasks()" />
</div>
</template>
