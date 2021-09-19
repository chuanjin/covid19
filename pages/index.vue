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
          <Vaccination />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  layout: 'default'
}
</script>


<style>
#vaccine {
  background: black;
}
</style>
