<template>
  <div class="mb-5">
    <h1 class="mt-3">Add an infection</h1>

    <form>
      <div class="form-group">
        <label>Location</label>
        <input class="form-control" type="text" v-model="infection.location" />
      </div>
      <div class="form-group">
        <label>Time</label>
        <input class="form-control" type="number" v-model="infection.time" />
      </div>
      <div class="form-group">
        <label>Pathogen ID</label>
        <select v-model="infection.pathogen_id" class="form-control">
          <option v-for="id in pathogen_ids" v-bind:key="id">{{ id }}</option>
        </select>
      </div>
      <div class="form-group">
        <label>Person ID</label>
        <select v-model="infection.person_id" class="form-control">
          <option v-for="id in persons_ids" v-bind:key="id">{{ id }}</option>
        </select>
      </div>

      <button v-on:click="addInfection()" type="button" class="btn btn-primary">
        Add Infection
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      infection: {
        location: null,
        time: null,
        pathogen_id: null,
        person_id: null,
      },
      persons_ids: [],
      pathogen_ids: [],
    };
  },
  mounted: function () {
    this.getPersonIds();
    this.getPathogenIds();
  },
  methods: {
    getPersonIds: function () {
      axios.get("http://localhost:8080/infections/persons").then((response) => {
        this.persons_ids = [];
        for (let person of response.data) {
          this.persons_ids.push(person.id)
        }
      });
    },
    getPathogenIds: function () {
      axios.get("http://localhost:8080/infections/pathogens").then((response) => {
        this.pathogen_ids = [];
        for (let pathogen of response.data) {
          this.pathogen_ids.push(pathogen.id)
        }
      });
    },
    addInfection() {
      axios
        .post("http://localhost:8080/infections/infections", this.infection)
        .then((response) => {
          alert("Infection added");
          console.log(response.data);

          // reset input fields
          this.infection = {};

          // uncomment the following line if you want to redirect to /infections
          //this.$router.push("/infections");
        });
    },
  },
};
</script>