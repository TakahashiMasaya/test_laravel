<template>
  <div class="container">
    <table class="table table-hover">
      <thead class="thead-light">
        <tr>
          <th scope="col">
            #
          </th>
          <th scope="col">
            Title
          </th>
          <th scope="col">
            Content
          </th>
          <th scope="col">
            Person In Charge
          </th>
          <th scope="col">
            Show
          </th>
          <th scope="col">
            Edit
          </th>
          <th scope="col">
            Delete
          </th>
        </tr>
      </thead>
      <tbody
        v-for="task in tasks"
        :key="task.id"
      >
        <tr>
          <th scope="row">
            {{ task.id }}
          </th>
          <td>{{ task.title }}</td>
          <td>{{ task.content }}</td>
          <td>{{ task.person_in_charge }}</td>
          <td>
            <router-link :to="{name: 'task.show', params: {taskId: task.id}}">
              <button class="btn btn-primary">
                Show
              </button>
            </router-link>
          </td>
          <td>
            <router-link :to="{name: 'task.edit', params: {taskId: task.id}}">
              <button class="btn btn-success">
                Edit
              </button>
            </router-link>
          </td>
          <td>
            <button
              class="btn btn-danger"
              @click.prevent="deleteTask(task.id)"
            >
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      tasks: [],
      htmlTasks: '',
    };
  },
  mounted() {
    this.getTasks();
  },
  methods: {
    getTasks() {
      axios.get('/api/tasks').then((res) => {
        this.tasks = res.data;
      });
    },
    deleteTask(id) {
      axios.delete(`/api/tasks/${id}`)
        .then((res) => {
          this.getTasks();
        });
    },
  },
};
</script>
