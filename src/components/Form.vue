<script setup>
  const props = defineProps(['addTask', 'taskTemp', 'changeFilter', 'editTaskTemp']);
</script>

<template>
  <form @submit.prevent="props.addTask">
    <div class="row">
      <div class="col">
        <input
          :value="props.taskTemp"
          @change="props.editTaskTemp"
          required
          type="text"
          placeholder="Enter task description here..."
          class="form-control"
        />
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-outline-primary">Add Task</button>
      </div>
      <div class="col-md-2">
        <select @change="props.changeFilter" class="form-control">
          <option value="all">All Tasks</option>
          <option value="pending">Pending</option>
          <option value="completed">Completed</option>
        </select>
      </div>
    </div>
  </form>
</template>
