<template>
  <div class="mb-5">
    <h1 class="mt-3">List of all Infections</h1>
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Location</th>
          <th>Time</th>
          <th>Pathogen ID</th>
          <th>Person ID</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="infection in infections" :key="infection.id">
          <td>
            {{ infection.id }}
          </td>
          <td>
            {{ infection.location }}
          </td>
          <td>
            {{ infection.time }}
          </td>
          <td>
            {{ infection.pathogen.id }}
          </td>
          <td>
            {{ infection.person.id }}
          </td>
        </tr>
      </tbody>
    </table>
    <router-link to="/create-infection">+ Add Infection</router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      infections: [],
    };
  },
  mounted: function () {
    this.getInfections();
  },
  methods: {
    getInfections: function () {
      axios.get("http://localhost:8080/infections/infections").then((response) => {
        this.infections = response.data;
      });
    },
  },
};
</script>
