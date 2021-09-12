<template>
  <div>
    <b-card
      title="China"
      :img-src="flag"
      img-alt="Image"
      img-top
      tag="article"
      style="max-width: 20rem;"
      class="mb-2"
      >
      <b-card-text>
        <ul>
          <li>Population: {{ population }}</li>
          <li>Total cases: {{ cases }}</li>
          <li>Today cases: {{ todayCases }}</li>
          <li>Total deaths: {{ deaths }}</li>
          <li>Today deaths: {{ todayDeaths }}</li>
          <li>Total recovered: {{ recovered }}</li>
          <li>Today recovered: {{ todayRecovered }}</li>
        </ul>
      </b-card-text>

      <b-button href="/" variant="primary">Go back</b-button>
    </b-card>
  </div>

</template>

<script>

export default {

  data() {
    return {
      population: 0,
      cases: 0,
      deaths: 0,
      recovered: 0,
      todayCases: 0,
      todayDeaths: 0,
      todayRecovered: 0,
      flag: ""
    }
  },

  async created() {
    const data = await this.$axios.$get("https://disease.sh/v3/covid-19/countries/china")
    this.population = data.population
    this.cases = data.cases
    this.todayCases = data.todayCases
    this.deaths = data.deaths
    this.todayDeaths = data.todayDeaths
    this.recovered = data.recovered
    this.todayRecovered = data.todayRecovered

    this.flag = data.countryInfo.flag
  }

}
</script>
