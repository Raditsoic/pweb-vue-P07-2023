<template>
    <div class="d-flex justify-content-lg-end" style="margin-top: 20px; margin-right: 20px;">
      <button @click="modal" class="btn btn-primary">Add New Task</button>
      <modal :show="addTaskModal" @close="modal">
        <template v-slot:modal-title>
          <h1 class="modal-title fs-5">Add Task</h1>
        </template>
        <createTask @close-modal="modal"></createTask>
      </modal>
    </div>
  
    <viewTask></viewTask>
</template>
  
<script>
  import Modal from "../components/Modal.vue";
  import createTask from "../components/createTodo.vue";
  import viewTask from "../components/viewTask.vue";
  import { tasks } from "../data/task.js";
  
  export default {
    components: {
      Modal,
      createTask,
      viewTask
    },
    data() {
      return {
        tasks,
        addTaskModal: false
      };
    },
    methods: {
      modal() {
        this.addTaskModal = !this.addTaskModal;
      }
    }
  };
</script>

<style>

</style>
  