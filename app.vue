<template>
  <NuxtLayout>
  <div>
    <form @submit.prevent="addTask">
      <input v-model="newTask" name="newTask" autocomplete="off" />
      <button>追加する</button>
    </form>
    <ul>
      <li v-for="(task, index) in tasks" :key="task">
        <span>{{ task }}</span>
        <button @click="$event =>deleteTask(index)">削除する</button>
      </li>
    </ul>
    <button @click="allDeleteTasks">全て削除する</button>
    <div>件数{{ tasks.length }}</div>
    
  </div>
  </NuxtLayout>
</template>
<script setup>
  const tasks = useCookie(
    'tasks',
    {
      default: () => []
    }
  )
  // 新しく追加されるタスク
  const newTask = ref('')

  function addTask() {
    if(newTask.value.length >= 1) {
      tasks.value.push(newTask.value)
    }
    newTask.value = ''
  }

  function deleteTask(index) {
    tasks.value.splice(index, 1)
  }

  function allDeleteTasks() {
    tasks.value = []
  }
</script>
