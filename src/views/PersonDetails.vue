<template>
  <div class="mb-5">
    <h1 class="mt-3">Person (ID: {{ personId }})</h1>
    <p>Name: {{ person.name }}</p>
    <p>Birthdate: {{ person.birthdate }}</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      personId: this.$route.params.id,
      person: { },
    };
  },
  mounted: function() {
    this.getPerson();
  },
  methods: {
    getPerson: function() {
      axios.get("http://localhost:8080/infections/persons/" + this.personId )
      .then( response => {
        this.person = response.data;
      })
    }
  }
};
</script>