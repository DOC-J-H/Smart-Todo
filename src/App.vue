<template>
  <div>
    <h1>智能待办事项管理器</h1>
    <form @submit.prevent="addTask">
      <input v-model="newTask" placeholder="输入新任务" />
      <button type="submit">添加任务</button>
    </form>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        {{ task.name }}
        <button @click="removeTask(task.id)">删除</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTask = ref('');
    const tasks = ref(JSON.parse(localStorage.getItem('tasks')) || []);

    const addTask = () => {
      const task = { id: Date.now(), name: newTask.value };
      tasks.value.push(task);
      localStorage.setItem('tasks', JSON.stringify(tasks.value));
      newTask.value = '';
    };

    const removeTask = (id) => {
      tasks.value = tasks.value.filter(task => task.id !== id);
      localStorage.setItem('tasks', JSON.stringify(tasks.value));
    };

    return { newTask, tasks, addTask, removeTask };
  },
};
</script>
