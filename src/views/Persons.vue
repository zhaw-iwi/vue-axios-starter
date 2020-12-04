<template>
  <div class="mb-5">
    <h1 class="mt-3">List of all Persons</h1>
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Birthdate</th>
        </tr>
      </thead>
      <tbody>
        <tr :key="person.id" v-for="person in persons">
          <td>
            <router-link v-bind:to="'/persons/' + person.id">
              {{ person.id }}
            </router-link>
          </td>
          <td>
            {{ person.name }}
          </td>
          <td>
            {{ person.birthdate }}
          </td>
        </tr>
      </tbody>
    </table>
    <router-link to="/create-person">+ Add Person</router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      persons: [],
    };
  },
  mounted: function () {
    this.getPersons();
  },
  methods: {
    getPersons: function () {
      axios.get("http://localhost:8080/infections/persons").then((response) => {
        this.persons = response.data;
      });
    },
  },
};
</script>