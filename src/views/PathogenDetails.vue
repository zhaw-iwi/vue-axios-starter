<template>
  <div class="mb-5">
    <h1 class="mt-3">Pathogen (ID: {{ pathogenId }})</h1>
    <p>ICD-10: {{ pathogen.icd10 }}</p>
    <p>Incubation: {{ pathogen.incubation }}</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      pathogenId: this.$route.params.id,
      pathogen: { },
    };
  },
  mounted: function() {
    this.getPathogen();
  },
  methods: {
    getPathogen: function() {
      axios.get("http://localhost:8080/infections/pathogens/" + this.pathogenId )
      .then( response => {
        this.pathogen = response.data;
      })
    }
  }
};
</script>