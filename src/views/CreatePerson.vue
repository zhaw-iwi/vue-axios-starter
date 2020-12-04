<template>
  <div class="mb-5">
    <h1 class="mt-3">Add a person</h1>

    <form>
      <div class="form-group">
        <label>Name</label>
        <input class="form-control" type="text" v-model="person.name" />
      </div>
      <div class="form-group">
        <label>Birthdate</label>
        <input class="form-control" type="number" v-model="person.birthdate" />
      </div>
      <button v-on:click="addPerson()" type="button" class="btn btn-primary">
        Add Person
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      person: {
        name: "",
        birthdate: null,
      },
    };
  },
  methods: {
    addPerson: function() {
      axios
        .post("http://localhost:8080/infections/persons", this.person)
        .then((response) => {
          alert("Person added");
          console.log(response.data);

          // reset input fields
          this.person = {};

          // uncomment the following line if you want to redirect to /persons
          //this.$router.push("/persons");
        });
    },
  },
};
</script>