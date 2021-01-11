<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-sm-6">
        <form @submit.prevent="submit">
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
  data() {
    return {
      task: {},
    };
  },
  methods: {
    submit() {
      axios.post(`/api/tasks`, this.task).then((res) => {
        this.$router.push({ name: 'task.list' });
      });
    },
  },
};
</script>
