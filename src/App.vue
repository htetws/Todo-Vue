<template>
  <div class="col-11 col-md-6 col-lg-4 rounded-3 container bg-white my-5 p-3 border">
    <Header @add-task-toggle="AddTaskToggle" @hide-done-task="HideDone" :title="title" :addTaskToggle="addTaskToggle" />
    <AddTask v-show="addTaskToggle" @add-task-data="AddTaskData" />
    <hr>
    <Tasks @toggle-task="ToggleTask" @task-delete="TaskDelete" :tasks="tasks" />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';
import AddTask from './components/AddTask.vue';
export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask
  },
  data: () => ({
    title: "Todo Task",
    addTaskToggle: false,
    tasks: []
  }),
  methods: {
    AddTaskData(task) {
      this.tasks = [...this.tasks, task];
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    },
    TaskDelete(id) {
      if (confirm('Are u sure ?')) {
        this.tasks = this.tasks.filter(task => task.id !== id);
        localStorage.setItem('tasks', JSON.stringify(this.tasks))
      }
    },
    ToggleTask(id) {
      this.tasks = this.tasks.map(task => task.id === id ? ({ ...task, reminder: !task.reminder }) : task);
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    AddTaskToggle() {
      this.addTaskToggle = !this.addTaskToggle
    },
    HideDone(status) {
      if (status) {
        this.tasks = this.tasks.filter(task => !task.reminder)
      } else {
        const data = localStorage.getItem('tasks');
        const localData = JSON.parse(data);
        this.tasks = localData != null ? localData : this.tasks;
      }
    }
  },
  created() {
    const data = localStorage.getItem('tasks');
    const localData = JSON.parse(data);
    this.tasks = localData != null ? localData : this.tasks;
  }
}
</script>