<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-sm-6">
        <form @submit.prevent="submit">
          <div class="form-group row">
            <label
              for="id"
              class="col-sm-3 col-form-label"
            >ID</label>
            <input
              id="id"
              v-model="task.taskId"
              type="text"
              class="col-sm-9 form-control-plaintext"
              readonly
            >
          </div>
          <div class="form-group row">
            <label
              for="title"
              class="col-sm-3 col-form-label"
            >Title</label>
            <input
              id="title"
              v-model="task.title"
              type="text"
              class="col-sm-9 form-control"
            >
          </div>
          <div class="form-group row">
            <label
              for="content"
              class="col-sm-3 col-form-label"
            >Content</label>
            <input
              id="content"
              v-model="task.content"
              type="text"
              class="col-sm-9 form-control"
            >
          </div>
          <div class="form-group row">
            <label
              for="person-in-charge"
              class="col-sm-3 col-form-label"
            >Person In Charge</label>
            <input
              id="person-in-charge"
              v-model="task.person_in_charge"
              type="text"
              class="col-sm-9 form-control"
            >
          </div>
          <button
            type="submit"
            class="btn btn-primary"
          >
            Submit
          </button>
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
    submit() {
      axios.put(`/api/tasks/${this.taskId}`, this.task).then((res) => {
        this.$router.push({ name: 'task.list' });
      });
    },
  },
};
</script>
