<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-sm-6">
        <form>
          <div class="form-group row border-bottom">
            <label
              for="id"
              class="col-sm-3 col-form-label"
            >ID</label>
            <input
              id="id"
              type="text"
              class="col-sm-9 form-control-plaintext"
              readonly
              :value="taskId"
            >
          </div>
          <div class="form-group row border-bottom">
            <label
              for="title"
              class="col-sm-3 col-form-label"
            >Title</label>
            <input
              id="title"
              type="text"
              class="col-sm-9 form-control-plaintext"
              readonly
              :value="task.title"
            >
          </div>
          <div class="form-group row border-bottom">
            <label
              for="content"
              class="col-sm-3 col-form-label"
            >
              Content</label>
            <input
              id="content"
              type="text"
              class="col-sm-9 form-control-plaintext"
              readonly
              :value="task.content"
            >
          </div>
          <div class="form-group row border-bottom">
            <label
              for="person-in-charge"
              class="col-sm-3 col-form-label"
            >Person In Charge
            </label>
            <input
              id="person-in-charge"
              type="text"
              class="col-sm-9 form-control-plaintext"
              readonly
              :value="task.person_in_charge"
            >
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  props: {
    taskId: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      task: {},
    };
  },
  mounted() {
    this.getTask();
  },
  methods: {
    getTask() {
      axios.get(`/api/tasks/${this.taskId}`).then((res) => {
        this.task = res.data;
      });
    },
  },
};
</script>
