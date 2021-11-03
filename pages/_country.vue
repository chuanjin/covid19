<template>
  <div>
    <client-only>
      <b-container>
        <b-row>
          <b-col>
            <b-card
              :title="country"
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
          </b-col>

          <b-col>
            <LineChart v-if="loaded" :chartdata="chartdata" />
          </b-col>
        </b-row>
      </b-container>
    </client-only>
  </div>

</template>


<script>

export default {

  data() {
    return {
      loaded: false,
      chartdata: null,
      population: 0,
      cases: 0,
      deaths: 0,
      recovered: 0,
      todayCases: 0,
      todayDeaths: 0,
      todayRecovered: 0,
      flag: "",
      country: this.$route.params.country
    }
  },

  async mounted() {
    this.loaded = false
    try {
      const data = await this.$axios.$get("https://disease.sh/v3/covid-19/countries/" + this.country)
      this.population = data.population
      this.cases = data.cases
      this.todayCases = data.todayCases
      this.deaths = data.deaths
      this.todayDeaths = data.todayDeaths
      this.recovered = data.recovered
      this.todayRecovered = data.todayRecovered
      this.flag = data.countryInfo.flag

      const vdata = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/" + this.country + "?lastdays=5")
      const vaccinations = Object.values(vdata['timeline'])
      const labels = Object.keys(vdata['timeline'])
      this.chartdata = {
        labels: labels,
        datasets: [
          {
            label: 'Vaccination Data',
            backgroundColor: '#F87979',
            borderColor: '#FF7979',
            data: vaccinations
          }
        ]
      }

      this.loaded = true
    } catch(e) {
      console.error(e)
    }
  }

}
</script>
