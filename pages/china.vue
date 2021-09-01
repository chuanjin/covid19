<template>
  <div>
    <b-card
      title="China"
      img-src=""
      img-alt="Image"
      img-top
      tag="article"
      style="max-width: 20rem;"
      class="mb-2"
      >
      <b-card-text>
        cases: {{ cases }}
      </b-card-text>

      <b-button href="/" variant="primary">Go back</b-button>
    </b-card>
  </div>

</template>

<script>

export default {

  data() {
    return {
      cases: 0,
      flag: ""
    }
  },

  async created() {
    const data = await this.$axios.$get("https://disease.sh/v3/covid-19/countries/china")
    this.cases = data.cases
  }

}
</script>
