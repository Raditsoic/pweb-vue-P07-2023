<template>
  <title>Create Task</title>
  <input type="text" class="form-control m-1" id="todoName" v-model="taskName" 
      placeholder="What do you need to do?">
  <input type="date" class="form-control m-1" id="todoTime" v-model="taskTime"
      placeholder="When do you need to do it?">
  <select class="form-select m-1" aria-label="Default select example" v-model="taskPriority">
    <option selected>Select Priority</option>
    <option value="High Priority">High</option>
    <option value="Medium Priority">Medium</option>
    <option value="Low Priority">Low</option>
  </select>
  
  <button @click="addTask" class="btn btn-primary m-1">Add Task</button>
</template>

<script>
import { tasks } from "../data/task.js";

export default {
  emits: ["close-modal"],
  data() {
    return {
      tasks,
      taskName: "",
      taskTime: "",
      taskPriority: "Select Priority",
      status: "",
    };
  },
  methods: {
    addTask() {
      if (
        this.taskName === "" ||
        this.taskTime === "" ||
        this.taskPriority === ""
      )
        return;
        const existingIds = this.tasks.task.map((task) => task.id);
        let newId = 0;
        while (existingIds.includes(newId.toString())) {
          newId++;
        }

        
        const newTask = {
        id: newId.toString(),
        name: this.taskName,
        time: this.taskTime,
        priority: this.taskPriority,
        status: false,
      };
      console.log(newTask.id);
      tasks.addTask(newTask);
      this.taskName = "";
      this.taskTime = "";
      this.$emit("close-modal");
    },
  },
  mounted() {
    document.title = "Create Task";
  }
};
</script>

<style>

</style>