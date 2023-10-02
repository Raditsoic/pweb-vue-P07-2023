<script>
import { tasks } from "../data/task.js";
    export default {
        data() {
          return {
            tasks,
          }
        },
        methods: {
          priorityClass(scale, status)
          {
            if (status === true)
            {
              return "table-dark line-through";
            }

            else{
            switch(scale)
            {
              case "Low Priority": return "table-primary";
              case "Medium Priority": return "table-warning";
              case "High Priority": return "table-danger";
            }
          }
          }
        },
        mounted() {
          document.title = "Todo"; // Set the desired title
        }
    }
</script>

<template>
    <div class="d-flex text-center align-items-center justify-content-center">
      <table class="table table-hover">
        <thead>
          <tr>
            <th scope="col">Activity</th>
            <th scope="col">Time</th>
            <th></th>
            <th></th>
            <th></th>
            <th scope="col">Priority</th>
          </tr>
        </thead>
        <tbody>
          <template v-for="(task, id) in tasks.task" :key="task.id">
            <tr :class="priorityClass(task.priority, task.status)">
              <td>{{ task.name }}</td>
              <td>{{ task.time }}</td>
              <td>
                <input type="checkbox" v-model="task.status" @click="updateTaskStatus(id)">
              </td>
              <td><button class="btn" :class="{ 'btn-dark': task.status }" @click="tasks.deleteTask(task.id)">
                <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class="bi bi-journal-x" viewBox="0 0 16 16">
                  <path fill-rule="evenodd" d="M6.146 6.146a.5.5 0 0 1 .708 0L8 7.293l1.146-1.147a.5.5 0 1 1 .708.708L8.707 8l1.147 1.146a.5.5 0 0 1-.708.708L8 8.707 6.854 9.854a.5.5 0 0 1-.708-.708L7.293 8 6.146 6.854a.5.5 0 0 1 0-.708z"/>
                  <path d="M3 0h10a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2v-1h1v1a1 1 0 0 0 1 1h10a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H3a1 1 0 0 0-1 1v1H1V2a2 2 0 0 1 2-2z"/>
                  <path d="M1 5v-.5a.5.5 0 0 1 1 0V5h.5a.5.5 0 0 1 0 1h-2a.5.5 0 0 1 0-1H1zm0 3v-.5a.5.5 0 0 1 1 0V8h.5a.5.5 0 0 1 0 1h-2a.5.5 0 0 1 0-1H1zm0 3v-.5a.5.5 0 0 1 1 0v.5h.5a.5.5 0 0 1 0 1h-2a.5.5 0 0 1 0-1H1z"/>
                </svg>
              </button></td>
              <td><router-link :to="{ name: 'task', params: { id: id } }">
                <button class="btn" :class="{ 'btn-dark': task.status }">
                  <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class="bi bi-pencil-square" viewBox="0 0 16 16">
                    <path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
                    <path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"/>
                  </svg>
                </button>
            </router-link></td>
            <td>{{ task.priority }}</td>
            </tr>
          </template>
        </tbody>
      </table>
    </div>
    <button  @click="tasks.clearAll" class="btn btn-secondary m-1">Clear All Tasks</button>
    <button id="done-clear" @click="tasks.clearDone" class="btn btn-secondary m-1">Clear Done</button>
  </template>

<style>
.line-through {
  text-decoration: line-through;
}
tbody td {
  vertical-align: middle;
}
</style>