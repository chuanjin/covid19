<template>
  <div>
    <b-container>
      <b-row>
        <b-col>
          <ul>
            <li v-for="country in labels">
              <NuxtLink :to="country">{{ country }} </NuxtLink>
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
      labels: ['China', 'US', 'UK', 'Canada', 'Germany', 'France', 'Italy', 'Australia', 'Sweden', 'India' ],
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
    this.vaccine = []
    try {
      for (let country of this.labels) {
        var data = await this.$axios.$get("https://disease.sh/v3/covid-19/vaccine/coverage/countries/" + country + "?lastdays=1")
        const vaccine = Object.values(data['timeline'])[0]
        this.vaccine.push(vaccine)
      }

      this.chartdata = {
        labels: this.labels,
        datasets: [{
          label: 'Vaccination',
          barPercentage: 0.8,
          data: this.vaccine,
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
