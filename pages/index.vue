<template>
  <div>
    <b-container>
      <b-row>
        <b-col>
          <ul>
            <li>
              <NuxtLink to="/china">China</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/">US</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/">UK</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/">Canada</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/">Germany</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/">France</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/">Italy</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/">Australia</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/">Sweden</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/">India</NuxtLink>
            </li>
          </ul>
        </b-col>
        <b-col>
          <BarChart v-if="loaded" :chartdata="chartdata" :options="options" />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>


<script>

export default {

  layout: 'default',

  data() {
    return {
      loaded: false,
      chartdata: null,
      labels: ['China', 'US', 'UK', 'Canada', 'Germany', 'France', 'Italy', 'Australia', 'Sweden', 'Inida' ],
      options: {
        scales: {
          yAxes: [{
            ticks: {
              beginAtZero: true
            }
          }]
        }
      }
    }
  },

  async mounted() {
    this.loaded = false
    try {
      var data = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/China?lastdays=1")
      const vaccine_China = Object.values(data['timeline'])[0]
      data = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/us?lastdays=1")
      const vaccine_US = Object.values(data['timeline'])[0]
      data = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/uk?lastdays=1")
      const vaccine_UK = Object.values(data['timeline'])[0]
      data = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/canada?lastdays=1")
      const vaccine_Canada = Object.values(data['timeline'])[0]
      data = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/germany?lastdays=1")
      const vaccine_Germany = Object.values(data['timeline'])[0]
      data = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/france?lastdays=1")
      const vaccine_France = Object.values(data['timeline'])[0]
      data = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/italy?lastdays=1")
      const vaccine_Italy = Object.values(data['timeline'])[0]
      data = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/australia?lastdays=1")
      const vaccine_Australia = Object.values(data['timeline'])[0]
      data = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/sweden?lastdays=1")
      const vaccine_Sweden = Object.values(data['timeline'])[0]
      data = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/india?lastdays=1")
      const vaccine_India = Object.values(data['timeline'])[0]
      this.chartdata = {
        labels: this.labels,
        datasets: [{
          label: 'Vaccination',
          barPercentage: 0.8,
          data: [vaccine_China, vaccine_US, vaccine_UK, vaccine_Canada, vaccine_Germany, vaccine_France, vaccine_Italy, vaccine_Australia, vaccine_Sweden, vaccine_India],
          backgroundColor: [
            'rgba(255, 99, 132, 0.2)',
            'rgba(255, 159, 64, 0.2)',
            'rgba(255, 205, 86, 0.2)',
            'rgba(75, 192, 192, 0.2)',
            'rgba(54, 162, 235, 0.2)',
            'rgba(153, 102, 255, 0.2)',
            'rgba(21, 203, 207, 0.2)',
            'rgba(25, 205, 86, 0.2)',
            'rgba(55, 99, 132, 0.2)',
            'rgba(205, 205, 186, 0.2)',
          ],
          borderColor: [
            'rgb(255, 99, 132)',
            'rgb(255, 159, 64)',
            'rgb(255, 205, 86)',
            'rgb(75, 192, 192)',
            'rgb(54, 162, 235)',
            'rgb(153, 102, 255)',
            'rgb(21, 203, 207)',
            'rgba(25, 205, 86)',
            'rgba(55, 99, 132)',
            'rgba(205, 205, 186)',
          ],
          borderWidth: 1
        }]
      }
      this.loaded = true
    } catch (e) {
      console.error(e)
    }
  }
}


</script>


<style>
#vaccine {
  background: black;
}
</style>
