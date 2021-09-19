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
      loaded: true,
      chartdata: {
        labels: [1,2,3,4,5,6,7],
        datasets: [{
          label: 'Vaccination',
          barPercentage: 0.8,
          data: [65, 59, 80, 81, 56, 55, 40],
          backgroundColor: [
            'rgba(255, 99, 132, 0.2)',
            'rgba(255, 159, 64, 0.2)',
            'rgba(255, 205, 86, 0.2)',
            'rgba(75, 192, 192, 0.2)',
            'rgba(54, 162, 235, 0.2)',
            'rgba(153, 102, 255, 0.2)',
            'rgba(21, 203, 207, 0.2)'
          ],
          borderColor: [
            'rgb(255, 99, 132)',
            'rgb(255, 159, 64)',
            'rgb(255, 205, 86)',
            'rgb(75, 192, 192)',
            'rgb(54, 162, 235)',
            'rgb(153, 102, 255)',
            'rgb(201, 203, 207)'
          ],
          borderWidth: 1
        }]
      },
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

  }
}


</script>


<style>
#vaccine {
  background: black;
}
</style>
